![[Pasted image 20260528172324.png]]     
Centrální limitní věta

![[Pasted image 20260528175535.png]]
```
%pr7

%protoze meze jsou 0 a 1

n = 1000;

mu = 0.5;

Dx= (1-0)^2/12;

mu_prumer = mu;

Dx_prumer = sqrt(Dx/n)

Z = (0.520-mu_prumer)/Dx_prumer;

%jelikož je větší tak

1-normcdf(Z)
```


![[Pasted image 20260528181825.png]]
```
%pr10

Ex = 3*400;

Dx = 4*400;

Dx_ = sqrt(Dx);

Z = (1000-Ex)/Dx_;

normcdf(Z)
```
![[Pasted image 20260528193525.png]]

```
%pr 9

Ex = 90;

Dx= 10^2;

Ex_ = Ex*64

Dx_Sum = Dx * 64;

sigma = sqrt(Dx_Sum);

Z = (6000-Ex_)/sigma;

1-normcdf(Z)
```
![[Pasted image 20260528194041.png]]
```
%pr 8

Ex = 5;

%jelikož pro exponencialní rozdělení to je takto Ex = 1/lambda tak

%vypočítamé lambdu abychom mohli vypočítat Dx = 1/lambda^2

lambda = 1/5;

n=100;

Dx = 1/lambda^2

%počítáme průmer takže

Ex = 5;

Dx_ = Dx/n;

sigma = sqrt(Dx_)

Z = (4-Ex)/sigma

normcdf(Z)
```
![[Pasted image 20260528194722.png]]
```
%Pr 11

%hazime kostkou teda

Ex = (1+6)/2

Dx = (6-1)^2/12

n = 100

Ex_sum = Ex*n

Dx_sum = Dx*100

sigma = sqrt(Dx_sum)

%jelikož jsou 2 hranice udělame Z1 a Z2

Z1 = (319.5 - Ex_sum) / sigma

Z2 = (380.5 - Ex_sum) / sigma

normcdf(Z2)-normcdf(Z1)
```
![[Pasted image 20260528200054.png]]
![[Pasted image 20260528200411.png]]
Pro poisscdf

```
%pr 12;

1-binocdf(104.5,600,1/6)

lambda = 600*1/6;

1-poisscdf(104.5,lambda);

%ZDE je to jine počítame počet šestek takže jinný vzorec pro Ex a Dx

n=600;

Ex = n*1/6;

Dx = n*1/6*(1-1/6)

sigma = sqrt(Dx);

Z = (104.5-Ex)/sigma;

1-normcdf(Z)
```
Rozdíl výběrových průměrů
![[Pasted image 20260528201057.png]]
```
%pr14 tohle je jinej typ příkladu kde jsou 2 hodnoty strřední hodnoty odečítame rozptyl sčítame ale pozer je to rozptyl takže na 2 

Ex_plat = 27000;

Dx_plat = 8000;

Ex_naklad = 7000;

Dx_naklad = 2000;

Ex_both = Ex_plat-Ex_naklad;

Dx_both = Dx_plat^2+Dx_naklad^2;

sigma = sqrt(Dx_both)

Z = (25000-Ex_both)/sigma;

1-normcdf(Z)
```
![[Pasted image 20260528201821.png]]
```
%pr 17

%zde je to taky jinný počítame podíl/procenta takže E = p, rozptyl =

%(sqrt(p*(1-p)/n)

p = 0.55;

n = 1000;

E = p;

rozptyl = sqrt(p*(1-p)/n);

Z = (168/1000-E)/rozptyl;

normcdf(Z)
```
![[Pasted image 20260528202226.png]]
```
%pr 20

n1 = 250;

a1 = 62;

n2 = 340;

a2 = 141;

p1 = a1/n1;

p2 = a2/n2;

E = p2-p1;

sigma = sqrt(p1*(1-p1)/n1+p2*(1-p2)/n2);

%chceme kladný takže větší jak 0);

Z = (0-E)/sigma;

1-normcdf(Z)

fprintf('%.7f\n', 1-normcdf(Z))
```
![[Pasted image 20260528203038.png]]
```
%pr 21

Z = (0.1 -E)/sigma;

1-normcdf(Z) %jen změníme z 0 na 0.1
```
Chíííí kvadrat
![[Pasted image 20260528203237.png]]
```
%pr 22

chi2inv(0.05,10)

chi2inv(0.95,10)
```
![[Pasted image 20260528203433.png]]
```
%pr24

1-chi2cdf(20,12)
```
Studentovo
![[Pasted image 20260528203644.png]]

```
1-tcdf(1, 2)

1-tcdf(1, 4)

1-tcdf(1, 10)

1-tcdf(1, 100)

1-normcdf(1)
```
![[Pasted image 20260528203838.png]]
```
%pr 26

tinv(0.05,10)

tinv(0.95,10)
```
Fisherovo 
![[Pasted image 20260528203947.png]]
```
%pr27

finv(0.05, 10, 5)

finv(0.95, 10, 5)

finv(0.05, 5, 10)

finv(0.95, 5, 10)
```