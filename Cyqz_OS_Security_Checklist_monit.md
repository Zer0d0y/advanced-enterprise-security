Monit
系统资源、文件/目录/文件系统、进程、网络监控，配置Email报警。

1.安装
apt-get install monit

2.配置
vi /etc/monit/monitrc

  set daemon 30            
  set logfile /var/log/monit.log
  set idfile /var/lib/monit/id
  set statefile /var/lib/monit/state


set mailserver smtp.exmail.qq.com port 465 username "monit@Zer0d0y.info" password "password here" using SSLAUTO
set alert Zer0d0y@Zer0d0y.info
set mail-format {
  from: monit@Zer0d0y.info
  subject: $SERVICE $EVENT at $DATE
  message: Monit $ACTION $SERVICE at $DATE on $HOST: $DESCRIPTION.
           Yours sincerely,
           monit
}

  set eventqueue
      basedir /var/lib/monit/events # set the base directory where events will be stored
      slots 100                     # optionally limit the queue size
 set httpd
     port 2812
     use address 127.0.0.1
     allow localhost
   include /etc/monit/conf.d/*

check file passwd_file with path "/etc/passwd"
        if changed checksum then alert
check file shadow_file with path "/etc/shadow"
        if changed checksum then alert
check file group_file with path "/etc/group"
        if changed checksum then alert
check file wosai-public-key with path "/home/wosai/.ssh/authorized_keys"
        if changed checksum then alert
check file root-public-key with path "/root/.ssh/authorized_keys"
        if changed checksum then alert
check file sshd_bin with path "/usr/sbin/sshd"
        if changed checksum then alert
check file sshd_config with path "/etc/ssh/sshd_config"
        if changed checksum then alert
check file monitrc with path "/etc/monit/monitrc"
        if changed checksum then alert

