# aria2.conf
本项目提供一个不错的aria2配置文件，同时提供MacOS下的开机启动并可控的解决方案

### conf注意事项
使用请将配置文件中三处文件路径修改为自己的路径

将aria.conf放在`~/.aria2/`下

配置文件中没有启用input-file选项，理由在文件中有说明

### MacOS开机启动详细

将Aria2.sh放在你喜欢的地方😆

修改plist中sh的路径

将local.Aria2.plist放在`~/Library/LaunchAgents/`下

打开终端执行以下命令添加启动计划
 
	launchctl load ~/Library/LaunchAgents/local.Aria2.plist
	
添加完后任务便立刻开始

可以通过以下命令查看是否添加成功

    launchctl list | grep Aria2

可以通过以下命令进入screen查看aria2的运行状态

	screen -r Aria2
	
要退出screen请按下Ctrl+a后输入d

若要重启rpc，有两种方法

第一种:进入screen，按下Ctrl+C终止任务

使用`screen -dmS Aria2 /path/to/shell/Aria2.sh`开启aria-rpc

第二种:

	launchctl stop local.Aria2
	launchctl start local.Aria2

如果要删除开机启动 请把load改成unload

PS:shell中aria2使用了绝对路径，这是brew安装的aria2所在路径，之所以使用绝对路径是因为如果不这样做会有bug(似乎仅限于sh，bash应该就没事，要是没事干可以把shell的头改成bash)

其他系统的话可以把screen和aria2命令写在同一行里添加到rc.local

大概是这个样子

	su - username -c 'screen -dmS Aria2 aria2c --enable-rpc=true --input-file=/Users/name/.aria2/aria2.session --conf-path=/Users/name/.aria2/aria2'

嵌套太多可能会失败，建议拆成shell后添加到rc.local

完

