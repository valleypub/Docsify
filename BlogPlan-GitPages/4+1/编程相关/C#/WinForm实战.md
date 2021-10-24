[toc]


# Windows Forms概念

## Windows运行机制(事件-消息机制)

- 
- Windows通过WinAPI对这些机制提供了完整的支持，但对WinAPI的调用非常复杂，不便于使用。幸好.NET Framework对这些底层机制进行了很好的封装。


## 基于控件的编程



## 基于事件的编程





# Windows Form快速入门
### 新建一个Windows窗体程序

- 刚新建好的Windows窗体程序只有：

### 给程序新增 FormXXX 类型
- 新增的这个类型其实就是一种窗体的模板，可以使用下面2种方式来在Program.cs中的Main() 中进行窗体显示：
	1. Application类的方式
		- Application.Run(new Form1() )
	2. 实例化的方式
		- Form1 myForm = new Form1();
		- myForm.Show() + myForm.Close()
		- myForm.ShowDialog()



### 两种用户显示窗体
#### 无模式窗体
- 是什么		
- 什么情况使用
- how use it in code 
	- Show() + Close()
		- 使用show显示时必须使用close来关闭，why？？？？
	- Hide() 
		- 使用Hide()可简化窗体的不可见处理
```c#
using System;
using System.Collecions.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Threading;

namespace WindowsFormsApp1
{
    static class Program
    {
        /// <summary>
        /// 应用程序的主入口点。
        /// </summary>
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            //Application.Run(new Form1());

            Form2 myForm = new Form2();
            myForm.Show();
            Thread.Sleep(5000);
            
            //使用show显示时必须使用close来关闭
            myForm.Close();
        }
    }
}

```

#### 模式窗体
- 是什么
- 什么情况使用
- how use it in code
	- ShowDialog()
		- 这里直到对话框被用户消除对ShowDialog的调用时才会返回
```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Threading;

namespace WindowsFormsApp1
{
    static class Program
    {
        /// <summary>
        /// 应用程序的主入口点。
        /// </summary>
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            //Application.Run(new Form1());

            Form2 myForm = new Form2();
            
            //接受框的返回值
            DialogResult result = myForm.ShowDialog();
            if(result == DialogResult.OK)
            {
                
            }

        }
    }
}


```

- 确定DiaglogResult值
	- 是什么
		- DialogResult返回值一般表示的是用户是通过单击哪个按钮来关闭对话框的。这个返回值是从DialogResult枚举类型中获得的，它包含了如下值：
			<img src="C:\Users\king-kong\Desktop\BlogPlan\picture\C#\WinForm\DialogResult枚举.PNG" style="zoom:50%;" />
	- why need use这个值？？
		- 需要考虑返回值的一个原因就是调用对话框所调用的代码可以容易地判断对话框是否包含有效数据，如下所示：



### 控制Windows窗体应用程序

#### Application类 管理窗体
- 是什么
	- Application类用于为Windows窗体应用程序提供基本应用程序级别的操作。
- why need it
- how use it
	- __永远不要直接创建Application类的实例，应当调用由Application类公开的静态方法和属性__。
		- 由Application类提供的静态方法，如Run和Exit，可用于控制应用程序启动和终止的方式。
		- 由Application类公开的静态属性可以确定信息，如用于存储应用程序数据的路径。

##### 使用Application类启动窗体


