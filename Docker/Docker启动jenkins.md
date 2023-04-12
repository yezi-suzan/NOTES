
参考
--------
[https://github.com/jenkinsci/docker/blob/master/README.md](https://github.com/jenkinsci/docker/blob/master/README.md)

过程
----------
1. 获取最新版的Image
	```bash
	docker pull jenkins/jenkins:lts-jdk11
	```
2. 为持久化数据创建一个docker卷，
	```bash
	docker volume create --name jenkins-master-data
	```	
3. 运行
	
	```
	docker run -d \
	-p 8080:8080 -p 50000:50000 \
	--name jenkins-master \
	-v jenkins-master-data:/var/jenkins_home \
	--restart=on-failure \
	jenkins/jenkins:lts-jdk11
	```	
	> 参数解释：
	>	- `-d` 在后台运行（分离运行detach）
	>	- `-p` 绑定端口
	>	- `-v` 绑定卷
	>	- `--name` 命名
	>	- `--restart` 重启策略
4. 查看日志
	```
	docker logs -f jenkins-master
	```	
5. 测试是否启动
	```	
	curl http://localhost:8081/
	```
6. 停止（留出足够的时间让数据库完全关闭）
	```
	docker container stop --time=120 [[nexus]]
	```