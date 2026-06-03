![[Pasted image 20260528172324.png]]     
Centrální limitní věta

![[Pasted image 20260528175535.png]]
```
%pr7

%protoze meze jsou 0 a 1

n = 1000;

%stredni hodnota
mu = 0.5;

%rozptyl  ((b-a)^2/12)
Dx= (1-0)^2/12;

mu_prumer = mu;

%smerodatna odchylka
Dx_prumer = sqrt(Dx/n)

%vypocitame o kolik smerodatnych odchylek je dal nez stred
Z = (0.520-mu_prumer)/Dx_prumer;

%jelikož je větší tak

1-normcdf(Z)
```


![[Pasted image 20260528181825.png]]
```
%pr10

%stredni hodnota celku
Ex = 3*400;

%rozptyl celku
Dx = 4*400;

%smerodatna odchylka
Dx_ = sqrt(Dx);

%o kolik je dal hranice od ocekavaneho prumeru
Z = (1000-Ex)/Dx_;

normcdf(Z)
```
![[Pasted image 20260528193525.png]]

```
%pr 9

%stredni hodnota jednoho
Ex = 90;

%rozptyl jednoho
Dx= 10^2;

%stredni hodnota celku
Ex_ = Ex*64

%rozptyl celku
Dx_Sum = Dx * 64;

%celkova smerodatna odchylka
sigma = sqrt(Dx_Sum);

%o kolik smer. odchylech lezi dal nez stredu
Z = (6000-Ex_)/sigma;


1-normcdf(Z)
```
![[Pasted image 20260528194041.png]]
```
%pr 8

%stredni hodnota
Ex = 5;

%jelikož pro exponencialní rozdělení to je takto Ex = 1/lambda tak

%vypočítamé lambdu abychom mohli vypočítat Dx = 1/lambda^2

lambda = 1/5;

n=100;

%teoreticky rozptyl
Dx = 1/lambda^2

%počítáme průmer takže

Ex = 5;

%teoreticky rozptyl vybraneho prumeru
Dx_ = Dx/n;

%smerodatna odchylka
sigma = sqrt(Dx_)

Z = (4-Ex)/sigma

normcdf(Z)

```
![[Pasted image 20260528194722.png]]
![[Pasted image 20260601194644.png]]
tohle je myšleno k tomu rozptylu
```
%každý pokus má střední hodnotu 3 chyby a rozptyl 4 chyby na druhou

str_hodnota=(1+2+3+4+5+6)/6;


rozptyl=2*((1-str_hodnota)^2+(2-str_hodnota)^2+(3-str_hodnota)^2)/6;

% centrální limitní věta

pocet_hodu=100;

mu=str_hodnota*pocet_hodu;

sigma2=rozptyl*pocet_hodu;

sigma=sqrt(sigma2);

P=normcdf(380.5,mu,sigma)-normcdf(319.5,mu,sigma)
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

%stred. hodnota
Ex = n*1/6;

%teoreticky rozptyl (n * p * q) n = n, p = pravdepodobnost ze padne 6, q =
%pravdepodobnost ze 6 nepadne (1 - p) 
Dx = n*1/6*(1-1/6)

%smer. odchylka
sigma = sqrt(Dx);

Z = (104.5-Ex)/sigma;

1-normcdf(Z)
```
Rozdíl výběrových průměrů
![[Pasted image 20260528201057.png]]
```
%pr14 tohle je jinej typ příkladu kde jsou 2 hodnoty strřední hodnoty odečítame rozptyl sčítame ale pozer je to rozptyl takže na 2 

%stredni hodnota
Ex_plat = 27000;

%smer. odchylka
Dx_plat = 8000;

%sted. hodnota
Ex_naklad = 7000;

%odchylka
Dx_naklad = 2000;

%prumer stred. hodnot
Ex_both = Ex_plat-Ex_naklad;

%prumerny rozptyl 
Dx_both = Dx_plat^2+Dx_naklad^2;

%smer. odchylka
sigma = sqrt(Dx_both)

Z = (25000-Ex_both)/sigma;

1-normcdf(Z)
```
![[Pasted image 20260528201821.png]]
```
%pr 17

%zde je to taky jinný počítame podíl/procenta takže E = p, rozptyl =

%(sqrt(p*(1-p)/n)

%pravdepodobnost uspechu
p = 0.55;

%pocet odpovedi
n = 1000;

%stredni hodnota
E = p;

%smerodatna odchylka ne rozptyl
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

%podil pro 2015
p1 = a1/n1;

%podil pro 2016
p2 = a2/n2;

%stredni hodnota
E = p2-p1;

%kombinovana smer. odchylka
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
%tcdf kdyz potrebuju zjistit pravdepodobnost
%Když zadání začíná slovy: _„Určete pravděpodobnost, že...“
1-tcdf(1, 2)

1-tcdf(1, 4)

1-tcdf(1, 10)

1-tcdf(1, 100)

1-normcdf(1)
```
![[Pasted image 20260528203838.png]]
```
%pr 26 
%tinv pouziju kdyz znam pravdepodobst (kvantil)
%(Když zadání začíná slovy: _„Určete kvantil...“_ nebo _„Najděte %kritickou %hodnotu...“_)

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