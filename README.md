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
	常见的变量命名方式有很多，比如驼峰命名法(Camel-Case),匈牙利命名法等。由于匈牙利命名法具有较大的争议性，而实际操作中驼峰命名法也能够很好地体现变量的功能或含义，因而我们决定统一采用驼峰命名法命名变量，即：
	变量如果由两个及以上的单词组合而成，则第一个单词的首字母小写，其余单词的首字母全部大写。
	例如：targetAngle realAngle等等，这边不再赘述。
	另外，尽量避免使用宏定义，宏定义在很多情况下会影响编译的效率，或者造成一些意想不到的错误。
	如果需要用宏定义定义一个常数，不妨用如下的方式：
	以工程车为例，如果我要定义一个关于横移电机转动速度的常数，那么我可以在header文件中：
	inline constexpr uint32_t CROSS_MOVE_SPEED = 10;
	以此来完成常量的声明。
### 局部变量
	采用驼峰命名法，确定好变量的类型，不要错乱。
	可以用uint8_t来代替bool。
	一般常量或者计数器可以用uint32_t 自行酌情处理
	变量要体现其内涵或者是功能，比如：
	targetAngle : 目标角度
	presentTarget : 当前目标
	clawInited : 爪子是否已经初始化过了

	在命名变量的时候，最好写全单词，不要嫌烦，大多数IDE都有补全功能，一个完整的变量名更加易读。
	在变量名过长的时候，可考虑采用下划线，将变量按照语义分成若干个部分，每个部分确定一个语义。

	有些情况下可以采用公认的缩写：
	argument 可缩写为 arg 
	buffer 可缩写为 buff 
	clock 可缩写为 clk 
	command 可缩写为 cmd 
	compare 可缩写为 cmp 
	configuration 可缩写为 cfg 
	device 可缩写为 dev 
	error 可缩写为 err 
	hexadecimal 可缩写为 hex 
	increment 可缩写为 inc、 
	initialize 可缩写为 init 
	maximum 可缩写为 max 
	message 可缩写为 msg 
	minimum 可缩写为 min 
	parameter 可缩写为 para 
	previous 可缩写为 prev 
	register 可缩写为 reg 
	semaphore 可缩写为 sem 
	statistic 可缩写为 stat 
	synchronize 可缩写为 sync 
	temp 可缩写为 tmp

### 静态全局变量
 
### 全局变量
	全局常数建议采用全大写 比如:MAX_CROSS_TARGETANGLE,CROSS_MOVE_SPEED等等	
## 函数命名规范

### 文件内函数命名规范
	大驼峰命名（Rx，ID之类的专有名词保持），例：MainControlLoop。
	如果有多个专有名词叠加应当以下划线进行分割，例：HAL_CAN_RxCpltCallback。

### 类内函数命名规范
	大驼峰命名（Rx，ID之类的专有名词保持）。例：RxHandle,TxHandle,Handle,Reset,Init。
	读取/返回private的成员变量以Get/Set开头，例：SetTargetAngle，GetRxID。

## 宏定义命名规范

```
全部使用大写字母，单词之间加下划线进行分割（枚举同样建议使用此方式定义）。例：#define PI_ROUNDED 3.14。
（来自华为C语言规范）除非必要，应尽可能使用函数代替宏。宏对比函数，有一些明显的缺点：
1.宏缺乏类型检查，不如函数调用检查严格。
2.宏展开可能会产生意想不到的副作用，如#define SQUARE(a) (a) * (a)这样的定义，如果是SQUARE(i++)，就会导致i被加两次；如果是函数调用double square(double a) {return a * a;}则不会有此副作用。
3.以宏形式写的代码难以调试难以打断点，不利于定位问题。
4.宏如果调用的很多，会造成代码空间的浪费，不如函数空间效率高。
```

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
