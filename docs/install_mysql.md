#### ubuntu install mysql

1.install process  
+ 1.[官网下载deb插件](http://dev.mysql.com/downloads/repo/apt/.)

+ 2.install deb
    >sudo dpkg -i mysql-apt-config_0..***_all.deb

+ >sudo apt update

+ >sudo apt install mysql-client mysql-server mysql-workbench

2.ubuntu uninstall mysql

+ >sudo apt-get autoremove --purge mysql-server-5.7

+ >sudo apt-get remove mysql-server

+ >sudo apt-get autoremove mysql-server 

+ >sudo apt-get remove mysql-common

+ >sudo rm -rf /etc/mysql/ /var/lib/mysql


3.clean

+ >dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P

+ >sudo apt autoremove

+ >sudo apt autoreclean
