##### 1.4.7 const 활용
포인터를 const로 정의하면, 그 포인터가 가리키는 값을 변경할 수 없다.

```c
int test(void)
{
	char s[] = "test";
    const char * p = s;
    p[0] = 'T';	/* const 포인터가 가리키는 주소의 값을 변경하려고 시도	*/
    
    return 0;
}
```

##### 1.4.8 const를 인자로 활용
```c
void strcopy(char * dst, const char * src)
{
	while (*src != '\0')
    	*(dst++) = *(src++);
    *dst = '\0';
}
```
- `const char *`로 정의한 포인터가 가리키는 값은 변경할 수 없다. (경고)
- `const char *` 포인터를 `char *`로 형변환 하는 것은 허용되지 않는다. (경고)

`const`를 반환하는 함수의 활용 예
```c
typedef enum { Black, White, Blue, Red, Green } Color;

const char * ColorName(Color c)
{
	const char * s;
    switch(c)
    {
    	case Black: s = "Black" break;
        case White: s = "White" break;
        case Blue : s = "Blue"  break;
        case Red  : s = "Red"   break;
        case Green: s = "Green" break;
        default   : s = "Unknown";
    }
    
    return s;
}
```

##### 1.4.9 const를 사용할 때 주의사항
`const`로 선언할 수 있는 것은 모두 const로 선언하는 것이 좋을 것처럼 여겨진다. 하지만 실제로는 그렇지 않다. 특히 함수가 깊게 중첩되는 경우에는 `const`를 사용하지 않는 것이 좋다.