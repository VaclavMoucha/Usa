![[Pasted image 20260529164426.png]]
```
%pr 1 H0: pi1=pi2=pi3=pi4=pi5=pi6 HA: neplatí H0

x = [1,2,3,4,5,6];

freq = [11,8,14,5,7,5];

hranice = [0.5,1.5,2.5,3.5,4.5,5.5,6.5];

[h,p,stats]=chi2gof(x,'expected',[50/6,50/6,50/6,50/6,50/6,50/6],'edges',hranice,'frequency',freq,"Alpha",0.05)

%Hypotezu na hladině vyznamnosti 5= příjmame pvalue = 0.1797

```
![[Pasted image 20260529164550.png]]
```
%PR2 H0:Dpi1=pi2=pi3=pi4=pi5=pi6 HA: neplatí H0

x = [1,2,3,4,5,];

freq = [15,10,10,8,7];

hranice = [0.5,1.5,2.5,3.5,4.5,5.5];

expected = [18,14,10,4.5,3.5];

[h,p,stats]=chi2gof(x,"Expected",expected,"Edges",hranice,"Alpha",0.05,"Frequency",freq);

%hypotezu na hladině významnnost 5% příjmame , pvalue = 0.0511
```
![[Pasted image 20260529164907.png]]
```
%Pr3

x=[0*ones(1,385),1*ones(1,431),2*ones(1,148),3*ones(1,29),4*ones(1,5),5*ones(1,1)];

%tahle kokotina je hygepdf(kolik úspěchů jsem získal, velikost celé

%populace,počet úspěšných prvků v populaci, velikost výběru)

%neboli jeste pro mě hygepdf(trefená čísla,49,6výherních, 6 tipovaných)

H5=hygepdf(5,49,6,6)*1000;

H4=hygepdf(4,49,6,6)*1000;

H3=hygepdf(3,49,6,6)*1000;

H2=hygepdf(2,49,6,6)*1000;

H1=hygepdf(1,49,6,6)*1000;

H0=hygepdf(0,49,6,6)*1000;

[h,p,stats]=chi2gof(x,'expected',[H0,H1,H2,H3,H4,H5])

%zjistím očekávané četnosti skupin.

%tady zase binopdf(počet uspěchů , počet pokusů , pravděpodobnost uspěchu)

B5=binopdf(5,6,6/49)*1000;

B4=binopdf(4,6,6/49)*1000;

B3=binopdf(3,6,6/49)*1000;

B2=binopdf(2,6,6/49)*1000;

B1=binopdf(1,6,6/49)*1000;

B0=binopdf(0,6,6/49)*1000;

[h,p,stats]=chi2gof(x,'expected',[B0,B1,B2,B3,B4,B5])
```
![[Pasted image 20260529170131.png]]
```
%pr4

data0(1:3)=0;

data1(1:10)=1;

data2(1:15)=2;

data3(1:12)=3;

data4(1:17)=4;

data5(1:10)=5;

data6(1:10)=6;

data7(1:9)=7;

data8(1:5)=8;

data9(1:5)=9;

data10(1:4)=10;

data11(1:5)=11;

x=[data0,data1,data2,data3,data4,data5,data6,data7,data8,data9,data10,data11];

[h,p,stats]=chi2gof(x,'cdf',{@poisscdf,mean(x)})

%hypotezu zamítáme
```
![[Pasted image 20260529171510.png]]
```
%prr 5

a = poissrnd(10,1,100);

[h,p,stats]=chi2gof(a,'cdf',{@poisscdf,mean(a)})

a =[a,14,15,17,18,19,21,22,24,26,27,27,28,32,34,36 ];

[h,p,stats]=chi2gof(a,'cdf',{@poisscdf,mean(a)})

%první platí H0 u druhého už ne
```
![[Pasted image 20260529172102.png]]

```
%pr6

%šance je 1/3 na černou losuje se 5

pbila=20/30;

opakovani=5;

x=[0,1,0,1,0,2,0,1,1,0,0,1,0,1,0,2,0,1,1,0,0,0,0,1,2,1,1,2,1,0,1,2,1,2,3];

E=length(x)*[binopdf(0,5,2/3),binopdf(1,5,2/3),binopdf(2,5,2/3),binopdf(3,5,2/3),binopdf(4,5,2/3),binopdf(5,5,2/3)];

[h1,p1,stats1]=chi2gof(x,'expected',E,'edges',[-0.5,0.5,1.5,2.5,3.5,4.5,5.5])

%zamítáme H0
```
![[Pasted image 20260529172656.png]]
```
%pr7

data = readtable("P0907.xlsx");

x = data.Var1(:,1)';

[h,p,stats]=chi2gof(x,'CDF',{@expcdf,mean(x)})

[h,p,stats]=chi2gof(x,'CDF',{@wblcdf,mean(x)})

%data nejsou z exponencialního ani z weibullova
```
![[Pasted image 20260529173610.png]]

