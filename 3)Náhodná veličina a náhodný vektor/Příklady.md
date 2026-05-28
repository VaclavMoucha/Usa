![[Pasted image 20260528094044.png]]

```
syms x;

F = (x^3)/8;

limit(F,0);

limit(F,2);

%dat na hustotu pravděpodobnosti

f = diff(F);

%střední hodnota a rozptyl

strhod=int(x.*f,0,2)

rozptyl=int((x-strhod).^2.*f,0,2)

%a)

x=0.0;

F00=(x^3)/8;

x=1;

F10=(x^3)/8;

Pa=F10-F00

%b)

x=0.5;

F05=(x^3)/8;

x=1.5;

F15=(x^3)/8;

Pb=F15-F05

%c

x=2;

F20=(x^3)/8;

Pc=(F10-F00)+(F20-F15)
```
![[Pasted image 20260528095625.png]]
```
x = importdata("P0328.mat");

mean(x)

var(x)

median(x)

q_5 = quantile(x,0.05)

q_95 = quantile(x,0.95)

q_25 = quantile(x,0.25)

q_75 = quantile(x,0.75)

histogram(x)
```