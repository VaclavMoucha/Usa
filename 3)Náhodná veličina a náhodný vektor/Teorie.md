# Náhodná veličina  
  
Náhodná veličina je reálná veličina (výsledek náhodného pokusu), která může nabývat různých hodnot.  
  
---  
  
# Distribuční funkce  
  
Distribuční funkce:  
  
$$  
F(x)=P(X \le x)  
$$  
  
udává pravděpodobnost, že náhodná veličina \(X\) bude menší nebo rovna \(x\).  
  
Někdy:  
  
$$  
F(x)=P(X<x)  
$$  
  
## Vlastnosti distribuční funkce  
  
- \(0 \le F(x) \le 1\)  
- funkce je neklesající  
  
$$  
x_1 < x_2 \Rightarrow F(x_1) \le F(x_2)  
$$  
  
- zleva spojitá  
  
$$  
\lim_{x \to -\infty}F(x)=0  
$$  
  
$$  
\lim_{x \to \infty}F(x)=1  
$$  
  
---  
  
# Diskrétní náhodná veličina  
  
Diskrétní náhodná veličina nabývá pouze diskrétních hodnot (konečně nebo spočetně mnoho).  
  
Pravděpodobnostní funkce:  
  
$$  
P(X=x_i)=p(x_i)  
$$  
  
Distribuční funkce:  
  
$$  
F(x)=\sum_{x_i \le x} p(x_i)  
$$  
  
---  
  
# Spojitá náhodná veličina  
  
Spojitá náhodná veličina nabývá všech hodnot z určitého intervalu.  
  
Používá se hustota pravděpodobnosti:  
  
$$  
f(x)=\frac{dF(x)}{dx}  
$$  
  
Pravděpodobnost:  
  
$$  
P(a \le X \le b)=\int_a^b f(x)\,dx  
$$  
  
## Vlastnosti hustoty  
  
$$  
f(x)\ge0  
$$  
  
$$  
\int_{-\infty}^{\infty} f(x)\,dx =1  
$$  
  
---  
  
# Číselné charakteristiky  
  
## Střední hodnota \(E(X)\)  
  
Průměrná hodnota náhodné veličiny.  
  
### Diskrétní  
  
$$  
E(X)=\sum x_i p(x_i)  
$$  
  
### Spojitá  
  
$$  
E(X)=\int_{-\infty}^{\infty} x f(x)\,dx  
$$  
  
---  
  
# Rozptyl \(D(X)\)  
  
Vyjadřuje rozptýlenost hodnot kolem střední hodnoty.  
  
### Diskrétní  
  
$$  
D(X)=\sum (x_i-E(X))^2 p(x_i)  
$$  
  
### Spojitá  
  
$$  
D(X)=\int_{-\infty}^{\infty}(x-E(X))^2 f(x)\,dx  
$$  
  
---  
  
# Směrodatná odchylka  
  
$$  
\sigma=\sqrt{D(X)}  
$$  
  
Udává variabilitu dat kolem průměru.  
  
---  
  
# Kvantily  
  
Kvantil \(x_p\):  
  
$$  
P(X<x_p)=p  
$$  
  
- medián = 50% kvantil  
- dolní kvartil = 25%  
- horní kvartil = 75%  
  
---  
  
# Modus  
  
Nejčetnější hodnota.  
  
---  
  
# Výběrové charakteristiky  
  
## Výběrový průměr  
  
$$  
\bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i  
$$  
  
---  
  
# Výběrový rozptyl  
  
$$  
s^2=\frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}  
$$  
  
---  
  
# Výběrová směrodatná odchylka  
  
$$  
s=\sqrt{\frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}}  
$$




Kdy distribuční funkce 
![[Pasted image 20260528100831.png]]
Používáš ji tehdy, když tě zajímá pravděpodobnost **kumulativní** (začínáš od nejmenšího možného minima a sčítáš pravděpodobnosti až po bod $x$). Matematicky vyjadřuje:
![[Pasted image 20260528100806.png]]


Kdy Pravděpodobností funkce 
![[Pasted image 20260528100823.png]]