```
%pr9

x = importdata("P0909.mat")';

mean(x)

std(x)

[h,p,stats]= chi2gof(x,"CDF",{@normcdf,mean(x),std(x)})

[h,p,stats]= chi2gof(x,"CDF",{@normcdf,15,5})

%data jsou z normalního rozdělení s mu = 13.15 a sigma = 4.58 pval = 0.6397

%data nejsou z normalního rozdělení s mu 15, a sigma 5 , pval =2.7099e-05
```
![[Pasted image 20260529174151.png]]
```
%pr10
%nedává smysl tenhle příklad pouze ta druhá část
x = importdata("P0910.mat")';

[h,p,stats]= chi2gof(x,"CDF",{@normcdf,20,10})

%zamítáme H0,pval = 5.9012e-07

x = sort(x);

boxplot(x)

x(1:3)=NaN;

x(106:110)=NaN;

[h,p,stats]= chi2gof(x,"CDF",{@normcdf,20,10}) 
```
![[Pasted image 20260529175019.png]]
```
%Pr 13

a = normrnd(20,10,1,50);

b = normrnd(30,10,1,50);

c = [a,b];

mu = mean(c);

sigma = std(c);

[h,p,stats] = chi2gof(c,"CDF",{@normcdf,mu,sigma})

%hypotezu příjmáme
```
![[Pasted image 20260529175501.png]]

```
%pr 14

data = importdata("P0914.mat")';

a = wblfit(data)

[h,p,stats] = chi2gof(data,"CDF",{@wblcdf,a(1),a(2)})

%Hypotézu schvalujeme
```
![[Pasted image 20260529180231.png]]
```
%Pr15

vyska=[162,167,170,171,172,175,178,179,180,181,182,184,185,187,191,195];

a = zeros(length(vyska),2);

a(:,1)=vyska';

[mu,sigma] = normfit(vyska);

a(:,2)=normcdf(a(:,1),mu,sigma)

[h,p,kstat,cv] = kstest(vyska,"CDF",a ,"Alpha",0.05)

[h,p,kstat,cv] = lillietest(vyska,0.05,"norm")

%obě dvě hypotézy příjmáme
```
![[Pasted image 20260529181216.png]]
```
%Pr 16

t=[37,48,54,75,81,104,123,141,156,187,195,213,241,254,271,289,312,345,395,412,461,512,651,731];

wblplot(t);

a(1:length(t),1)=t';

a(:,2)=expcdf(t,mean(t));

[h,p,kstat,cv] = kstest(t,a);

par = wblfit(t);

a(:,2)=expcdf(t,par(1),par(2));

[h,p,kstat,cv] = kstest(t,a)

%obě dvě hypotézy schvalujeme
```
![[Pasted image 20260529182622.png]]
```
%pr16a

t=[37,48,54,75,81,104,123,141,156,187,195,213,241,254,271,289,312,345,395,412,461,512,651,731];

a(1:length(t),1)=t';

fprintf("100---------------------------------")

a(:,2)=expcdf(t,100);

[h,p,kstat,cv] = kstest(t,a)

fprintf("200---------------------------------")

a(:,2)=expcdf(t,200);

[h,p,kstat,cv] = kstest(t,a)

fprintf("333---------------------------------")

a(:,2)=expcdf(t,333);

[h,p,kstat,cv] = kstest(t,a)

fprintf("500---------------------------------")

a(:,2)=expcdf(t,500);

[h,p,kstat,cv] = kstest(t,a)

fprintf("1000---------------------------------")

a(:,2)=expcdf(t,1000);

[h,p,kstat,cv] = kstest(t,a)
```
![[Pasted image 20260529184034.png]]

