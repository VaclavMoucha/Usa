Jednovýběrový test pro rozptyl
![[Pasted image 20260529120652.png]]
```
%pr 1

%H0: sigma^2 <=2.25 HA : sigma^2 >2.25

data = importdata("P0801.mat");

rozptyl = 2.25;

[h,p,ci,stats] = vartest(data,rozptyl,0.05,"right")

%Hypotézu H0 , že rozptyl je menší nebo roven 2.25 příjmáme, pvalue =

%0.3798
```
![[Pasted image 20260529120714.png]]
```
%pr2 H0: rozptyl <= 0.6 HA:rozptyl >0.6
x=[2.22, 3.54, 2.37, 1.66, 4.74, 4.82, 3.21, 5.44, 3.23, 4.79, 4.85, 4.05, 3.48, 3.89, 4.90, 5.37];
[h,p,ci,stats] = vartest(x,0.6,0.05,"right")
% Hypotézu H0: že rozptyl nemá překročit hodnotu 0.6 , zamitáme , pval =
% 0.0038
```
![[Pasted image 20260529120839.png]]
```
%pr3 H0: smerodatnaOdchylka = 3000 HA: smerodatnaOdchylka !=300

s=357;

sigma = 300;

n = 25;

T = (s^2/sigma^2)*(n-1)

test_dolni=chi2inv(0.025,n-1)

test_horni=chi2inv(0.975,n-1)

p_value=chi2cdf(T,n-1);

p_value=2*min(p_value,1-p_value)
%H0 prijmáme jelikož 0.1698 > 0.05
```
Jeednovýběrový test pro střední hodnotu 
![[Pasted image 20260529121749.png]]
```
%pr5 H0:spotřeba = 8.8 l/100km HA: spotřeba !=8.8 l/100km

% H0: rozptyl = 0.1 HA:rozptyl != 0.1

Spotreba=[8.8, 8.9, 9.0, 8.7, 9.3, 9.0, 8.7, 8.8, 9.4, 8.6, 8.9];

[h,p,ci,stats] = ttest(Spotreba,8.8,0.05,"both")

[h,p,ci,stats] = vartest(Spotreba,0.1,0.05,"both")

%Hypotezu H0 že na hladině 5% vyznamnosti činí 8.8 příjmáme, pval = 0.1455

%Hypotezu H0 že na hladině 5% vyznamnosti je rozptyl roven 0.1 příjmáme

%pval- 0.3973
```
párového testu testujeme jestli je **rozdíl středních hodnot** roven nějaké hodnotě
![[Pasted image 20260529123106.png]]
```
%pr 7

x=[35.0,36.0,36.3,36.8,37.2,37.6,38.3,39.1,39.3,39.6,39.8;

37.2,38.1,38.2,37.9,37.6,38.3,39.2,39.4,39.7,39.9,39.9];

a = x(1,:);

b = x (2,:);

[h,p,ci,stats]= ttest(a,b,0.05,"both")

c = a-b;

[h,p,ci,stats]= ttest(c,0,0.05,"both");

[h,p,ci,stats]= ttest(c,0,0.05,"left");
%a) Hypotézu H0 o shodě parametrů na hladině významnosti 5% zamítáme, pval=0.0024

% b) Hypotézu H0 na hladině významnosti 5 % zamítáme, pval=0.0012. Prokázali jsme na hladině významnosti 5 % vliv tepelné úpravy.

```
Znamínkový test slouží pro ověření medianu
![[Pasted image 20260529123831.png]]

```
%pr 8 H0: median = 25 HA : median !=5

x=[-6,-3,-1,0,2,3,5,6,7,8,9,11,12,14,15,18,22,28,32,37,41];

[p,h]= signtest(x,25,0.05)

% Hypotezu H0: na hladině 5% vyznamnosti že median je roven 25 zamítáme ,

% pval = 0.0072
```
![[Pasted image 20260529124120.png]]
```
%pr 9 H0 median =8.8 HA: median != 8.8

Spotreba=[8.8, 8.9, 9.0, 8.7, 9.3, 9.0, 8.7, 8.8, 9.4, 8.6, 8.9];

[p,h] = signtest(Spotreba,8.8,0.05)

%Na hladině výnamnosti 5% H0 že median je roven 8.8 příjmame, pval = 0.5078
```
Kvantilový test 
![[Pasted image 20260529130343.png]]
```
%pr11 H0: x₀.₁₀ = 1.5, HA: x₀.₁₀ ≠ 1.5

x=[2,3,4,5,6,7,7,8,8,9,11,12,13,15,16,18,19,22,25,28,31,34,37,39,42,45,48];

p0 = 0.10; % 10% kvantil

m0 = 1.5; % testovaná hodnota

n = length(x);

% počet hodnot menších než m0

Z_minus = sum(x < m0);

n_upravene = sum(x ~= m0); % vynecháme hodnoty rovné m0

% p-value oboustranný

pval = 2 * binocdf(min(Z_minus, n_upravene - Z_minus), n_upravene, p0)

%jelikož 0.1163 > 0.05 příjmáme
```
Jednovýběrový wilcoxonnův test
![[Pasted image 20260529131046.png]]
```
%pr 13 H0:median =220 HA: median !=220

data = importdata("P0812.mat");

[p,h,stats]=signrank(data,220,0.05)

%Na hladině vyznamnosti 5% hypotézu H0 že se median rovna 220 zamítáme.

%pval= 0.0171
```
Test relativní četnosti
![[Pasted image 20260529131659.png]]
![[Pasted image 20260529132011.png|143]]
```
%pr15 H0: π = 0.15

%HA: π ≠ 0.15

p=82/1000;

pi =0.15;

n = 1000;

T = (p-pi)/sqrt((pi*(1-pi))/n);

pval = 2 * min(normcdf(T,0,1), 1-normcdf(T,0,1))

%pvalue <0.05 zamítáme H0
```


