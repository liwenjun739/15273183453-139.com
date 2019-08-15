## 使用禅道Docker安装包安装

#### 一、下载地址

禅道开源版：     <http://dl.cnezsoft.com/zentao/docker/docker_zentao.zip>

数据库用户名：  **root**,默认密码：  **123456**。运行时，可以设置  **MYSQL_ROOT_PASSWORD**变量来更改密码。

可挂载目录

**/app/zentaopms**:该目录为禅道目录，里面包含禅道代码及附件上传目录。

**/var/lib/mysql**:该目录为数据库的数据目录。

#### 二、安装使用

注意：需要关闭下selinux

**1、构建镜像**

下载安装包，解压缩。 进入docker_zentao目录，执行命令 docker build -t [镜像名称] [Dockerfile所在目录]

```
docker build -t zentao ./
```

**2、运行镜像**

```
docker run --name [容器名称] -p [主机端口]:80 -v [主机代码目录]:/app/zentaopms -v [主机数据目录]:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=[数据库密码] -d [镜像名]:latest
```

例如

创建 /data/www /data/data 目录。

执行命令：

```
docker run --name zentao -p 80:80 -v /data/www:/app/zentaopms -v /data/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d zentao:latest
```

运行成功

![img](http://blog.cnezsoft.com/file.php?f=201811/f_0051d09ea269741151ee9ef09ab5bd79.png&t=png&o=&s=full&v=1533028736)

**3、安装禅道**



![通过浏览器访问http://ip，系统会自动转入安装程序。](https://www.zentao.net/file.php?f=201807/f_1c42c3c21c87edbc3c4f0a939981b56d&t=png&o=&s=&v=1530496689)

 上一步

通过浏览器访问http://ip，系统会自动转入安装程序。

下一步

![ä½¿ç¨äº§åé¡"éµå¾ªæä"¬çææåè®®ï¼ä¸å¾æèªå"é¤æ å¿ãé¾æ¥ã](https://www.zentao.net/file.php?f=201906/f_84182eea02e17387f1e09bbdbad50152&t=jpg&o=&s=&v=1560997299)



![æ£æ¥ç³"ç"å®è£ç¯å¢ï¼å¦è½¯ä"¶çæ¬ãè¯"åæéç­ãå¦æéè¯¯ææç¤ºæä½å³å¯ã](https://www.zentao.net/file.php?f=201807/f_6613767c57e1f60659d14418ae75eacb&t=png&o=&s=&v=1530496689)

![å¡"åæ°æ®åºç¸å³ä¿¡æ¯ï¼å¦æ°æ®åºå·²å­å¨ï¼å¯å¾éæ¸ç©ºç°ææ°æ®ã](https://www.zentao.net/file.php?f=201807/f_d8b759050d95fe79ce2f566fa8895877&t=png&o=&s=&v=1530496689)

![çæéç½®æä"¶my.phpï¼ç®¡çåå¯èªè¡ä¿®æ¹è®¾ç½®ï¼æ³éè£ç³"ç"åå é¤è¯¥æä"¶å³å¯ã](https://www.zentao.net/file.php?f=201807/f_dfd2c39254730e1b1e3385c0dcb74f1c&t=png&o=&s=&v=1530496689)



![è®¾ç½®ç®¡çåå¸å·åå·¥ä½æ¹å¼ã](https://www.zentao.net/file.php?f=201807/f_2dbe382eff3820893b6ea709eaa84b21&t=png&o=&s=&v=1530496689)

#### 三、升级

**1、重新构建镜像**

重新修改Dockerfile，重新运行构建镜像命令

![img](https://cdn.chanzhi.org/web/data/upload/201901/f_b7d687e81c194461fd6de2efddb9ee34.webp?v=190801)

```
docker build -t zentao ./
```

**2、关闭容器**

```
docker stop 容器ID
```

![img](https://cdn.chanzhi.org/web/data/upload/201901/f_422f3a20ac27483f910fec21244b9373.webp?v=190801)

```
docker stop 6b26b184f322
```

**3、用新镜像运行容器**

用之前运行镜像的命令，用新的镜像重新运行容器。

注意：[主机代码目录]、[主机数据目录]、mysql密码 必须和之前的容器一致。

**4、升级禅道**

![img](https://cdn.chanzhi.org/web/data/upload/201901/f_9ed6c623e670de83a5e5638761d41e0e.webp?v=190801)

在 [主机代码目录] 的 www 目录创建 ok.txt。

创建后，点击 继续更新。

![img](https://cdn.chanzhi.org/web/data/upload/201901/f_7e3deaa82d59f1019792e1a3713a651a.webp?v=190801)

升级成功。

#### 四、访问禅道数据库

##### 1、安装成功之后，确认下容器的ID：

![img](https://cdn.chanzhi.org/web/data/upload/201901/f_226895ff1e28da962e125c9cd844c783.webp?v=190801)

##### 2、进入docker容器：

执行下面命令，ID使用上面查询的ID即可。

```
docker exec -it cc8f97cdf51b /bin/bash
```

结果： ![img](https://cdn.chanzhi.org/web/data/upload/201901/f_77b7e0d70a31b4a272efb07efd8e2086.webp?v=190801)

##### 3、访问数据库：

密码默认是123456，但是运行镜像的时候  **MYSQL_ROOT_PASSWORD**修改密码的话，需要使用修改后的密码。

![img](https://cdn.chanzhi.org/web/data/upload/201901/f_c6eb7ec65c576001facd5f473d213da1.webp?v=190801)