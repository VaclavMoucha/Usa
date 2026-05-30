|Typ dat|Předpoklad|Metoda|MATLAB funkce|
|---|---|---|---|
|Kategoriální (Ano/Ne, vzdělání...)|žádný|**χ² test** (kontingenční tabulka)|`crosstab(x,y)`|
|Spojitá (výška, hmotnost...)|normální rozdělení|**Pearsonův** koeficient|`corrcoef(x,y)`|
|Spojitá (výška, hmotnost...)|nenormální rozdělení|**Spearmanův** koeficient|`corr(x,y,'type','Spearman')`|
![[Pasted image 20260530105847.png]]
```
%pr 1 H0:hodnoty v kontigenční tabulce jsou statisticky nezávisle HA: -||- závislé

%zenich

x1(1:39)=1;

x2(1:34)=2;

x3(1:27)=3;

x = [x1,x2,x3];

%nevěsty

y11(1:24)=1;

y12(1:12)=2;

y13(1:3)=3;

y21(1:7)=1;

y22(1:24)=2;

y23(1:3)=3;

y31(1:3)=1;

y32(1:9)=2;

y33(1:15)=3;

y=[y11,y12,y13,y21,y22,y23,y31,y32,y33];

[tbl,chi2,p]=crosstab(x,y)

%H1,pval -p32E-9 Na hladině významnosti 5% zamítáme hypotézu že vzdělaní nevěsty a ženicha

%jsou vzájemně nezávislé veličiny;

%zamítame jelikož je to menší než 0.05
```
![[Pasted image 20260530111249.png]]
```
%pr2



%H0 obliba sportu při vlastním sportování a u televize je nezávislá

%veličina

%H1 obliba sportu při vlastním sportování a u televize je závislá veličina

x1(1:145)=1;

x2(1:32)=2;

x3(1:30)=3;

x4(1:27)=4;

y11(1:133)=1;

y12(1:6)=2;

y13(1:2)=3;

y14(1:4)=4;

y21(1:15)=1;

y22(1:10)=2;

y23(1:4)=3;

y24(1:3)=4;

y31(1:4)=1;

y32(1:1)=2;

y33(1:25)=3;

y41(1:9)=1;

y43(1:1)=3;

y44(1:17)=4;

x=[x1,x2,x3,x4];

y=[y11,y12,y13,y14,y21,y22,y23,y24,y31,y32,y33,y41,y43,y44];

[tbl,chi2,p]=crosstab(x,y)

%H1, pval=5E-53, Na hladině významnosti 5 % zamítáme hypotézu, že obliba dělaného sportu je nezávislá na oblibě sportu sledovaného v televizi.]
```
![[Pasted image 20260530111632.png]]
Zde se ptají jestli má vliv takže musíme počítat  o kolik je větší šance
```
a=58;

b=112;

c=24;

d=19;

%výpočet testovací statistiky

T=a*d/(b*c)

%výpočet intervalu

Tmin=T*exp(-(sqrt(1/a+1/b+1/c+1/d))*norminv(0.975,0,1))

Tmax=T*exp((sqrt(1/a+1/b+1/c+1/d))*norminv(0.975,0,1))
%Ale dá se i pomocí kontigenčních tabulek
x1(1:170)=1;

x2(1:43)=2;

x = [x1,x2];

y11(1:58)=1;

y12(1:112)=2;

y21(1:24)=1;

y22(1:19)=2;

length(x)

y=[y11,y12,y21,y22];

length(y)

[tbl,chi2,p] = crosstab(x,y)

%při obou dvou zamítáme H0, pval= 0.009 jinak u prvího zbůsobu zjistíme

%podle toho jestli je T<1 nebo T>1 zde je T<1 takže zamítáme
```
![[Pasted image 20260530112057.png]]
```
%pr4

a=30;

b=36;

c=21;

d=43;

%výpočet testovací statistiky

T=a*d/(b*c)

%výpočet intervalu

Tmin=T*exp(-(sqrt(1/a+1/b+1/c+1/d))*norminv(0.975,0,1))

Tmax=T*exp((sqrt(1/a+1/b+1/c+1/d))*norminv(0.975,0,1))

%Zde je T>1 takže příjmáme
```
![[Pasted image 20260530112845.png]]
```
x=[7, 8, 10, 4, 14, 9, 6, 2, 13, 5]

y=[9, 7, 12, 6, 15, 6, 8, 4, 11, 8]

plot(x,y,'x')

corrcoef(x,y)
%kolerace je 0.8452
```
![[Pasted image 20260530113019.png]]

```
%pr 7

x=[7, 8, 10, 4, 14, 9, 6, 2, 13, 5];

y=[9, 7, 12, 6, 15, 6, 8, 4, 11, 8];

[h,p]=lillietest(x,'distribution','norm');

[h,p]=lillietest(y,'distribution','norm');

%data jsou z normálního rozdělení

[r,p,RLO,RUP]=corrcoef(x,y);

%Zamítame hypotezu H0 o nezávislosti dat jelikož pval < 0.05, r = 0.8452,

%intervalový odhad korelace je mezi <0.4608,0.9626>
```
![[Pasted image 20260530114720.png]]
```
%pr8

data = importdata("P1008.mat");

x = data.x;

y = data.y;

[h,p]=lillietest(x,'distribution','norm')

[h,p]=lillietest(y,'distribution','norm')

%data jsou z normálního rozdělení

[r,p,RLO,RUP]=corrcoef(x,y)

%data jsou z normálního rozdělení, r=0.9414, pval=1E-95, 95% intervalový odhad korelace je <0.9233,0.9554>]
```
![[Pasted image 20260530114730.png]]
```
%pr 9

data=load('P1009.mat')

A=data.A;

B=data.B;

plot(A,B,'x')

%test normality dat

[h,p]=lillietest(A,'distribution','norm')

[h,p]=lillietest(B,'distribution','norm')

%Pozor u funkce corr musí být sloupcové vektory dat

%korelační koeficient

[r,p]=corr(A',B','type','Spearman')

%data komponenty A nejsou normálně rozdělené pval<0.001, data komponenty B jsou normálně rozdělené, použiji Spearmanův korelační koeficient; r=0.0336, H0, pval=0.2887
```



