---
title: C++ 控制台居中输出
---

# C++ 控制台居中输出

思路：首先获取控制台屏幕缓冲区大小，再获取要输出的字符串的长度，到这里基本上就完成了，最后再移动光标到目标区域并输出，就大功告成了。
1. 获取控制台屏幕缓冲区大小

```cpp
HANDLE hOutput = GetStdHandle(STD_OUTPUT_HANDLE);
CONSOLE_SCREEN_BUFFER_INFO bInfo;
GetConsoleScreenBufferInfo(hOutput, &bInfo);
int dwSizeX=bInfo.dwSize.X,dwSizey=bInfo.dwSize.Y;
```
2. 获取要输出的字符串的长度

```cpp
int len=strlen(str);
```
3. 移动光标到目标区域

```cpp
COORD pos;
pos.X = x; //横坐标
pos.Y = y; //纵坐标
SetConsoleCursorPosition(hOut, pos);
```
完整代码

```cpp
#include<bits/stdc++.h>
#include<windows.h>//头文件 
using namespace std;
void gotoxy(HANDLE hOut, int x, int y)//移动光标 
{
	COORD pos;
	pos.X = x; //横坐标
	pos.Y = y; //纵坐标
	SetConsoleCursorPosition(hOut, pos);
}
void middle(char str[],int y)
{
	HANDLE hOutput = GetStdHandle(STD_OUTPUT_HANDLE);
    CONSOLE_SCREEN_BUFFER_INFO bInfo;
    GetConsoleScreenBufferInfo(hOutput, &bInfo);
    int dwSizeX=bInfo.dwSize.X,dwSizey=bInfo.dwSize.Y;//获取控制台屏幕缓冲区大小
    int len=strlen(str);//获取要输出的字符串的长度
	int x=dwSizeX/2-len/2;
	gotoxy(hOutput,x,y);//移动光标
	cout<<str;
}
int main()
{
	char str[100];
	int y;
	cin>>str>>y;//输入：输出的字符串，在第几行输出 
    middle(str,y);
	return 0;
}
```


![效果](https://img-blog.csdnimg.cn/f08920642e914d1fa03b3a39470165ea.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBASHVhbmdNWTIwMDc=,size_18,color_FFFFFF,t_70,g_se,x_16)



备注：本人不能保证该文章和该文章中的代码无错误、无缺陷，请自行判断后使用。如遇到问题请联系本人。转载请标明出处。