##### 使用Application类确定应用程序路径信息
- 是什么
	- 当Windows窗体应用程序需要定位文件时，通常需要确定路径信息。
	- Application类包括可简化常用路径确定这一任务的属性，常用路径的例子有应用程序路径、用于存放应用程序数据的文件夹等。如：
		1. Application.StartupPath
			- 是
			- C:\Users\king-kong\Desktop\VS_Project\WindowsFormsApp1\WindowsFormsApp1\bin\Release
		2. Application.ExecutablePath
			- 是
			- C:\Users\king-kong\Desktop\VS_Project\WindowsFormsApp1\WindowsFormsApp1\bin\Release\WindowsFormsApp1.exe
		3. Application.CommonAppDataPath
			- 是Windwos窗体应用程序的所有用户共享的公共数据
			- C:\ProgramData\WindowsFormsApp1\WindowsFormsApp1\1.0.0.0
		4. Application.UserAppDataPath
			- 是
			- C:\Users\king-kong\AppData\Roaming\WindowsFormsApp1\WindowsFormsApp1\1.0.0.0
		5. Application.LocalUserAppDataPath
			- 是
			- C:\Users\king-kong\AppData\Local\WindowsFormsApp1\WindowsFormsApp1\1.0.0.0

##### 使用Application类关闭窗体应用程序
- 默认情况下，当主窗体关闭时应用程序就会退出。主窗体是什么？？？？

- 几种关闭的方式：
	1. Application.Exit()
		- Exit方法不会立即关闭应用程序，而是关闭所有消息泵，返回Run方法。
	2. 一般不要直接调用Exit，因为它会立刻关闭任何当前打开的窗体。关闭应用程序的一个较好的方法是调用主窗体的Close方法。主窗体就是自己实例化 or 用Application.Run()开启的那个FormX类的对象？？？
	3. 为了使用户在应用程序退出时能接收到通知，可以给Application.ApplicationExit事件添加一个事件处理程序。用这个事件处理程序来清除应用程序占有的资源，如下所示：
```c#
//窗体构造器￼
Form1()￼   
{￼          
	Application.ApplicationExit += new EventHandler(Application_ApplicationExit)；
}￼ 

private void Application_ApplicationExit (object sender，EventArgs e)￼   
{￼
    connection.Close()；￼     
    stream.Close()；￼
}


```

#### 使用Form属性改变窗体形态
- 设置窗口边框风格
	- 在FormX.Designer.cs中 使用 ```this.FormBorderStyle = System.Windows.Forms.FormBorderStyle.Sizable;``` 来更改FormX窗口模板的样式

2. 设置窗口背景色
	- 在FormX.Designer.cs中 使用 ```this.BackColor = ``` 
3. 创建窗口的大小
	- 在FormX.Designer.cs中 使用 ```this.Size = ``` 
4. 创建窗口的位置
	- 在FormX.Designer.cs中 使用 ```this.StartPosition = ``` 
		- 这个属性必须被设置为FormStartPosition枚举类型中的一个值。在默认情况下，StartPosition被设置为WindowsDefaultLocation。
5. 窗口标题标题
	- 在FormX.Designer.cs中 使用 ```this.Text = ``` 
6. 窗口当前状态
	- 执行应用程序时，FormWindowState属性会被更新。根据窗体的当前状态将FormWindowState设置为如下之一


#### 为窗体添加控件

##### 控件概述
- 是什么

- 注意：
	- 所有的控件都共享一组可通过操作影响控件外观和行为的公共属性(System.Windows.Forms命名空间中的__Control抽象类__)
	- 控件通过引发事件来通知开发人员在控件中出现了一些重要的事情。

##### 添加Button控件

##### TextBox控件类
- 什么场景来使用

