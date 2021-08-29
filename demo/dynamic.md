# 绘制动态图
## 例子1.


```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
# jupyter运行，需要输入下面这个命令
%matplotlib qt5

N = 20
plt.close() # 关闭打开的图形窗口
def anni():
    fig = plt.figure()
    plt.ion() # 打开交互式绘图interactive
    for i in range(N):
        plt.cla()           # 清除原有图像
        plt.xlim(-0.2,20.4) # 设置x轴坐标范围
        plt.ylim(-1.2,1.2)  # 设置y轴坐标范围
        # 每当i增加的时候，增加自变量x的区间长度，可以理解为不断叠加绘图，所以每次循环之前都使用plt.cla()命令清除原有图像
        x = np.linspace(0,i+1,1000) 
        y = np.sin(x)
        plt.plot(x,y)
        plt.pause(0.1)
    # plt.ioff() #关闭交互式绘图
    
    plt.show()

anni()

```

## 例子2.


```python
fig, ax = plt.subplots()
xdata, ydata = [], []
ln, = plt.plot([], [], 'ro',animated=True)

def init():
    ax.set_xlim(-np.pi,np.pi)
    ax.set_ylim(-1, 1)
    return ln,

def update(frame):
    xdata.append(frame)
    ydata.append(np.sin(frame))
    ln.set_data(xdata, ydata)
    return ln,

anim = animation.FuncAnimation(fig, update, frames=np.linspace(-np.pi,np.pi, 90),interval=10,
                    init_func=init,blit=True)
anim.save('test2.gif',writer='pillow')
plt.show()


```

## 例子3


```python
import numpy as np
import matplotlib.pyplot as pl
import matplotlib.animation as animation

x = np.linspace(0, 10, 100)
y = np.sin(x)

fig, ax = plt.subplots()
line, = ax.plot(x, y, color='k')

def update(num, x, y, line):
    line.set_data(x[:num], y[:num])
    line.axes.axis([0, 10, -1, 1])
    return line,

ani = animation.FuncAnimation(fig, update, len(x), fargs=[x, y, line],
                              interval=25, blit=False)
ani.save('test3.gif',writer='pillow')
plt.show()

```