![[Pasted image 20260529132813.png]]
```
%15a H0: stredniHodnota = 3000 HA: stredniHodnota !=3000

Tporuch=[80,160,240,320,400,560,720,800,900,960]

t = [Tporuch,1000];

cens = [0,0,0,0,0,0,0,0,0,0,1];

freq = [1,1,1,1,1,1,1,1,1,1,40];

[par io] = expfit(t,0.05,cens,freq)

% zamítáme jelikož je to v rozmezí
```
Dvojvyberovy test  rozptylů
![[Pasted image 20260529133246.png]]


```
%pr 16 H0: sigma = sigma2 HA: sigma!=sigma2

Rano=[98.5, 98.6, 98.7, 98.7, 98.7, 98.8, 98.9, 99.2, 99.3, 99.3]

Odpoledne=[98.1,98.2, 98.3, 98.4, 98.6, 98.7, 98.8, 98.9, 99.0, 99.0]

[h,p,ci,stats]= vartest2(Rano,Odpoledne, 0.05,"both")

%hypotezu h0 o vyznamnosti 5% prijmame s pval= 0.7187
```



![[Pasted image 20260529133313.png]]
```
%pr19

x=[35.0,36.0,36.3,36.8,37.2,37.6,38.3,39.1,39.3,39.6,39.8;

37.2,38.1,38.2,37.9,37.6,38.3,39.2,39.4,39.7,39.9,39.9];

a = x(1,:);

b = x(2,:);

[h,p,ci,stats]=ttest2(a,b,0.05,"both")

%na vyznamnosti 5% prijmame H0 , pval =0.112
```
![[Pasted image 20260529133714.png]]
```
a = [62,54,55,60,53,58];

b = [52,56,50,49,51];

[h,p,ci,stats]=ttest2(a,b,0.05,"both")
```

![[Pasted image 20260529134037.png]]
```
%pr22 H0. str = str2, HA: str !=str2

x=[24,26,27,28,28,28,29,31,32,33];

y=[-21,-5,3,8,14,17,19,21,29,38,46,52,68];

[h,p] = vartest2(x,y,0.05,"both")

%rozptyly nejsou stejné data jsou z normalního rozdělení

[h,p,ci,stats] = ttest2(x,y,0.05,"both","unequal")

%pro stredni hodnoty prijmame s pval 0.3680
```
Man  whit
![[Pasted image 20260529134529.png]]
```
%pr23 H0:median1 = median2 HA: median1 !=median2

x=[12,14,16,18,19,19,21,23,25,27,31,35,39,42];

y=[15,18,21,24,27,29,32,35];

[p,h,stats]= ranksum(x,y,0.05)

%příjmame H0 pval = 0.707
```
testovaní relativních četností 
![[Pasted image 20260529134956.png]]
```
%pr 24

n1 = 1240;x1 = 325;

n2 = 741; x2 = 287;

p1 = x1/n1;

p2 = x2/n2;

T = (p1-p2) / sqrt((p1*(1-p1)/n1) + (p2*(1-p2)/n2))

pval = 2*min(normcdf(T,0,1), 1-normcdf(T,0,1))

%na hladině výnamnosti 5% se H0 zamítá;
```
vicevyberove testy ![[Pasted image 20260529135452.png]]
```
%pr 25 H0:r1 = r2 =r3 HA: alespon jedna dvojice se liší

x1=[18,19,19,19,20,21,21,22,22,23,23,24,24,24,25,25,25,26,26,26,27,28];

x2=[17,18,18,19,19,20,21,21,22,22,22,23,23,23,23,24,24,25,25,26,26,27,28,29] ;

x3=[16,17,18,18,18,19,20,20,20,20,21,21,21,22,23,23,23,24,25,26,27,27,28,28,29,31];

x4=[14,15,16,16,17,18,19,20,22,22,22,23,24,25,25,27,27,27,28,28,28,31,31,33,34];

data = [x1,x2,x3,x4]';

skupina1(1:length(x1)) = 1;

skupina2(1:length(x2)) = 2;

skupina3(1:length(x3)) = 3;

skupina4(1:length(x4)) = 4;

skupiny = [skupina1,skupina2,skupina3,skupina4];

[p,stats]= vartestn(data,skupiny,"Display","on","TestType","Bartlett")

[p,stats]= vartestn(data,skupiny,"Display","on","TestType","LeveneQuadratic")
```
![[Pasted image 20260529140042.png]]
rozptyly jsou shodné pval = 0.0041, b) pval = 0.00022
![[Pasted image 20260529140118.png]]
```
%pr26

data = importdata("P0826.mat");

groups = [ones(100,1);2*ones(100,1);3*ones(100,1);4*ones(100,1);5*ones(100,1)];

[p,stats]= vartestn(data,groups,"Display","on","TestType","Bartlett")

[p,anovatab,stats]= anova1(data,groups,"on")
```
Kruskalll
![[Pasted image 20260529142254.png]]
```
[p,anovatab,stats]=kruskalwallis(data2,skupiny,"on")
```
Mnohonásobné porovnávání
![[Pasted image 20260529142344.png]]