- 通常用于可编辑文本，不过也可使其成为只读控件。
- how to use it	
	- string text = inputTextBox.Text;
	- int textLength = inputTextBox.TextLength;
	- 使用MaxLength属性限制用户输入的最大字符数，默认是32767(0111 1111 1111 1111) 16bit的最大正数。
		- inputTextBox.MaxLength = 16;
	- 删除文本框控件中的文本
		- inputTextBox.Clear(); 
	- 隐藏文本框控件中的密码
		1. 使用PasswordChar来指定文本框的掩码
			- inputTextBox.PasswordChar = ' * ';
		2. 还可以使用UseSystemPasswordChar属性。
			- 该属性的__优先级高于PasswordChar属性__。每当UseSystemPasswordChar设置为true时，将使用默认系统密码字符，并忽略由PasswordChar设置的任何字符。
	- 让文本框控件支持多行。默认文本框横向可以拉伸但纵向只支持单行
		- inputTextBox.Multiline = true;
	- WordWrap属性指示多行文本框控件能否自动换行。一行最多容纳多少字符？？？？？
		- inputTextBox.WordWrap = false;
	- 使用ScrollBars属性可指定滚动条，该属性必须使用ScrollBar枚举类型的值，默认为ScrollBars.None;
		- inputTextBox.ScrollBars = ScrollBars.None;
		- ![]()
		- 如果将WordWrap属性设置为true，则不管ScrollBars属性的值是什么，都不会显示水平滚动条。
	- 从多行TextBox中获取文本。
		1. 使用Text属性和单行文本框一样
			- string str = multilineTextBox.Text;
		2. 使用Lines属性
			- string[] contents = multilineTextBox.Lines;
	- 更改Enter/Tab按键在文本框控件中的作用。
		- 使用AcceptReturn属性更改焦点在文本框控件下时Enter按键的功能
			- 如果被设置为true，则指定在控件中按下Enter键时，会在控件中创建一行新的文本。
			- 如果设置为false，则指定按下Enter键时，将激活窗体的默认按钮。该属性的默认值为false。
		- 使用AcceptTab属性更改焦点在文本框控件下时Tab按键的功能
			- 如果被设置为ture，则指定在控件中按下Tab键时，将在控件中输入一个制表符。
			- 如果属性设置为false，用户就可通过按下Tab键来移动焦点。属性默认值为false。
	- 更改文本框控件的外观
		1. BorderStyle属性
			- 必须是BorderStyle枚举类型的值。默认情况下，BorderStyle属性设置为Fixed3D。
		2. 

- 常用事件
	1. TextChanged事件。当控件中的文本发生改变时，该事件就会被引发。


##### Lable控件类

- 注意：
	- Lable类虽然与其他控件有许多相同属性(如：)，但Lable类通常作为静态空间使用
	- 它从不接收输入焦点。相反，它把焦点按照Tab键的控制次序传递给下一控件。
		- 因此，与文本框或其他控件相关的标签控件经常被直接放置在相关控件前面，并提供在表示快捷键的字符前面附加&符号作为说明。这就使得用户可以使用Alt+相应快捷键来选择与标签相关联的控件

##### LinkLable控件类

- 是什么
	- LinkLabel控件可以向Windows窗体应用程序添加Web样式的链接。
	- 该控件常用于提供到相关网页的链接，或作为使用网页类用户界面的窗体的浏览控件来使用。如：LinkedClicked事件 + Process.Start("http://www.baidu.com") 来使用
	- 一切可以使用Label控件的地方，都可以使用LinkLabel控件。

- 事件
	- LinkClicked事件
		- 当用户单击标签控件时LinkLabe类会引发LinkClicked事件。




##### ListBox类

- 是什么	
	- ListBox控件显示一个项列表，用户可从中选择一项或多项。
	- 如果项总数超出可以显示的项数，则自动向ListBox控件添加滚动条。

- 在ListBox控件内部，维护着三个集合。
	- 这三个集合的用途如下：
		- ListBox.ObjectCollection包括ListBox控件中包含的所有项。
		- ListBox.SelectedObjectCollection包含选定项的集合，该集合是包含在ListBox控件中的项的子集。
		- ListBox.SelectedIndexCollection包含选定索引的集合，该集合是ListBox. ObjectCollection的索引的子集。这些索引指定选定的项。
		- ![]()
	- Items、SelectedItems和SelectedIndices属性提供对ListBox所使用的三个集合的访问。


