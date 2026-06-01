![[Pasted image 20260528150326.png]]
![[Pasted image 20260528140828.png]]
![[Pasted image 20260528121721.png]]

| **Rozdělení**         | **Funkce v MATLABu** | **Základní volání (Syntaxe)** | **Co přesně funkce vrací (Výstup)** | **Význam parametrů**                                                                       |
| --------------------- | -------------------- | ----------------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------ |
| **Rovnoměrné**        | `uniffit`            | `[vystup] = uniffit(data)`    | Dvouprvkový řádek: `[a, b]`         | `a` = dolní mez<br><br>  <br><br>`b` = horní mez                                           |
| **Exponenciální**     | `expfit`             | `[muhat] = expfit(data)`      | Jeden skalár (číslo): `muhat`       | `muhat` = střední hodnota ($\mu = 1/\lambda$)                                              |
| **Weibullovo**        | `wblfit`             | `[parhat] = wblfit(data)`     | Dvouprvkový řádek: `[a, b]`         | `a` = měřítko (scale)<br><br>  <br><br>`b` = tvar (shape)                                  |
| **Normální**          | `normfit`            | `[mu, sigma] = normfit(data)` | Dvě samostatná čísla: `mu`, `sigma` | `mu` = střední hodnota ($\mu$)<br><br>  <br><br>`sigma` = směrodatná odchylka ($\sigma$)   |
| **Log-normální**      | `lognfit`            | `[mu, sigma] = lognfit(data)` | Dvě samostatná čísla: `mu`, `sigma` | `mu` = střední hodnota _logaritmu dat_<br><br>  <br><br>`sigma` = odchylka _logaritmu dat_ |
| **Erlangovo (Gamma)** | `gamfit`             | `[parhat] = gamfit(data)`     | Dvouprvkový řádek: `[a, b]`         | `a` = tvar (počet fází, zaokrouhlit)<br><br>  <br><br>`b` = měřítko                        |
![[Pasted image 20260528122235.png]]
```
x=unifrnd(0,1,1,100);

y=5*x+10
```
Exponencialní
![[Pasted image 20260528123542.png]]
```
EX=3;

lambda=1/EX;

F=1-exp(-lambda*2)
```
![[Pasted image 20260528124216.png]]
```
%pr17a

vstup = readtable("P0517a.xlsx");

x = vstup.Var1(:,1);

a = expfit(x)

expcdf(10000,a/1)

poisspdf(2,8640/a)
```
Weibullovo rozdělení
![[Pasted image 20260528125457.png]]
```
x = importdata("P0521.mat");

wblfit(x)
```
![[Pasted image 20260528125737.png]]
```
data = readtable("P0521b.xlsx");

%výsledky ve formě struktury, vstupy jsou uloženy jako data a dále v listu1

%načteme 79 vstupních dat

x=data.Var1(:,1)';

%zkouska ukončena poruchou, tedy cens=0

%každé dato je jenom jednou

cens(1:79)=0;

freq(1:79)=1;

%přidání dat s ukončením zkoušky časem

x(80)=10000;

cens(80)=1;

freq(80)=21;

%výpočet

wblfit(x,0.05,cens,freq)
```
Normální rozdělení 
![[Pasted image 20260528135343.png]]
```
vysledek_a=norminv(0.2,5,2)

vysledek_b=norminv(0.5,5,2)

%symetrické kolem 0.5

vysledek_c=norminv(0.8,5,2)

vysledek_d=normcdf(3.5,5,2)

vysledek_e=normcdf(8,5,2)

vysledek_f=normcdf(6.5,5,2)
```

![[Pasted image 20260528141742.png]]
```
normcdf(51,50,0.7)-normcdf(49,50,0.7)
```
![[Pasted image 20260528142119.png]]
```
smerOdchylka = 3;

a = normcdf(5,0,smerOdchylka)-normcdf(-2,0,smerOdchylka)

b = 1 - a

c = a^3

d = 1-c
```
![[Pasted image 20260528144810.png]]
![[Pasted image 20260528145433.png]]![[Pasted image 20260528145735.png]]
```
a = 0.25 + normcdf(3,10,sqrt(20))

x = norminv(a,10,sqrt(20))
```
Logaritmicko blbost

![[Pasted image 20260528150450.png]]
```
logncdf(4, 3, 4) - logncdf(2, 3, 4)

x = 0:0.001:5;

plot(x, lognpdf(x, 3, 4))
```
![[Pasted image 20260528150727.png]]
```
a = exprnd(100,1000,1)

b = wblrnd(100,1.5,1000,1)

c = wblrnd(100,3,1000,1)

d = normrnd(100,30,1000,1)

data = [a,b,c,d]

boxplot(data)
```