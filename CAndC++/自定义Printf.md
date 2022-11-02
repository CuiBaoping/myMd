# 自定义Printf函数

~~~c
#include <stdarg.h>
#include <stdio.h>

int Uart_Printf(char *format, ...)
{
    int ret = 0;
    char buffer[64];
    va_list aptr;

    va_start(aptr, format);
    ret = vsprintf((void *)buffer, format, aptr);
    va_end(aptr);

    if(0 < ret){
        Uart_Send_InterData(buffer, ret);	//调用通讯口，发送
    }
    
    return(ret);
}
~~~