- how use it
	1. 向ListBox中添加项目
		- 要向列表框中添加项目，实际上是向ListBox类所维护的ObjectCollection对象（即，listBox.Items）添加项目。有如下几种方法：
		1. 使用Add(newItem)在列表框的末尾插入
			- listBox.Items.Add(newItem);
		2. 使用Insert(0，newItem)来定点插入
			- listBox.Items.Insert( i，newItem);
			- 索引 i 的取值有限制：
				- 索引不得小于0，且不大于当前列表框中的项目数。如果传递了一个过小或过大的值作为索引，就会引发ArgumentoutOutOfRangeException异常。
		3. 使用AddRange()一次添加多个项目,AddRange()有两个重载版本：
			1. 插入一个string[]数组
				- listBox.Items.AddRange(string[] items)
			2. 将一个列表框中的内容复制到另一个ListBox控件
				- listBox.Items.AddRange(listBox2.Items)
		- 并没有任何限制规定只能向列表框中添加简单的字符串，也可以添加更复杂类型的实例。
	2. 从列表框中删除项目
		- 要从列表框中删除项，必须从ListBox对象的项目集合（即，listBox.Items）中删除项目。
		1. 使用RemoveAt( index ) 删除指定位置的项目
			- listBox.Items.RemoveAt(index)
			- index为待删除项目的索引，index的值必须在当前列表框的可用范围之内，如果传递的索引不在范围内会引发ArgumentOutOfRangeException异常
		2. 使用Remove( Items )
			- listBox.Items.Remove(item1)
		3. 使用Clear()删除列表框中的所有项目
			- listBox.Items.Clear()
	3. 选择列表框项目
		- 是什么
			- 列表框的默认操作就是在任何时刻最多只允许选定一项。不过，列表框可以容易地变为允许多重选择。
		1. 获取所选项的索引
			- int index = listBox.SelectedIndex;
			- 注意：
				- 如果支持多重选择，此时listBox.SelectedIndex返回的是其中一个选定项的索引。怎么确定是多个选定项中的哪一个？？？
		2. 获取所选项的引用
			1. SelectedItem属性
			2. SelectedIndices属性，返回的是一个索引构成的集合。
				- ListBox.SelectedIndexCollection indices = listBox. SelectedIndices;
				- 注意：
					- 对于多重选择ListBox，SelectedIndices属性返回一个集合，该集合包含ListBox中选定的所有项的索引。
					- 对于单项选择ListBox，此属性返回一个包含单个元素的集合，该元素包含ListBox中唯一选定项的索引。

			3. SelectedItems属性
				- ListBox. SelectedObjectCollection selectedItems = listBox.Selectedltems；￼
		3. 通过Code选择ListBox中项目
			- 是什么
				- 一般ListBox中的项目都是用户通过鼠标来进行选中的，但是也可以通过Code来进行选择
			1. 通过SelectedIndex属性来选中单个项目
				- listBox.SelectedIndex = 2;
				- 注意：
					- 通过SelectedIndex = -1来清楚单个项目的选定状态
					- 对于单选列表框，选择新项目会取消对当前选定项的选定状态。对于支持多项选择的列表框，选择新的项目则不会自动取消对当前任何选定项的选择。
			2. 使用SetSelected(0，true)
				- listBox.SetSelected(0，true);



- 事件
	1. SelectedIndexChanged事件
	2. SelectedValueChanged事件
		- 只要列表框控件中有选定或取消选定的项目，那么就会引发前两个事件。
	3. DoubleClick事件。
		- 当用户双击列表框中的项时，将生成DoubleClick事件


- 其他有用的属性
	- MultiColumn属性
	- Sorted属性



##### CheckedListBox
- 是什么
	- 它几乎能完成列表框可以完成的所有任务，__并且还可以在列表中的项旁边显示复选标记__

- how use it
	1. 添加项目
	2. 删除项目
	3. 选择项目


- 事件

- 有用的属性
	- ThreeDCheckedBoxes属性
		- checkedListBox.ThreeDCheckedBoxes = true;
		- 在默认情况下，这个属性被设为false，这就使得复选框具有平面外观。如果ThreeDCheckBoxes属性设为true，那么复选框就会具有轮廓分明的三维外观


