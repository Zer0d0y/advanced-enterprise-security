设置File Permissions and Masks 文件权限和权限masks，System jobs（Cron）

##### 1.Verify Permissions on Files with Local Account Information and Credentials
chown root /etc/shadow
chgrp shadow /etc/shadow

chown root /etc/group
chgrp root /etc/group
chmod 644 /etc/group

chown root /etc/gshadow
chgrp shadow /etc/gshadow

chown root /etc/passwd
chgrp root /etc/passwd
chmod 0644 /etc/passwd


##### 2.Verify that Shared Library Files Have Restrictive Permissions & Have Root Ownership

DIRS1="/lib /lib64 /usr/lib"
for dirPath in $DIRS1; do
find $dirPath -perm /022 -type f -exec chmod go-w '{}' \;
done

for LIBDIR in /usr/lib /lib /lib64
do
if [ -d $LIBDIR ]
then
find -L $LIBDIR \! -user root -exec chown root {} \;
fi
done

##### 3.Verify that System Executables Have Restrictive Permissions & Have Root Ownership

DIRS2="/bin /usr/bin /usr/local/bin /sbin /usr/sbin /usr/local/sbin"
for dirPath in $DIRS2; do
find "$dirPath" -perm /022 -exec chmod go-w '{}' \;
done

find /bin/ /usr/bin/ /usr/local/bin/ /sbin/ /usr/sbin/ /usr/local/sbin/  \! -user root -execdir chown root {} \;

##### 4.system jobs ROOT only

chown root:root /etc/crontab
chmod og-rwx /etc/crontab

chown root:root /etc/cron.hourly
chmod og-rwx /etc/cron.hourly

chown root:root /etc/cron.daily
chmod og-rwx /etc/cron.daily

chown root:root /etc/cron.weekly
chmod og-rwx /etc/cron.weekly

chown root:root /etc/cron.monthly
chmod og-rwx /etc/cron.monthly

chown root:root /etc/cron.d
chmod og-rwx /etc/cron.d

