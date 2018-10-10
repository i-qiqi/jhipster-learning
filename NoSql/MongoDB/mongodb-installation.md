# MongoDB
> [Install MongoDB Community Edition on Debian](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-debian/)
>
> [deepin 安装 mongodb 数据库](Install MongoDB Community Edition on Debian)

## Installation Guide(Community Edition)
- Using .deb Packages
```bash
# Import  the public key used by the package management system.
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
#  Create the source list dile using appropriate for the your version of Debian or other
echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#  Issue the following command to reload the local package database.
sudo apt-get update
# Install the MongoDB pacakges.
# if latest version
sudo apt-get install -y mongodb-org
# if a specific release
sudo apt-get install -y mongodb-org=4.0.2 mongodb-org-server=4.0.2 mongodb-org-shell=4.0.2 mongodb-org-mongos=4.0.2 mongodb-org-tools=4.0.2
# To prevent unintended upgrades
echo "mongodb-org hold" | sudo dpkg --set-selections
echo "mongodb-org-server hold" | sudo dpkg --set-selections
echo "mongodb-org-shell hold" | sudo dpkg --set-selections
echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
echo "mongodb-org-tools hold" | sudo dpkg --set-selections
```
- Run the MongoDV CE
 Most Unix-like operating systems limit the system resources that a session may use. These limits may negatively impact MongoDB operation. See UNIX ulimit Settings for more information.
- by default ,
  - its data files in `/var/lib/mongodb`;
  - Its log files in `/var/log/mongodb`;
  -  we can specify alternate log and data file directories in `/etc/mongodb.conf`

 ```bash
# Start MongoDB
sudo service mongod start
# Verify that MongoDB has started successfully
cat /var/log/mongodb/mongod.log |grep port
# Stop MongoDB.
sudo service mongod stop
# Restart MongoDB
sudo service mongod restart
# Begin using MongoDB,Start a mongo shell on the same host machine as the mongod. Use the --host command line option to specify the localhost address (in this case 127.0.0.1) and port that the mongod listens on
mongo --hoosr 127.0.0.1:27017
# 设置开机启动或禁用 MOngoDB 开机自启
sudo systemctl enable mongod
```
## Uninstall ...
