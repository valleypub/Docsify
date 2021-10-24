[toc]

# 包
- 包在unity中是一个很重要的概念
- 
## 几种包
### 核心包(core packages)
### 预览包
### 已验证包
### 内置包
## Package Manager
## 创建自定义包
### 包的两个名字
- 一个包有两个名称：__正式名称__和__显示名称__，前者用于注册包，后者是用户在 Editor 中看到的面向用户的名称。
	- 显示名称应简短，但应在一定程度上表明包中的内容。除此以外，Unity Package Manager 对显示名称没有任何限制
	- 正式名称必须遵循 Unity Package Manager 命名约定，也就是使用反向域名表示法。名称必须满足以下条件：
		- 以 com.<公司名称> 开头。例如，一个正式的 Unity 包为“com.unity.timeline”。
		- 如果您希望正式名称显示在 UI 中，则长度不能超过 50 个字符。如果包名称不需要出现在 UI 中，则 Unity Package Manager 会将名称长度限制为不超过 214 个字符。
		- 只能包含小写字母、数字、连字符 (-)、下划线 (_) 和句点 (.)
		- 要指示嵌套的命名空间，请为命名空间添加一个句点作为后缀。例如，“com.unity.2d.animation”和“com.unity.2d.ik”。
### 包布局
- 这是正式 Unity 包遵循的包布局约定：
```
<root>
  ├── package.json
  ├── README.md
  ├── CHANGELOG.md
  ├── LICENSE.md
  ├── Editor
  │   ├── Unity.[YourPackageName].Editor.asmdef
  │   └── EditorExample.cs
  ├── Runtime
  │   ├── Unity.[YourPackageName].asmdef
  │   └── RuntimeExample.cs
  ├── Tests
  │   ├── Editor
  │   │   ├── Unity.[YourPackageName].Editor.Tests.asmdef
  │   │   └── EditorExampleTest.cs
  │   └── Runtime
  │        ├── Unity.[YourPackageName].Tests.asmdef
  │        └── RuntimeExampleTest.cs
  └── Documentation~
       └── [YourPackageName].md
```
#### Unity的Editor平台和Runtime平台
- why每个工程下都要有Editor版本的子文件夹和runtime版本的子文件夹？？他们究竟是什么？？
- 
### 包布局中每个组件的说明
#### 包清单(package.json)
#### 向包添加测试
- 与任何类型的开发一样，向包添加测试是一种好习惯。
- 必须完成三个步骤来设置对包的测试：
	- 1. 创建 C# 测试文件并将测试文件放在 Tests 文件夹下
	- 2. 为测试创建 asmdef 文件
	- 3. 为包启用测试

#### 程序集定义文件(.asmdef)
#### 共享包

### 依照包布局创建自定义包