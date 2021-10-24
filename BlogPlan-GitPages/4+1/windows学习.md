[toc]


## 特殊文件夹路径

C:\Users\lenono\AppData\Roaming\Microsoft\Windows\Start Menu
```
此路径下配置的是在 开始菜单里可见的程序???
```

C:\Windows\System32
```
cmd.exe


```
C:\Windows\System32\WindowsPowerShell\v1.0
```
powershell所在的位置
```


## windows环境变量

```
用户变量只对某一用户有效，如果一台电脑多个用户同时使用，为了防止配置的环境变量相互影响，所以每个用户各自维护一个至多自己有用的环境变量(如:共用一个环境变量时，如果不同用户使用的不同版本的软件具有相同的名字如devenv.exe这样的话，那每次只会打开环境变量最上面的那个，因为采用的是"顺序查询"+"剪枝")

系统环境变量，对整个电脑的所有用户都生效。

如果电脑只有一个用户在使用,这样其实只需要配置"系统环境变量"就可以了

```
```
系统环境变量 优先于 用户变量。
每次先查询系统环境变量，再查询用户变量。
```
```
环境变量目前不支持重名的路径???
如：

```

### 用户变量

### 系统变量
```
set(cmd.exe下,powershell下不行)   查看系统环境变量

```
#### 可以使用% %对变量名进行拼接

%变量名%	==	变量值
变量值	== %变量名%\变量值

%SystemRoot%\system32

```
常用：
%USERPROFILE%  =C:\Users\用户名
%SystemRoot%  =C:\WINDOWS
%SystemDrive%  =C:
%APPDATA%  =C:\Users\用户名\AppData\Roaming
%LOCALAPPDATA%  =C:\Users\用户名\AppData\Local
%windir%  =C:\WINDOWS
%Path%  =C:\Windows\system32;C:\Windows; 
%ProgramData%  =C:\ProgramData
%ProgramFiles%  =C:\Program  Files
%ProgramFiles(x86)%  =C:\Program  Files  (x86)

其他：
%ALLUSERSPROFILE%  =C:\ProgramData
%CommonProgramFiles%  =C:\Program  Files\Common  Files
%CommonProgramFiles(x86)%  =C:\Program  Files  (x86)\Common  Files
%CommonProgramW6432%  =C:\Program  Files\Common  Files
%COMPUTERNAME%  =MyPC
%ComSpec%  =C:\WINDOWS\system32\cmd.exe
%HOMEDRIVE%  =C:
%HOMEPATH%  =\Users\用户名
%LOGONSERVER%  =\\MicrosoftAccount
%OS%  =Windows_NT
%ProgramW6432%  =C:\Program  Files   
%PUBLIC%  =C:\Users\Public 
%TEMP%  =C:\Users\用户名\AppData\Local\Temp
%TMP%  =C:\Users\用户名\AppData\Local\Temp
%USERDOMAIN%  =MyPC 
%USERNAME%  =用户名
```

#### 可以使用 %变量名% 跳转到相应的路径

可以在"运行"(win+R)中输入，%变量名% 来跳转到相应的文件夹

可以在 cmd.exe 中 输入  cd %变量名%  来进行跳转


### powershell环境变量
```
powershell的环境变量机制与 机器环境变量不太一样。
```
可以使用 $env: 来以机器环境变量的方式使用环境变量
```
注：
1. $env：中的环境变量只是机器环境变量的一个副本，即使你更改了它，下一次重新打开时，又会恢复如初。（.NET方法更新环境变量除外）

2. 通过$env:，这就提示powershell忽略基本的variable:驱动器，而是去环境变量env:驱动器中寻找变量

3. (环境变量==普通变量一样使用) 为了和其它变量保持一致，powershell环境变量也可以象其它变量那样使用。比如你可以把它插入到文本中。
PS> "My computer name $env:COMPUTERNAME"

```
**常用命令**

*1. 显示环境变量*
```
ls env:
```
*2. 读取环境变量*
```
$env:变量名

```
*3. 新建环境变量*
```
$env: 变量名 = "变量值"
$env: workdir = "%APPDATA%\workdir"
```
*4. 删除环境变量*
```
del env:变量名
```
*6. 更新环境变量*
```
$env: os = "系统名"
PS> $env:OS
Windows_NT
PS>  $env:OS="Redhat Linux"
PS> $env:OS
Redhat Linux
```
**上述对于环境变量的操作只会影响当前powershell会话，并没有更新在机器上。
.NET方法[environment]::SetEnvironmentvariable操作可以立刻生效.**
*7.永久改变powershel的环境变量*
```
PS> [environment]::SetEnvironmentvariable("Path", ";c:\powershellscript", "User")
PS> [environment]::GetEnvironmentvariable("Path", "User")
;c:\powershellscript
```



## cmd.exe 与 powershell


### 
管道
|
重定向
>		覆盖
>																				
>	>	追加

get-conent	文件绝对路径(支持linux方式)

### powershell常用命令
[powershell命令中文学习网站](https://www.pstips.net/powershell-online-tutorials#Powershell%E4%BA%A4%E4%BA%92%E5%BC%8F)

cmd        进入cmd模式
exit	退回powershell

netstat
ipconfig
route print

"命令名"      看作字符串
&"命令名"   看作命令来执行
```
PS C:\PS> "ls"
ls
PS C:\PS> &"ls"

    Directory: C:\PS

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2011/11/23     17:25            ABC
-a---        2011/11/23     17:36         14 a.txt
-a---        2011/11/23     17:25          0 b.txt
-a---        2011/11/23     17:25          0 c.txt
-a---        2011/11/23     17:25          0 d.txt
-a---        2011/11/23     17:37        242 test.txt
```

数学运算可以直接运行
```
PS C:\pstest> 1+2+3
6
PS C:\pstest> 0xABCD
43981
PS C:\pstest> 3.14*10*10
314
PS C:\pstest> 1+3-(2.4-5)*(7.899-4.444)
12.983
```
可以识别特殊单位:KB，MB，GB，TB，PB
```
PS C:\pstest> 1pb/1tb
1024
PS C:\pstest> 1tb/1gb
1024
PS C:\pstest> 1gb/1kb
1048576
PS C:\pstest> 1gb/20mb*10kb
524288
```

cmdlet是什么????
```

```

powershell执行脚本
`脚本和批处理都属于伪可执行文件，它们只是包含了若干命令行解释器能够解释和执行的命令行代码。`
**powershell执行脚本比cmd更安全**

```
cmd中可以使用 同名.bat文件 对 内置命令 进行覆盖,
powershell会优先运行 内置命令
```
**powershell可以执行两种脚本：.bat(.cmd), .psl**
