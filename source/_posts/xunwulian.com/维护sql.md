

### 1、设置失效日期为，激活日期加一年的那个月的一号

    update tb_cardinfo set user_end_date =  date_add(date_add(user_open_date, interval 1 year), interval - day( date_add(user_open_date, interval 1 year) ) + 1 day) ;

### 2、设置appName

    update tb_cardinfo c from app a set c.app_name = a.app_name where c.app_id = a.app_id;
 

### 3、设置套餐

    update tb_cardinfo set user_pkg = 1 where user_pkg = 10;
    update tb_cardinfo set user_pkg = 2 where user_pkg = 30;
    update tb_cardinfo set user_pkg = 3 where user_pkg = 70;
    update tb_cardinfo set user_pkg = 4 where user_pkg = 150;
    update tb_cardinfo set user_pkg = 5 where user_pkg = 500;
    update tb_cardinfo set user_pkg = 6 where user_pkg = 700;
    update tb_cardinfo set user_pkg = 7 where user_pkg = 1024;
    update tb_cardinfo set user_pkg = 8 where user_pkg = 2048;


## 导入卡号命令

    cat card_20170320.txt | awk '{print "insert into tb_cardinfo(msisdn, user_id, sub_user_id, app_id) values(\x27"$1"\x27"",\x27"1"\x27,""\x27\x27"",\x27zxtd\x27);"}' >card_20170320.sql 

    awk '{print "update tb_cardinfo set user_id = (select user_id from sys_user where username = \x27"$3"\x27), user_name =\x27"$3"\x27 where msisdn>=\x27"$1"\x27 and msisdn <=\x27"$2"\x27;"}'

    cat zxtd.txt | awk '{print "update tb_cardinfo set user_id = (select user_id from sys_user where username = \x27"$4"\x27), user_name =\x27"$4"\x27, app_id=\x27zxtd\x27, user_pkg="$6", user_open_date=\x27"$1"\x27, user_price="$7" where msisdn>=\x27"$2"\x27 and msisdn <=\x27"$3"\x27;"}' >zxtd.sql


