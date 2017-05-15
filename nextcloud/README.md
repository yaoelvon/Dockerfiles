# nextcloud

## 创建一个独立的容器网络

```
docker network create nextcloud
```

## 准备环境
创建一个文件夹，名字为cloud，在文件夹中新建一个文件Caddyfile，内容如下：
```
example.com {
  proxy / [你的本机ip地址]:2333 {
	transparent
  }
  log /var/log/caddy.log
  gzip
}
```

## 新建一个文件，叫做docker-compose.yml
内容跟本目录下docker-compose.yml相同


## 启动
```
docker-compose up -d
```

## 当mysql数据库配置错误时
报错：`Error while trying to create admin user:Failed to connect to the database:An exception occurred in driver:SQLSTATE[HY000] [2002] No such file or directory`，检查数据库配置是否正确。

## 将文件所属和组所属改为www-data
```
chown www-data:www-data ./data/cloud/config
chown www-data:www-data ./data/cloud/data
chown www-data:www-data ./data/cloud/apps
```
若不设置，会报错：Can't create or write into the data directory

## 将sqlite模式修改为mysql
进入cloud_cron容器，运行命令```php occ db:convert-type --all-apps mysql root db nextcloud```

```
root@guest:~/cloud/data/cloud/data/fengyao/files/md2release# docker exec -it cloud_cron /bin/bash
<l$ php occ db:convert-type --all-apps mysql root db nextcloud
The process control (PCNTL) extensions are required in case you want to interrupt long running commands - see http://php.net/manual/en/book.pcntl.php
What is the database password?
Creating schema in new database
oc_accounts
 1/1 [============================] 100%oc_activity
 45/45 [============================] 100%oc_activity_mq
    0 [>---------------------------]oc_addressbookchanges
 1/1 [============================] 100%oc_addressbooks
 2/2 [============================] 100%oc_admin_sections
 5/5 [============================] 100%oc_admin_settings
 10/10 [============================] 100%oc_appconfig
 99/99 [============================] 100%oc_authtoken
 3/3 [============================] 100%oc_bruteforce_attempts
 3/3 [============================] 100%oc_calendarchanges
    0 [>---------------------------]oc_calendarobjects
    0 [>---------------------------]oc_calendars
 2/2 [============================] 100%oc_calendarsubscriptions
    0 [>---------------------------]oc_cards
 1/1 [============================] 100%oc_cards_properties
 4/4 [============================] 100%oc_comments
    0 [>---------------------------]oc_comments_read_markers
    0 [>---------------------------]oc_credentials
    0 [>---------------------------]oc_dav_shares
    0 [>---------------------------]oc_federated_reshares
    0 [>---------------------------]oc_file_locks
 10/10 [============================] 100%oc_filecache
 57/57 [============================] 100%oc_files_trash
 4/4 [============================] 100%oc_flow_checks
    0 [>---------------------------]oc_flow_operations
    0 [>---------------------------]oc_group_admin
    0 [>---------------------------]oc_group_user
 1/1 [============================] 100%oc_groups
 1/1 [============================] 100%oc_jobs
 14/14 [============================] 100%oc_mimetypes
 16/16 [============================] 100%oc_mounts
 1/1 [============================] 100%oc_notifications
 2/2 [============================] 100%oc_preferences
 6/6 [============================] 100%oc_privatedata
    0 [>---------------------------]oc_properties
    0 [>---------------------------]oc_schedulingobjects
    0 [>---------------------------]oc_share
    0 [>---------------------------]oc_share_external


    0 [>---------------------------]oc_storages
 3/3 [============================] 100%oc_systemtag
    0 [>---------------------------]oc_systemtag_group
    0 [>---------------------------]oc_systemtag_object_mapping
    0 [>---------------------------]oc_trusted_servers
    0 [>---------------------------]oc_twofactor_backup_codes
    0 [>---------------------------]oc_users
 1/1 [============================] 100%oc_vcategory
    0 [>---------------------------]oc_vcategory_to_object
    0 [>---------------------------]www-data@248dbb952349:~/html$
```

## 参考
1.[Converting Database Type](https://docs.nextcloud.com/server/9/admin_manual/configuration_database/db_conversion.html)
2.[下一代私人云盘 NextCloud 的安装配置](http://www.jianshu.com/p/a2798b1ac8a4)