```
x3=unifrnd(0,1,1,3);

x5=unifrnd(0,1,1,5);

x10=unifrnd(0,1,1,10);

x20=unifrnd(0,1,1,20);

x50=unifrnd(0,1,1,50);

x100=unifrnd(0,1,1,100);

%testování, zda data jsou z rovnoměrného rozdělení <0,1>

%prvni sloupec hodnoty, druhy sloupec hodnota distribucni funkce.

%(zde oba sloupce budou shodné, protože je to z rovnoměrného rozdělení 0,1)

CDF3(:,1)=x3';

CDF3(:,2)=unifcdf(CDF3(:,1),0,1);

CDF5(:,1)=x5';

CDF5(:,2)=unifcdf(CDF5(:,1),0,1);

CDF10(:,1)=x10';

CDF10(:,2)=unifcdf(CDF10(:,1),0,1);

CDF20(:,1)=x20';

CDF20(:,2)=unifcdf(CDF20(:,1),0,1);

CDF50(:,1)=x50';

CDF50(:,2)=unifcdf(CDF50(:,1),0,1);

CDF100(:,1)=x100';

CDF100(:,2)=unifcdf(CDF100(:,1),0,1);

[h3,p3]=kstest(x3,CDF3)

[h5,p5]=kstest(x5,CDF5)

[h10,p10]=kstest(x10,CDF10)

[h20,p20]=kstest(x20,CDF20)

[h50,p50]=kstest(x50,CDF50)

[h100,p100]=kstest(x100,CDF100)

%b]

CDF3b(:,1)=x3';

CDF3b(:,2)=unifcdf(CDF3(:,1),0.2,1.2);

CDF5b(:,1)=x5';

CDF5b(:,2)=unifcdf(CDF5(:,1),0.2,1.2);

CDF10b(:,1)=x10';

CDF10b(:,2)=unifcdf(CDF10(:,1),0.2,1.2);

CDF20b(:,1)=x20';

CDF20b(:,2)=unifcdf(CDF20(:,1),0.2,1.2);

CDF50b(:,1)=x50';

CDF50b(:,2)=unifcdf(CDF50(:,1),0.2,1.2);

CDF100b(:,1)=x100';

CDF100b(:,2)=unifcdf(CDF100(:,1),0.2,1.2);

[h3b,p3b,kstest3b]=kstest(x3,CDF3b)

[h5b,p5b,kstest5b]=kstest(x5,CDF5b)

[h10b,p10b,kstest10b]=kstest(x10,CDF10b)

[h20b,p20b,kstest20b]=kstest(x20,CDF20b)

[h50b,p50b,kstest50b]=kstest(x50,CDF50b)

[h100b,p100b,kstest100b]=kstest(x100,CDF100b)
```
![[Pasted image 20260529184104.png]]

```
%pr18

x = importdata("P0918.mat");

normplot(x)

a(1:length(x),1)=x';

a(:,2)= normcdf(x,10,3);

[h,p,kstat,cv] = kstest(x,a)

[h,p,kstat,cv] = lillietest(x,0.05,"norm")

%zamítáme obě dvě
```
![[Pasted image 20260529184836.png]]
```
x=[24,35,61,87,120,151,187,214,341,541,653,1213,2421]

%zpusob 1

%po zlogaritmování jsou data z normálního rozdělení

%lze použít Lillieforsův test

y=log10(x);

[h,p,kstat,critval]=lillietest(y)

%zpusob 2

%Kolmogorov test lognormal

par=lognfit(x)

CDF(:,1)=x';

CDF(:,2)=logncdf(CDF(:,1),par(1),par(2))

[h,p,ksstat,cv]=kstest(x,CDF)

%zpusob 3

%Kolmogorov test normal distribution

y=log10(x)

CDF(:,1)=y';

CDF(:,2)=normcdf(CDF(:,1),mean(y),std(y))

[h,p,ksstat,cv]=kstest(y,CDF)
```
Dvojvyběrový testy
![[Pasted image 20260529185453.png]]
```
x=[3,5,9,12,15,17,21,24] ;

y=[5,8,12,12,15,17,19,24,25,28];

[h,p,kstest] = kstest2(x,y)

%příjmáme H0 pval = 0.9854
```

![[Pasted image 20260529185712.png]]

```
%pr23


x=[31,36,42,48,52,57] ;

y=[15,18,22,27,29,34,35,38,43,49,52];

[h,p,kstest] = kstest2(x,y)

%příjmame H0 pvalue 0.2615
```
![[Pasted image 20260529185923.png]]

```
%pr24

a = normrnd(0.5,0.25,1,20);

b = unifrnd(0,1,1,20);

c = normrnd(0.5,0.25,1,200);

d = unifrnd(0,1,1,200);

[h,p,kstest] = kstest2(a,b)

[h,p,kstest] = kstest2(c,d)

%první příjmame druhou zamítáme
```
![[Pasted image 20260529190304.png]]

```
%pr25
data = readtable("P0925.xlsx");

x = data.Var1(:,1)';

y = data.Var2(:,1)';

[h,p,kstest] = kstest2(x,y)

%zamítame
```
![[Pasted image 20260529190604.png]]

```
Praha=[16,18,18,18,21,23,25,28,31,34,37,41,45,48,48,61]

Liberec=[13,14,14,15,15,16,17,18,23,28,34,36]

%H0 Praha<= Liberec H1 Praha>Liberec

[p,h]=ranksum(Praha,Liberec,'tail','right')

%H0 distribuce platu je v obou městech shodná, H1 v Praze je nižší

%distribuce platu než v Liberci

hold on

ecdf(Praha)

ecdf(Liberec)

hold off

%H0: F(Praha)>= F(Liberec) %H1: F(Praha)<F(Liberec)

[h,p,kstest]=kstest2(Praha,Liberec,0.05,'smaller')
```
![[Pasted image 20260529190642.png]]

```
x=[16,18,18,18,19,19,19,20,20,21,21,21,23,26] ;

y=[13,14,14,15,15,16,16,16,17,17,18,19,20,21,23,23,23,24,25,28];

[h,p,kstest]=kstest2(x,y)

[h,p,kstat,critval]=lillietest(x)

[h,p,kstat,critval]=lillietest(y)
```