##### ComboBox控件类
- 是什么	
	- 模拟下拉菜单。用的时候展开，不用的时候折叠。



#### 作为容器的控件

- 是什么


- Windows窗体设计器把控件放置到窗体表面时，会发生两件事。
	- 第一件事是控件的位置和大小被保存，且作为控件的属性使用，这些属性被序列化入窗体的InitializeComponents方法，会产生如下形式的代码：
		- <img src="C:\Users\king-kong\Desktop\BlogPlan\picture\C#\WinForm\控件加入Form做的第一件事.PNG" style="zoom:50%;" />
	- 第二件事是控件加入了Controls集合，它保存了窗体包含的每个子控件的引用。__一旦建立了保存关系，子控件就要接受其容器的环境属性__（例如，子控件要默认地使用容器的背景色。如果容器是隐藏的，那么子控件也会被隐藏；如果容器被禁用，那么子控件也会被禁用)。如下：
		- <img src="C:\Users\king-kong\Desktop\BlogPlan\picture\C#\WinForm\控件加入Form做的第二件事.PNG" style="zoom:50%;" />



- 容器是什么


- Form类是控件最常用的容器，但并非唯一可用的容器。还有另外两个控件类也可作为容器使用：
	- ● GroupBox为控件集合提供合理的分组，可以有标题，也可以没有。
	- ● Panel为其他控件提供可识别的分组。





#### WinForm下的事件处理
1. 给控件增加事件的3种方式：
	1. 双击窗体控制器中的 form or 控件
		- <img src="C:\Users\king-kong\Desktop\BlogPlan\picture\C#\WinForm\窗体控制器中双击控件.png" style="zoom:50%;" />
		- 优点：
			1. 简单
		- 缺点：
			1. 只能注册默认的事件，控件的好多其他有用的事件不能使用这种方式
	2. 通过窗体控制器右键打开form or 控件的属性界面，选择事件列表，双击想使用的事件，会自动在FormX.cs FormX.Designer.cs 中进行相应的代码改变
		- <img src="C:\Users\king-kong\Desktop\BlogPlan\picture\C#\WinForm\窗体控制器中右键打开属性面板.png" style="zoom:50%;" />
	3. 直接通过Code来
		1. 在FormX.cs中写一个委托 or 方法 
		2. 将FormX.cs中写的委托 or 方法 在FormX.Designer.cs中 注册进 FormX（即，this）or 控件（即，this.button1）的相应控件中

#### 将ESC/Enter按键 转换为 Button

#### 验证控件的内容



#### 




# Windows Form基础



# Windows Form进阶




# 实战:RssReader阅读器
## XML简介
- XML是什么
- why 有了 HTML 还需要 XML？？
	- 因为现在网络应用越来越广泛，仅仅靠HTML单一文件类型来处理千变万化的文档和数据已经力不从心，而且HTML本身语法十分不严密，严重影响网络信息传送和共享。人们早已经开始探讨用什么方法来满足网络上各种应用的需要。于是最终选择了XML作为下一代Web运用的数据传输和交互工具。

- HTML和XML的区别：本质区别是__网页将数据和显示混在一起(是定型的)，而XML则将数据和显示分开来(是非定型的)__
	- HTML是定型的
		- 有固定的标记来描述并显示网页内容。比如：<H1>表示首行标题有固定的尺寸，</H1>
	- XML是非定型的
	- 正是这种区别使得XML在网络应用和信息共享上方便、高效、可扩展。


## RSS简介
- 是什么
	- 一种不靠搜而靠“推”的新技术，却能够把信息“送”到我们面前。这就是RSS阅读器。(例如：微信订阅号、豆瓣APP、微博APP等首次进入的感兴趣领域的选择)
- why need it
- how use it

- 微信订阅号消息的推送方式 和 RSS的区别？？


## 常用的RSS阅读器


## 我们要开发的RSS阅读器
### 系统设计
#### 界面层
#### 业务逻辑层
#### 抽象类的设计