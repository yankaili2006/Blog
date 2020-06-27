
### 参考链接

    https://zero-to-jupyterhub.readthedocs.io/en/latest/setup-jupyterhub/setup-jupyterhub.html

#### config.yaml

Generate a random hex string representing 32 bytes to use as a security token. Run this command in a terminal and copy the output:

    openssl rand -hex 32
    
Create and start editing a file called config.yaml. In the code snippet below we start the widely available nano editor, but any editor will do.

    nano config.yaml
    
Write the following into the config.yaml file but instead of writing <RANDOM-HEX> paste the generated hex string you copied in step 1.

    proxy:
      secretToken: "<4235da6ad3e92513ebf9da8377f91ac482629cb7e559a392595be5343ba24ceb>"
      
Note

It is common practice for Helm and Kubernetes YAML files to indent using two spaces.

Save the config.yaml file. In the nano editor this is done by pressing CTRL+X or CMD+X followed by a confirmation to save the changes.


#### Install JupyterHub
Make Helm aware of the JupyterHub Helm chart repository so you can install the JupyterHub chart from it without having to use a long URL name.

    helm repo add jupyterhub https://jupyterhub.github.io/helm-chart/
    helm repo update
    
This should show output like:

Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
...Successfully got an update from the "jupyterhub" chart repository
Update Complete. ⎈ Happy Helming!⎈

#### Now install the chart configured by your config.yaml by running this command from the directory that contains your config.yaml:

# Suggested values: advanced users of Kubernetes and Helm should feel
# free to use different values.

    helm upgrade --install jhub-release jupyterhub/jupyterhub \
      --namespace liyankai  \
      --version=0.8.2 \
      --values ../config.yaml
      
    cd /Users/liyankai/github/auto_config
    helm install jhub-liyankai ./jupyterhub --namespace liyankai --version=0.8.2 --values jupyterhub/values.yaml --timeout=30m
    helm install jhub-liyankai ./jupyterhub --namespace liyankai --version=0.8.2 --values ./config.yaml --timeout=30m
    
#### 配置oauth2

    https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/348
  
    auth:
      type: custom
      custom:
        className: 'oauthenticator.azuread.AzureAdOAuthenticator'
        config:
          client_id: "market"
          client_secret: "market"
          oauth_callback_url: "http://192.168.64.23:32234/hub/oauth_callback"
          token_url: "https://yangxing3-dev-console.tsingj.local:31813/api/api-sso/oauth/token"  

#### github oauth2

    https://github.com/settings/applications/new
    
    https://zero-to-jupyterhub.readthedocs.io/en/latest/administrator/security.html
    
多种授权方式

    https://zero-to-jupyterhub.readthedocs.io/en/0.7.0/authentication.html
    
go oauth2 server

    https://github.com/RichardKnop/go-oauth2-server
    https://github.com/go-oauth2/oauth2

#### https
    
    https://discourse.jupyter.org/t/setting-up-binder-with-jupyterhub-oauth/2266
    
    binderhub:
      config:
        BinderHub:
          auth_enabled: true
          hub_url: https://hub.cern.ch
          use_named_servers: true
      jupyterhub:
        singleuser:
          cmd: jupyterhub-singleuser
        hub:
          services:
            binder:
              oauth_redirect_uri: "https://binder.cern.ch/oauth_callback"
              oauth_client_id: "binder-oauth-client-test"
          allowNamedServers: true
          extraEnv:
            OAUTH2_AUTHORIZE_URL: https://oauth.web.cern.ch/OAuth/Authorize
            OAUTH2_TOKEN_URL: https://oauth.web.cern.ch/OAuth/Token
            OAUTH_CALLBACK_URL: https://hub.cern.ch/hub/oauth_callback
          extraConfig:
            hub_extra: |
              c.JupyterHub.redirect_to_server = False
            binder: |
              from kubespawner import KubeSpawner
    
              class BinderSpawner(KubeSpawner):
                def start(self):
                    if 'image' in self.user_options:
                      # binder service sets the image spec via user options
                      self.image = self.user_options['image']
                    return super().start()
              c.JupyterHub.spawner_class = BinderSpawner
        auth:
          type: custom
          custom:
            className: oauthenticator.generic.GenericOAuthenticator
            config:
              token_url: "https://oauth.web.cern.ch/OAuth/Token"
              userdata_url: "https://oauthresource.web.cern.ch/api/User"
              groupdata_url: "https://oauthresource.web.cern.ch/api/Group"
              userdata_method: GET
              userdata_params: {'state': 'state'}
              username_key: username
   
   
#### not used

    hub:
      cookieSecret: "[redacted]"
      db:
        type: sqlite-memory
    proxy:
      secretToken: "[redacted]"
      service:
        type: NodePort
        labels: {}
        annotations: {}
        nodePort: 30888
    rbac:
      enabled: false
      
      
      
    
    
    ingress:
      enabled: true
      hosts:
        - hub.127.0.0.1.xip.io
        
#### used

    proxy:
      secretToken: "<4235da6ad3e92513ebf9da8377f91ac482629cb7e559a392595be5343ba24ceb>"
      https:
        hosts:
          - 192.168.64.24
        letsencrypt:
          contactEmail: omitted@omitted.edu
    
    #ingress:
    #  annotations:
    #    kubernetes.io/tls-acme: "true"
    #  tls:
    #   - hosts:
    #      - 192.168.64.24
    #     secretName: kubelego-tls-jupyterhub
    
    singleuser:
      defaultUrl: "/lab"
    
    hub:
      service:
        loadBalancerIP: 192.168.64.24
      extraConfig:
        jupyterlab: |
          c.Spawner.cmd = ['jupyter-labhub']
    
    auth:
      admin:
        users:
          - admin
 
### used
    proxy:
      secretToken: "<4235da6ad3e92513ebf9da8377f91ac482629cb7e559a392595be5343ba24ceb>"
      service:
        type: NodePort
        nodePorts:
          http: 30080
          https: 30443
      enabled: true
      https:
        hosts:
          - liyankai.tsingj.local
        type: secret
        secret:
          name: 'my-secret'
    
    singleuser:
      defaultUrl: "/lab"
    
    hub:
      extraConfig:
        jupyterlab: |
          c.Spawner.cmd = ['jupyter-labhub']
      extraEnv:
        OAUTH2_AUTHORIZE_URL: https://yangxing3-dev-console.tsingj.local:31813/api/api-sso/oauth/authorize
        OAUTH2_TOKEN_URL: https://yangxing3-dev-console.tsingj.local:31813/api/api-sso/oauth/token
        OAUTH_CALLBACK_URL: https://liyankai.tsingj.local:30443/hub/oauth_callback
        #OAUTH_TLS_VERIFY: 0
    
    auth:
      type: custom
      custom:
        className: oauthenticator.generic.GenericOAuthenticator
        config:
          client_id: "market"
          client_secret: "market"
          token_url: https://yangxing3-dev-console.tsingj.local:31813/api/api-sso/oauth/token
          userdata_url: https://yangxing3-dev-console.tsingj.local:31813/api/userinfo
          userdata_method: GET
          userdata_params: {'state': 'state'}
          username_key: preferred_username
    
    
    auth:
      type: custom
      custom:
        className: jupyterhub-tsingjauthenticator.tsingj_auth.TsingjOAuthenticator
      TsingjOAuthenticator:
        enable_auth_state: true
        client_id: 'market'
        client_secret: 'market'
        oauth_callback_url: 'https://liyankai.tsingj.local:30443/hub/oauth_callback'
        