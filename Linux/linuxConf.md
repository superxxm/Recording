# LinuxConifg
### 使用`nohup & job`等命令在后台运行程序
1. 通过使用`&`操作符号让job在后台运行
例如：拷贝大型文件时，可以让其在后台拷贝，我们就可以在终端中继续work了

```
  cp /bigfile /usr/temp &
```
这样就会在后台执行拷贝任务了，但是注意这时我们虽然可以在终端中做别的事情了，但是不能关闭终端哦！
2. 使用`jabs`来查看当前系统中的job
>jobs命令参考  
命令名称：jobs  
使用权限：所有权限  
命令描述：列出系统中的job。注意：不是所有shell都能使用次命令  
语法：jobs [-p | -l] [-n] [-p] [-x] [job id]  
参数：  
-p | -l ： Report the process group ID and working directory of the jobs.  
-n      ： Display only jobs that have stopped or exited since last notified.  
-p      ： Displays only the process IDs for the process group leaders of the selected jobs.  
-x      ： Replace any job_id found in command or arguments with the corresponding  
           process group ID, and then execute command passing it arguments.  
job id  ： The job id.  
3. Suspend key和`bg`命令的使用(将一个正在运行的job放到后台运行)
使用挂起键(Suspend key,通常是Ctrl+z)将该任务挂起即暂停，然后使用`bg`命令在后台让该job恢复执行
例如：执行一个任务，将其暂停，然后在在后台启动

```
  cp bigfile bigfile.bakup
  ^z
  jobs
  [1]+ Stopped cp bigfile bigfile.bakup
  bg %1
```
在job挂起后，可以使用`bg`命令，让job恢复到刚才中断的地方继续运行并将其放到后台执行，使用`bg %job number`来指定你需要对哪一个job进行操作，这里的`%`号告诉系统后面的数字是一个job number。
>bg命令参考  
命令名称：bg  
使用权限：所有权限  
命令描述：在后台恢复已停止的job继续运行。注意该命令不能在所有的Unix的shell下运行  
语法：bg [-l] [-p] [-x] [job]  
参数：  
-l    ： Report the process group ID and working directory of the jobs.  
-p    ： Report only the process group ID of the jobs.  
-x    ： Replace any job_id found in command or arguments with the corresponding process    
         group ID, and then execute command passing it arguments.  
job   ： Specifies the job that you want to run in the background.  
4. 使用`fg`命令，将在后台的job转换到前台
用法类似`bg`命令
5. 结束一个job

```
  kill %job number
```
### Linux下的`Ctrl-Z`、`Ctrl-C`、`Ctrl-D`的具体意义

- __Ctrl-Z：__挂起键，按下时，系统会将正在运行的程序挂起，然后放到后台，程序没有真正停止，用户可以通过bg,fg来恢复到暂停前的上下文环境中继续执行。
- __Ctrl-C：__中断键，按下时，系统会发出一个中断信号给正在运行的程序和shell。具体的结果会根据程序的不同而不同。一些程序接收到这个信号后会立即结束并退出程序，一些程序会忽略这个信号，还有一些会采取其他的动作。当shell接收到这个中断信号时，会返回提示界面，并等待下一个命令。
- __Ctrl-D：__标准输入输出EOF，在使用标准输入输出的设备中，遇到该符号会认为到了结尾，会结束输入或输出。
