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
	 ***********************************(C) COPYRIGHT 2020-2030 JiaoDragon************************************
	 * @file       
	 * @brief      
	 * @note
	 * @Version    
	 * @Date   
	 ***********************************(C) COPYRIGHT 2020-2030 JiaoDragon************************************
	 */
	 
	 一个比较典型的例子是
	 
	/**
	 ***********************************(C) COPYRIGHT 2020-2030 JiaoDragon************************************
	 * @file       CallbackAdministration.h
	 * @brief      Centralized management of callback functions
	 * @note
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
	
	
## 变量命名规范
	
### 局部变量

### 静态全局变量
	
### 全局变量

## 函数命名规范

## 宏定义命名规范
	
## 注释规范

## 控制算法规范

## 类/结构体规范

## git规范
