**Jsou parametry (a, b, c...) jen násobeny nebo přičítány?** → lineární → `fitlm`

**Je parametr v exponentu, jmenovateli, mocnině...?** → nelineární → `fitnlm`


![[Pasted image 20260530121650.png]]
```
%pr 1

x=[3,5,8,11,12,14,15];

y=[6,11,15,22,25,27,30];

vysl = fitlm(x,y,"linear")

%tedy vysledek je y= 0.3935 + 1.9595x, b může být nula jelikož výstup u

%intercept pValue = 0.65546 > 0.05
```
![[Pasted image 20260530122029.png]]
```
%pr3

x=[2,5,8,11,5,10,6];

y=[6,11,15,22,25,27,30];

vysl = fitlm(x,y,"linear")

%R - squared říká že model vysvětluje jen 29% dat hodně málo  jinak není vhodný protože pvalue > 0.05 kdyby byla menší tak je vhodný

```
![[Pasted image 20260530122719.png]]
```
%pr3

data = readtable("P1103.xlsx");

x = data.x;

y = data.y;

vysl = fitlm(x,y,"linear")

% y = 0.59591+3.0005x;
```
![[Pasted image 20260530122749.png]]
```
%pr5

data = readtable("P1105.xlsx");

x =data.x;

y = data.y;

vysl = fitlm(x,y,"quadratic")
```
![[Pasted image 20260530122957.png]]
U x1^2 je pval 0.847 > 0.05 takže není potřebný může byt 0
![[Pasted image 20260530123301.png]]
```
x=[1,2,3,4,5,6,6.5];

y=[3,5.1,6.9,8.8,10.9,13.3,14.1];

LM1=fitlm(x,y,'quadratic')

LM2=fitlm(x,y)

%z výsledků získaného parametru 0.0322 a směrodatné odchylky 0.0194

%se vypočte intervalový odhad

amin=0.0322-0.0194.*tinv(0.975,5)

amax=0.0322+0.0194.*tinv(0.975,5)
```
![[Pasted image 20260530123330.png]]
```
x=[1,2,3,4,5,6,7,8,9,10]';

y=[1,2,3,1,2,3,1,2,3,1]';

z=[3,9,17,10,16,26,14,25,38,23]';

LM1=fitlm([x,y],z,'linear')

LM2=fitlm([x,y],z,'interactions')
```


![[Pasted image 20260530123417.png]]
```
x=[1,2,3,4,5,6,7,8,9,10]';

y=[1,2,3,1,2,3,1,2,3,1]';

z=[3,9,17,10,16,26,14,25,38,23]';

LM1=fitlm([x,y],z,'quadratic')

LM2=fitlm([x,y],z,'purequadratic')

%pouze lineární model

LM3=fitlm([x,y],z)

%pvalue u všech parametrů tstat jsou menší než 0.05, F test má nižší hodnotu než u LM2,

%koeficient determinace se výrazně nesnížil.
```
![[Pasted image 20260530123454.png]]

```
x=[1,2,3,4,5,6,7,8,9,10]';

y=[2,5,8,10,12,15,18,19,21,24]';

LM1=fitlm(x,y)

int_b_min=2.3758-tinv(0.975,9)*0.064568

int_b_max=2.3758+tinv(0.975,9)*0.064568

%pval = 2*... oboustranný interval

%pval = 2* tcdf ... statistika jde na studentovo rozdělení

%pval = 2* tcdf((x-mu)/sigma,pocet stupnu volnosti)

pval=2*tcdf((2-2.3758)/0.064568,9)
%zamítáme jelikož je to menší než 0.05
```
![[Pasted image 20260530125303.png]]
```
%pr12

vstup=importdata('P1112.xlsx');

x=vstup.data.List1(:,1);

y=vstup.data.List1(:,2);

plot(x,y,'x')

%příklad ad a

LM=fitlm(x,y,'Constant')

%příklad ad b

modelfun=@(b,x)(b(1)./x+b(2));

beta0=[1,3]

NLM=fitnlm(x,y,modelfun,beta0)

```
![[Pasted image 20260530130357.png]]
a)
```
%pr13

data = readtable("P1113.xlsx")

x = data.x;

y = data.y;

modelfun=@(b,x)(b(3)*sin(b(1).*x+b(2)));

beta0=[1/3,1,5];

vysl = fitnlm(x,y,modelfun,beta0)
```
![[Pasted image 20260530130414.png]]
b)
```
data = readtable("P1113.xlsx")

x = data.x;

y = data.y;

modelfun=@(b,x)(b(3)*sin(b(1).*x+b(2)));
beta0=[1,0,1];

vysl = fitnlm(x,y,modelfun,beta0)
```
![[Pasted image 20260530130554.png]]
![[Pasted image 20260530130642.png]]

