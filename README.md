原项目https://github.com/Jonnyan404/zerotier-planet 
- 下载
```
    yum install docker docker-compose -y
    git clone https://github.com/feko2018/my-zerotier-planet.git
    cd my-zerotier-planet
```

- 配置docker-compose.yml
```
MYADDR=2.2.2.2 #改成自己的服务器公网IP
###可以修改8881，8882，8883为自定义端口对外
```

- 安装
```
    docker-compose up -d
    # 以下步骤为创建planet和moon
    docker cp mkmoonworld-x86_64 zerotier_planet:/tmp
    docker cp patch.sh zerotier_planet:/tmp
    docker exec -it zerotier_planet bash /tmp/patch.sh
    docker restart zerotier_planet
````

- 配置网络

然后浏览器访问 http://ip:8881 打开web控制台界面。用户admin密码看docker-compose.yml设置
登录后台，Add network创建网络后，在Networks里，快速创建Easy setup内网，

![image](https://user-images.githubusercontent.com/38614242/219947023-a5fe2cc3-e395-4f82-a75b-68ed216e88dd.png)
![image](https://user-images.githubusercontent.com/38614242/219947090-b937f274-3b70-4b8a-86dd-510e643a5786.png)

- 客户端下载planet和moon文件

浏览器访问http://ip:8883 打开planet和moon文件下载页面（亦可在项目根目录的`./ztncui/etc/myfs/`里获取）。

![image](https://user-images.githubusercontent.com/38614242/219952992-aec7b9e5-ecc3-44da-9326-bbec063f4e59.png)

- centos7安装zerotier客户端
```
curl -s https://install.zerotier.com/ | sudo bash
/bin/cp  planet  /var/lib/zerotier-one/planet  # 这个是上一步下载的文件planet
systemctl  restart  zerotier-one
zerotier-cli join 网络ID #这个网络ID在后台查看
```
![image](https://user-images.githubusercontent.com/38614242/219947470-ad5fec9b-44c6-4c92-aeb8-c789d228b0e0.png)

- 管理zerotier客户端授权
![image](https://user-images.githubusercontent.com/38614242/219947575-85682df0-3fd9-4a87-bdee-c5fc20f57ce3.png)

- Windows配置zerotier客户端
```
首先去zerotier官网下载一个zerotier客户端
或者https://bash.lanzoul.com/iAzeP0o24gvi 密码:4of6  记得解压再安装
安装后将 planet 文件（000000xxxxx.moon重命名planet）覆盖粘贴到C:\ProgramData\ZeroTier\One 中(这个目录是个隐藏目录，需要运允许查看隐藏目录才行)
Win+S 搜索 服务
找到ZeroTier One，并且重启服务
使用管理员身份打开PowerShell
执行zerotier-cli join 网络ID #这个网络ID在后台查看
看到join ok字样就成功了
```
