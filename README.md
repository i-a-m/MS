## 0x00:告示：
因为之前blog域名没有备案，已被禁止访问，现在可直接访问[123.206.56.205] ,
关于最新的细节，123.206.56.205>github>freebuf!
## 0x00 预览：
![image](https://github.com/0x024/MS/blob/master/data/temp/Screenshot%20from%202017-08-03%2019-10-53.png)

## 0x01环境：
[![](https://img.shields.io/badge/Ubuntu-mate-brightgreen.svg)]()
[![](https://img.shields.io/badge/Python-2.7-brightgreen.svg)]()
[![](https://img.shields.io/badge/OpenCV-3.2.0-brightgreen.svg)]()
[![](https://img.shields.io/badge/reapberry%20pi3-Model%20B%20-brightgreen.svg)]()

```
curl安装：
sudo apt-get install curl
```
```
LAMP:
sudo apt-get install apache2
sudo apt-get install php7.0
sudo apt-get install libapache2-mod-php7.0
sudo apt-get install mysql-server
sudo apt-get install phpmyadmin
sudo chmod 777 /var/www/html/
sudo ln -s /usr/share/phpmyadmin /var/www/html/
sudo sed -i 's/;extension=php_mbstring.dll/extension=php_mbstring.dll/' /etc/php/7.0/apache2/php.ini
sudo /etc/init.d/apache2 restart
mysql --user=root -p
CREATE DATABASE IF NOT EXISTS `MS` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
USE `MS`;
CREATE TABLE `None` (`None` int(11) NOT NULL) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
```
OpenCV 3.2.0
sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
git clone https://github.com/0x024/opencv.git    #为了方便,我已经将需要的包整合到我的github上，可以直接下载编译，
cd opencv #进入OpenCV目录
mkdir release
cd release
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..  #如果出现download ippicv失败的信息，重复运行本命令即可，还是不行，请挂代理！
make -j4  #这里的-j4代表job数，越大编译的速度越快,树莓派一定要-j1，
sudo make install
```


## 0x02 目录树:

![image](https://github.com/0x024/MS/blob/master/data/temp/Screenshot%20from%202017-08-03%2011-44-50.png)

## 0x03 执行:

```
运行前，

需要将./facepp/FaceAPI.py和BodyAPI.py中的api_key和api_secret换成你的
(为了便于您测试,我以将我的key放在里面，为了防止多人使用冲突，希望您后期换成个人的)
需要将./facepp/Dbconnect.py中的数据库信息换成自己的
（在搭建环境过程中，建议密码全部设置成ubuntu，方便记忆）

```

```java
python import.py     #将保存在./data/master/目录下的图片信息导入数据库

```


```java
python MS.py camera   #运行图像捕捉


```


```java
python MS.py check   #运行图像检测

```
## 0x04 :查看
- 可以打开127.0.0.1/phpmyadmin（默认的，如果牛的话，可以直接下命令行里查看）就可以看到
- ”io_data“-经过门口摄像头记录下来的图像所分析出来的信息，
- “walk_data”,可以记录下来，全程所有身体的运动情况，并且分析后写在数据库里面！
## 0x05：多说一句
1. 对于传感器的引脚的连接，这里我将VCC连接至 Pin#02，将Gnd连接至Pin#06，将Trig连接至Pin#03，将Echo连接至Pin#05，如果您要改动的话，也需要修改代码，慎思！
2. 对于手头没有树莓派或者传感器的朋友，我已经把ubuntu端的代码全部放在了Ubuntu文件夹里，可以fork下来，. 
	### 不同点
	- 运行方式。Python cam.py #运行摄像头 
			python MS.py #运行图像分析
	-  没有了传感器来控制摄像头开启，弊端就是，只要有运动物体，图像就会保存下来，
	-  把关闭摄像头的开关由时间控制，变成键盘控制，
	-  对于识别的身体面部图像，会在上面标记出该人名字，（因为树莓派计算能力有限）
	



