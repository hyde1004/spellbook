#### JNA (Java Native Access)

###### Reference
 - [Java Native Access](https://github.com/java-native-access/jna)
 - [jni vs jna](http://knight76.tistory.com/entry/jni-vs-jna)

###### Example 1
Java에서 사용할 C Library를 만듭니다.
``` c
/* myLib.h*/
void printHello(void);
void printString(char* str);
```
``` c
/* myLib.c */
#include <stdio.h>

void printHello(void)
{
    printf("Hello World !!! jna\n");
}

void printString(char* str)
{
    printf("%s\n", str);
}
```

다음과 같이 so 파일을 생성합니다.
``` bash
gcc -c myLib.c -fPIC
gcc -shared -o myLib.so myLib.o
```

so 파일을 이용하는 Java 파일을 작성합니다.
``` java
/* HelloWorld.java */
import com.sun.jna.Library;
import com.sun.jna.Native;
import com.sun.jna.Platform;

public class HelloWorld {
    public static void main(String[] args) {
        CLibrary.INSTANCE.printHello();
        CLibrary.INSTANCE.printString("Hi\n");
     }
}

interface CLibrary extends Library {
        CLibrary INSTANCE = (CLibrary) Native.loadLibrary(
            ("/home/junggu.lee/work/sandbox/jan_ex/myLib.so"), CLibrary.class);

           void printHello();
           void printString(String str);
}
```

다음과 같이 Java를 build 및 실행합니다.
``` bash
# jna.jar를 다운로드 후,
javac -classpath jna-4.2.2.jar HelloWorld.java
java -classpath jna-4.2.2.jar:. HelloWorld
```

###### Example 2
다음은 Exmaple 1을 수정하여, 두 정수의 덧셈을 하는 예제입니다.

``` c
/* myLib.h */
int add(int a, int b);

/* myLib.c */
int add(int a, int b)
{
    return a + b;
}
```

``` java
/* HelloWorld.java */
import com.sun.jna.Library;
import com.sun.jna.Native;
import com.sun.jna.Platform;

public class HelloWorld
{
    public static void main(String[] args)
    {
        int a = CLibrary.INSTANCE.add(10, 20);
        System.out.println(a);
    }
}

interface CLibrary extends Library
{
    CLibrary INSTANCE = (CLibrary) Native.loadLibrary(
        ("./myLib.so"), CLibrary.class);
    int add(int a, int b);
}
```

다음과 같이 실행하였습니다.
``` bash
gcc -c myLib.c -fPIC
gcc -shared -o myLib.so myLib.o
javac -classpath jna-4.2.2.jar HelloWorld.java
java -classpath jna-4.2.2.jar:. HelloWorld
# 결과 : 30
```
