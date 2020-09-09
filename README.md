# 电控部代码规范
# Electronic-control-code-specification

## 前言
	这是电控部三个人在某个周末突发奇想搞的电控部代码命名规范
		
## 文件规范	

### 文件形式
	新版框架中实现相近功能的代码应当存在于一对.c/.h文件之中，文件命名采用大驼峰式命名（MotorTask.c, MusicAutoPlay.h）
	
### 框架基本配置文件.h

### 源文件对应头文件.h
	源文件的开头应当包含以下内容
	
	/**
	 *********************************** COPYRIGHT 2020-2030 JiaoDragon ************************************
	 * @file       
	 * @brief      
	 * @note
	 * @author
	 * @Version    
	 * @Date   
	 *********************************** COPYRIGHT 2020-2030 JiaoDragon ************************************
	 */
	 
	 一个比较典型的例子是
	 
	/**
	 ***********************************(C) COPYRIGHT 2020-2030 JiaoDragon************************************
	 * @file       CallbackAdministration.h
	 * @brief      Centralized management of callback functions
	 * @note
	 * @author	   爱谁谁
	 * @Version    V1.0.0
	 * @Date       September-3-2020
	 ***********************************(C) COPYRIGHT 2020-2030 JiaoDragon************************************
	 */
	 
	 而后是头文件需要引用的一些头文件，包括但不限于C/C++标准库、当前任务（如音乐播放、OLED）需要引用的库文件。
	 
	 再之后是头文件的正式内容，大致包含以下6部分内容。

	/***	MAP	***/

	/***	CONSTANT VALUE	***/

	/***	TYPE DEFINE	***/

	/***	SPECIFIC INIT CONFIGURATION	***/

	/***	EXTERNAL VARIABLES	***/

	/***	APIs	***/

	其中MAP是对应的管脚映射，非主控板特定的映射关系应当采用二次定义的方式，包括但不限于句柄、定时器通道、GPIO；
	而后是常量的定义；
	接下来是枚举体、结构体、类的定义；
	和一些需要宏定义实现的初始值的赋值；
	最后是全局变量列表；
	以及函数接口列表。
	
	一个典型的例子是
	（等有缘人补上一个例子）
	
### 模块总头文件
	一些比较常见，经常性共同出现（如BSP）的文件应当存在一个总头文件，便于整个模块的引用。总头文件的命名应当为XXX_All.h/.hpp，其中XXX为模块名称。
	
## 变量命名规范
	
### 局部变量

### 静态全局变量
	
### 全局变量

## 函数命名规范

### 文件内函数命名规范
	函数的名称应当用下划线连接，其中首字母大写，第一部分应当为文件名称（除中断回调管理文件外），接下来为子模块名称，而后以此类推，最后补上函数的功能。
	
	例如Windmill_blade_color_init()、Windmill_motor_state_control()

### 类内函数命名规范
	大驼峰命名（Rx，ID之类的专有名词保持）。例：RxHandle,TxHandle,Handle,Reset,Init。读取/返回private的成员变量以Get/Set开头，例：SetTargetAngle，GetRxID
	
## 宏定义命名规范
	
## 注释规范
	
## 控制算法规范
	
## 类/结构体规范
### 类
* ***严禁new！！！*** （默认堆栈很小）
* 类内函数命名规范参见上文
* 命名用大驼峰，不加后缀。
* 构造函数里不需要写太多初始化，在Reset或Init中完成所有初始化。
* 用Handle函数完成对object的操作，例：调用Chassis：：chassis.Handle();即可完成整个底盘的intensity的计算
* 尽量用“读取”而不是“写入”，如：用遥控器控制底盘过程中，底盘电机的targetAngle的赋值过程最好在Chassis中而不是Remote中
* 上层类的object如chassis为对应类的静态成员变量，小驼峰命名。
* 函数实现尽量写在.cpp中。
* 用好inline和指针（减少数据传递量）
### 结构体
* 命名用大驼峰，加后缀_t
* 无需__packed
### 枚举
* 命名用大驼峰，加后缀_e
	
## git规范
	
