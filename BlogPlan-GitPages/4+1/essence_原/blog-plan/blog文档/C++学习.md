[toc]



# 目录
1.代码段短小 2.需重复大量使用的  函数 ，写成宏表达式，表达式只有一个返回值  

	#define RGB2Y(r,g,b) \
	((unsigned char)((66 * r + 129 * g + 25 * b + 128) >> 8) + 16)
	#define RGB2U(r,g,b) \
	((unsigned char)((-38 * r - 74 * g + 112 * b + 128) >> 8) + 128)
	#define RGB2V(r,g,b) \
	((unsigned char)((112 * r - 94 * g - 18 * b + 128) >> 8) + 128)





### define用法:

	#define K4A_DECLARE_HANDLE(_handle_name_)                                                                              \
	typedef struct _##_handle_name_                                                                                    \
	{                                                                                                                  \
	    size_t _rsvd; /**< Reserved, do not use. */                                                                    \
	} * _handle_name_;



### 泛化的形式:

    #define K4A_DECLARE_HANDLE(_handle_name_)                                                                              \
        typedef struct _##_handle_name_                                                                                    \
        {                                                                                                                  \
            size_t _rsvd; /**< Reserved, do not use. */                                                                    \
        } * _handle_name_;
        

配合:
	K4A_DECLARE_HANDLE(k4a_image_t);
	