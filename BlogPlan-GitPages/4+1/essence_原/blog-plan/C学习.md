[toc]



#### 

malloc()

realloc();  在不更改原空间内容的情况下，对空间扩容

	#include <stdio.h>
	#include <string.h>
	#include <stdlib.h>
	
	int main()
	{
	   char *str;
	
	   /* 最初的内存分配 */
	   str = (char *) malloc(15);
	   strcpy(str, "runoob");
	   printf("String = %s,  Address = %u\n", str, str);
	
	   /* 重新分配内存 */
	   str = (char *) realloc(str, 25);
	   strcat(str, ".com");
	   printf("String = %s,  Address = %u\n", str, str);
	
	   free(str);
	
	   return(0);
	}
	
	//结果输出
	
	String = runoob,  Address = 3662685808
	String = runoob.com,  Address = 3662685808
	
	




​	
​	