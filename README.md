
## 使用
#### 1.编译
```
docker build -t docker-registry.tfgzs.net/tfgzs/haproxy:1.6-1  ./
```
#### 2 在宿主机中存放配置文件
```
1.在宿主机创建/volume/haproxy目录作为我们的配置文件目录
	mkdir /volume/haproxy
2.将我们需要的配置文件放入到/volume/haproxy配置目录中
	cp haproxy.cfg /volume/haproxy/haproxy.cfg
	cp tfgzs.pem /volume/haproxy/tfgzs.pem
```
#### 2运行（生产环境）
```
docker run  -d --restart=always -p 80:80 -p 443:443 --name=haproxy -v /volume/haproxy:/usr/local/etc/haproxy:ro   docker-registry.tfgzs.net/tfgzs/haproxy:1.6-1   

说明：-v /volume/haproxy:/usr/local/etc/haproxy:ro  后面的:ro代表只读权限
```
#### 3.调试（测试环境，覆盖了entrypoint要执行的命令）
```
docker run -it --entrypoint /bin/bash -p 80:80 -p 443:443 --name=haproxy -v /volume/haproxy:/usr/local/etc/haproxy   docker-registry.tfgzs.net/tfgzs/haproxy:1.6-1   
```

### 注意：
如果你要自己编译Dockerfile,注意.sh文件的执行权限
```
    chmod 777  demo.sh      自己获取执行权
    chmod a+x  demo.sh      给所有人加上可执行权限，包括所有者，所属组，和其他人
    chmod o+x  demo.sh      只是给其他人加上可执行权限
```

### ACL定制法则：
     开放策略：拒绝所有，只开放已知  
     拒绝策略：允许所有，只拒绝某些 

### 参考文档
http://cbonte.github.io/haproxy-dconv/1.6/configuration.html  
http://www.ttlsa.com/linux/haproxy-study-tutorial/

https://hub.docker.com/r/rafpe/docker-haproxy-rsyslog/
https://rafpe.ninja/2016/05/16/haproxy-logging-within-docker-container/

 

