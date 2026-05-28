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

Z = (1000-1200)/40;

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