```
%pr15

data = readtable("P1115.xlsx");

x = data.x;

y = data.y;

%maximum x^7

modelfun=@(b,x)(b(1)+b(2).*x+b(3).*x.^2+b(4).*x.^3+b(5).*x.^4+b(6).*x.^5+b(7).*x.^6+b(8).*x.^7);

beta0=[0,0,0,0,0,0,0,0]

NLM=fitnlm(x,y,modelfun,beta0)

%maximum x^6

modelfun=@(b,x)(b(1)+b(2).*x+b(3).*x.^2+b(4).*x.^3+b(5).*x.^4+b(6).*x.^5+b(7).*x.^6);

beta0=[0,0,0,0,0,0,0]

NLM=fitnlm(x,y,modelfun,beta0)

%maximum x^5

modelfun=@(b,x)(b(1)+b(2).*x+b(3).*x.^2+b(4).*x.^3+b(5).*x.^4+b(6).*x.^5);

beta0=[0,0,0,0,0,0]

NLM=fitnlm(x,y,modelfun,beta0)

%maximum x^4

modelfun=@(b,x)(b(1)+b(2).*x+b(3).*x.^2+b(4).*x.^3+b(5).*x.^4);

beta0=[0,0,0,0,0]

NLM=fitnlm(x,y,modelfun,beta0)

%maximum x^3

modelfun=@(b,x)(b(1)+b(2).*x+b(3).*x.^2+b(4).*x.^3);

beta0=[0,0,0,0]

NLM=fitnlm(x,y,modelfun,beta0)
```
![[Pasted image 20260530131015.png]]
```
%pr 16

for i=1:100

x(i)=i;

end

for i=1:50

y(2*i-1)=(i-1)-(i-1).*(i-1);

y(2*i)=(i-1)+(i-1).*(i-1);

end

plot(x,y,'x')

LM=fitlm(x,y,'quadratic')

modelfun=@(b,x)(b(1)+b(2).*x+b(3).*x.^2);

beta0=[0,0,1]

NLM=fitnlm(x,y,modelfun,beta0)
```

![[Pasted image 20260530131102.png]]

```
vstup=importdata('P1117.xlsx');

x=vstup.data.List1(:,1);

y=vstup.data.List1(:,2);

z=vstup.data.List1(:,3);

X=[x,y];

modelfun=@(b,X)(b(1)./x+b(2)./y+b(3)./(x+y));

beta0=[2,4,1]

NLM=fitnlm(X,z,modelfun,beta0)

modelfun=@(b,X)(b(1)./y+b(2)./(x+y));

beta0=[4,1]

NLM=fitnlm(X,z,modelfun,beta0)
```

![[Pasted image 20260530131137.png]]
Pr21
```
x=[1,2,3,4,5,6,7,8,9,10];

y=[0,5,9,18,28,39,69,111,177,277];

modelfun=@(b,x)(b(1).*x.^2+b(2).*x+b(3));

beta0=[1,1,1]

NLM=fitnlm(x,y,modelfun,beta0)

modelfun1=@(b,x)(b(1).*x.^2+b(2).*x);

beta0=[1,1]

NLM1=fitnlm(x,y,modelfun1,beta0)
```
Pr22
```vstup=importdata('P1122.csv');

x=vstup(:,1);

y=vstup(:,2);

modelfun=@(b,x)(b(1)./(x.^b(2)));

beta0=[0.08,1]

NLM=fitnlm(x,y,modelfun,beta0)

%například počáteční řešení [10,-1], nemá vliv na výsledky

modelfun=@(b,x)(b(1)./(x.^b(2)));

beta0=[10,-1]

NLM=fitnlm(x,y,modelfun,beta0)

%například počáteční řešení [0,0], nemá vliv na výsledky

modelfun=@(b,x)(b(1)./(x.^b(2)));

beta0=[0,0]

NLM=fitnlm(x,y,modelfun,beta0)

```