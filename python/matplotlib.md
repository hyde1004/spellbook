#### matplotlib 이용하기
###### Reference
 - [파이썬 그래프 그리기](https://wikidocs.net/1019)
 - [Pyplot tutorial](http://matplotlib.org/users/pyplot_tutorial.html)
 - [matplotlib Tutorials](http://mple.m-artwork.eu/tutorial)
 - [matplotlib - 2D and 3D plotting in Python](http://nbviewer.ipython.org/github/jrjohansson/scientific-python-lectures/blob/master/Lecture-4-Matplotlib.ipynb)
 - [Basic Data Plotting with Matplotlib Part 2: Lines, Points & Formatting](http://bespokeblog.wordpress.com/2011/07/07/basic-data-plotting-with-matplotlib-part-2-lines-points-formatting/)

그래프를 위한 모듈이다. MatLab을 python에 적용한 듯한 느낌이다.
OS X에서 다음과 같이 설치하였다. 설치에 별다른 어려움은 없었다.
``` shell
pip3 install matploblib
```

Reference의 코드대로 입력하였더니, 잘 그려졌다.
다음은 line을 긋는 예제이다.
``` python
import matplotlib.pyplot as plt 
plt.plot([1, 2, 3, 4])
plt.show()
```

다음 예제는 좌표에 점을 찍는 예제이다.
```python
import matplotlib.pyplot as plt
plt.plot([1,2,3,4], [1,4,9,16], 'ro')
plt.axis([0, 6, 0, 20])
plt.show()
```

matplotlib은 다음 2가지 방식으로 이용가능하다.
 - pylab : matlab과 호환을 위한 matlab 유사함수 사용.
 - matplotlib.pyplot : Object Orient 방식.

관례적으로 다음과 같이 import 한다.
```python
* # pylab
t # matplotlib.pyplot
```
##### MATLAB-like API ([matplotlib - 2D and 3D plotting in Python](http://nbviewer.ipython.org/github/jrjohansson/scientific-python-lectures/blob/master/Lecture-4-Matplotlib.ipynb))
``` python
from pylab import 
x = linspace(0, 5, 10)
y = x * x
figure()
plot(x, y, 'r')
xlabel('x')
ylabel('y')
title('title')
show()
```
##### The matplotlib object-orinted API ([matplotlib - 2D and 3D plotting in Python](http://nbviewer.ipython.org/github/jrjohansson/scientific-python-lectures/blob/master/Lecture-4-Matplotlib.ipynb))
``` python
import matplotlib.pyplot as plt
fig = plt.figure()
axes = fig.add_axes([0.1, 0.1, 0.8, 0.8])
axes.plot(x, y, 'r')

axes.set_xlabel('x')
axes.set_ylabel('y')
axes.set_title('title')
```

#### ipython으로 사용하기
``` sh
ipython notebook --inline=pylab
```
