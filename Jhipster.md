# Jhipster

## Installation

>  yarn installation

### Yarn
- 添加源
```bash
node -v
v10.4.1
npm -v
6.1.0
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list`
sudo apt-get update && sudo apt-get install yarn --fix-missing  |  
bqzhu@pc:~$ which -a node
/home/bqzhu/.nvm/versions/node/v10.4.1/bin/node
/opt/node/bin/node
/usr/local/bin/node
/usr/bin/node
bqzhu@pc:~$ sudo apt remove nodejs
bqzhu@pc:~$ which -a node
/home/bqzhu/.nvm/versions/node/v10.4.1/bin/node
/opt/node/bin/node
/usr/local/bin/node
```
> curl s : 表示下载的意思<br>
apt-key add keyname, 把下载的key添加到本地trusted数据库中。<br>
'-' : 表示标准输入;<br>
tee file :输出到标准输出的同时，保存到文件file中

### Docker
> [deepin docker install](https://segmentfault.com/a/1190000013637975)

### pip
> [pip install](https://www.jianshu.com/p/fd3415eb8618)

```console
wget https://bootstrap.pypa.io/get-pip.py  --no-check-certificate
sudo python get-pip.py
```

### Starting the application
<font color="red">可能是网络原因</font>
![webdriver-manager](webdriver-manager-error.jpg)

## Running generated tests
> Good software development is never complete without good testing.

## Jhipster Domain Language(JDL)
- Entity modeling on JDL studio
  - [`online-store.jh`](online-store.jh)
  ```bash
  jhipster import-jdl online-store.jh
  ```
