---
title: "Hello"
date: 2019-09-20T14:10:35+08:00
draft: 
---

# harbor漏洞修复 CVE-2019-16097

##　漏洞描述

参考　[Harbor安全漏洞通告和解决方案](https://mp.weixin.qq.com/s?__biz=MzAwNzUyNzI5Mw==&mid=2730791036&idx=1&sn=f33ef47364a5e345f0f85871bab6dd4e&chksm=bc4cfe6e8b3b77787e95e132e4cfd5663b84b4c39dc8e48c2bf1f5fa5918eaf4505003b082e6&mpshare=1&scene=1&srcid=&sharer_sharetime=1568940791906&sharer_shareid=817e8cc69928f92cc39558dc238bc996&key=3d64c8ab0dfd206adb610561efdd4a97fd03cc3b36fc5e578e5e4c2b70216138b7b5dd2185dc173ce88c0bd5afea13dffcf37a5216cd539ed4a87e571ce849dcc92ffc20ec54ee51f419fd6b7a356b6e&ascene=1&uin=NzgxMDMyNDE0&devicetype=Windows+7&version=62060833&lang=zh_CN&pass_ticket=RaS56E%2BVcANTGp9kkrLwritXAfxqmG7DcOANfTpFZM%2BAib83XGVAz9ZGkn%2FUnntF)

## 修复方式

升级harbor版本

## 升级步骤

1.停止已有harbor服务

	cd harbor
	docker-compose down
	cd ..

2.备份

	#备份程序
	mv harbor <backdir>/
    #备份数据库
	cp -r <harbor_data_dir>/database

3.下载新版程序

	#下载
	wget https://storage.googleapis.com/harbor-releases/release-1.9.0/harbor-offline-installer-v1.9.0.tgz

	#解压缩	
	tar xvf harbor-offline-installer-v1.9.0.tgz

4.升级迁移

	#拉去升级程序
	docker pull goharbor/harbor-migrator:v1.9.0
	
	#升级配置文件
	docker run -it --rm -v ${harbor_cfg}:/harbor-migration/harbor-cfg/harbor.yml -v ${harbor_yml}:/harbor-migration/harbor-cfg-out/harbor.yml goharbor/harbor-migrator:[tag] --cfg up
	
5.启动新程序
	
	cd harbor
	docker-compose -up
