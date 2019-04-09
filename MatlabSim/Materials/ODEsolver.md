# 含参数微分方程matlab求解

对于Lorenz微分方程组
$$\begin{cases}
\dot{x}_{1} = - \frac{8}{3}x_{1}+x_{2}x_{3} \\ 
\dot{x}_{2} = - 10x_{2}+10x_{3} \\ 
\dot{x}_{3} = - x_{1}x_{2}+28x_{2}-x_{3} \\ 
\end{cases} $$

利用matlab中ode45求解时，先建立脚本文件描述方程组
```matlab
function y = lorenzeq(t,x)

	y =[-8/3*x(1)+x(2)*x(3); 
	    -10*x(2)+10*x(3);
	    -x(1)*x(2)+28*x(2)-x(3)];
end
```
定义初值和积分区间后，再调用ode45求解
```matlab
[t,x]=ode45('lorenzeq',[0,t_final],x0);
```
即可获得变步长L-K-F算法的积分结果。
然而，对于大部分情况，方程组中的参数并不是一定的，需要当作外部变量传入，此时，Lorenz方程可以用变量表示为：
```matlab
function y = Plorenzeq(t,x,Rio,Beta,Sigma)

y =[-Rio*x(1)+x(2)*x(3); 
    -Beta*x(2)+Beta*x(3);
    -x(1)*x(2)+Sigma*x(2)-x(3)];
end
```
其中，Rio,Beta,Sigma就是等待外部传入的变量。在调用数值积分算法时，ode45调用方法为
```matlab
[t,x]=ode45(@Plorenzeq,[0,t_final],x0,[],a,b,c);
```
或者
```matlab
[t,x]=ode45(@(t,x)Plorenzeq(t,x,a,b,c),[0,t_final],x0);
```
其中，a，b，c分别与Rio,Beta,Sigma对应。这样，参数就能在调用积分算法时从外部传入。

- **值得注意的是，在含控制输入的系统中，如$$ \dot{x}=f\left ( x,t,u \right )$$,其中控制量$$u$$可以看做是微分方程的参数，当控制量为常数时，可以通过上述方法使用。当控制量为时变信号时，仿真过程中可以循环分段调用ode45。**




##### **测控系  Matlab建模与仿真 参考资料**


---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"> </script>
