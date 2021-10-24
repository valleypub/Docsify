
[toc]




#### Array -> ArrayList -> ```List<T>``` 的进化史

##### Array -> ArrayList
- 是什么
	1. 可以将 ArrayList想象成一种“会自动扩增容量的Array”
		- ArrayList内部封装了一个Object类型的数组，从一般的意义来说，它和数组没有本质的差别，甚至于ArrayList的许多方法，如Index、IndexOf、Contains、Sort等都是在内部数组的基础上直接调用Array的对应方法。
	2. 牺牲一定的效率和类型检查 -> 动态扩容。
		- Array（[]）：最高效；但是其容量固定且无法动态改变
		- ArrayList：  容量可动态增长；但牺牲效率；
		- why Array -> ArrayList 会牺牲效率？？
			- 每当执行Add、AddRange、Insert、InsertRange等添加元素的方法，都会检查内部数组的容量是否不够了，如果是，它就会以当前容量的两倍来重新构建一个数组，将旧元素Copy到新数组中，然后丢弃旧数组，在这个临界点的扩容操作，应该来说是比较影响效率的。
	3. ArrayList存入对象时，抛弃类型信息，所有对象屏蔽为Object，编译时不检查类型，但是运行时会报错。
- why 会Array -> ArrayList这样进化？？
	- 有些数组在声明时无法确定大小
4. 各自的使用场景
	1. 基于效率和类型检验，应尽可能使用Array
	2. 无法确定数组大小时才使用ArrayList

- 具体的区别：
	1. Array类型的变量在声明的同时必须进行实例化(至少得初始化数组的大小)，而ArrayList可以只是先声明。
	2. Array只能存储同构的对象，而ArrayList可以存储异构的对象
	3. 在CLR托管对中的存放方式不同：Array是始终是连续存放的，而ArrayList的存放不一定连续。
	4. Array对象的初始化必须只定指定大小，且创建后的数组大小是固定的，而ArrayList的大小可以动态指定，其大小可以在初始化时指定，也可以不指定，也就是说该对象的空间可以任意增加。
	5. Array不能够随意添加和删除其中的项，而ArrayList可以在任意位置插入和删除项。




##### ArrayList -> ```List<T>```
