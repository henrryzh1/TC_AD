# windows10+Docker环境配置

激活注册阿里云镜像

![image-20210218204515483](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210218204515483.png)

登录阿里云镜像

![image-20210218205536996](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210218205536996.png)

创建镜像并Helloworld!测试。注意在build时“  .”是必须的，否则一直踩坑

![image-20210218212223704](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210218212223704.png)

## ![image-20210218212320702](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210218212320702.png)

初步的镜像搭建完成，进行镜像推送

![image-20210218213015855](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210218213015855.png)

进行基本测试

![image-20210218220408126](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210218220408126.png)

## 进行异常检测代码部署

代码：从github上下载baseline，部署到文件夹下

![image-20210220114831310](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210220114831310.png)

新建编写Dockerfile文件

```bash
#Base Images
##天池基础镜像
FROM registry.cn-shanghai.aliyuncs.com/tcc-public/pytorch:1.4-cuda10.1-py3
#### 把当前文件夹里的文件构建到镜像的根目录下
ADD . /
## 指定默认工作目录为根目录（需要把run.sh和生成的结果文件都放在该文件夹下，提交后才能运行）
WORKDIR /
## 镜像启动后统一执行 sh run.sh 
CMD ["sh", "run.sh"] 
```

构建镜像

![image-20210219110836289](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210219110836289.png)

进入容器配置环境

![image-20210219110931445](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210219110931445.png)

可以装个vim换源，这样快点

退出。然后将将镜像与容器连接

![image-20210219111133396](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210219111133396.png)

docker镜像push到阿里云镜像管理

整个docker搭建完毕！

接下来就是提交代码测试了

提交结果

![image-20210219111329518](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210219111329518.png)

存在错误需要修改代码，修改后将detect.py文件夹目录，采用baseline的训练好的模型best.pt

![image-20210220115014399](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210220115014399.png)

![image-20210220114533567](C:\Users\henrryzhou\AppData\Roaming\Typora\typora-user-images\image-20210220114533567.png)

