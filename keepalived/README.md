# Dockerfile
[2.0.8](https://github.com/thusihaveheard/docker/tree/master/keepalived/2.0.8/Dockerfile)

# 说明
<font color=red size=5>color=gray</font>  
$\color{red}{sdfh}$  
<font color='red'>*请不要使用2.0.8版本的源码，官方有bug!*</font>  
<font color='red'>*在制作镜像的时候也浮现了，具体地址 https://github.com/acassen/keepalived/issues/987*</font>  
   
 

本镜像不需传递任何参数，完全基于keepalived.conf挂载到容器的方案  

所以容器在启动的时候一定要挂载自定义keepalived.conf文件到容器里/etc/keepalived/keepalived.conf  

具体模板可参考上层的conf目录下的文件  

否则会走默认的keepalived.conf，将毫无意义！
