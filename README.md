github
======

##多个github账号的多ssh keys 配置##
同一个机子上对多个github账号操作会有什么影响；						
导致只有一个ssh keys而无法提交，所以需要配置多个ssh keys（只要你知道对方的账号和密码是可以提交的)



###1.创建另外一对ssh keys 为work_rsa###
	$ ssh-keygen -t rsa -C “mashuangshaung@Lirange.com”;
保存ssh keys为work_rsa

###2.添加新的身份信息###
	$ eval “(ssh-agent -s)”												
	$ ssh-add ～/.ssh/work_rsa
###3.配置/.ssh/config###

.ssh目录下新建config文件，我们需要通过Host别名，将不同的账号区分开来。			


	Host mashuangshuang.github.com				
		HostName github.com				
		PreferredAuthentications publickey			
		IdentityFile ~/.ssh/id_rsa		



	Host FEsy.github.com	
		HostName github.com	
		PreferredAuthentications publickey	
		IdentityFile ~/.ssh/FEsy_rsa	


	Host work.XXX.com	
		HostName XXX.com	
		PreferredAuthentications publickey	
		IdentityFile ~/.ssh/work_rsa	

###4.登录测试###

	$ ssh -T mashuangshaung.github.com	
	
	$ ssh -T FEsy.github.com	
	
	结果如下	
	![登录成功](./img/gitlogin.jpg)