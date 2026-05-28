![[Pasted image 20260527214211.png]]
Pocet vsech krychli je 5 * 5 * 5 = 125
a)27/125 - 27 = 3 * 3 * 3, to je cast krychle uvnitr
b)54/125 - 54 = 3 * 3 * 6, 3 * 3 cast na jedne strane ktera ma jen jednu stranu * pocet stran
c)36/125 - 36 = 12 * 3, pocet hran * vzdy 3 maji jen 2 strany nabarvene
d)8/125 - 8 krychle ma 8 rohu

![[Pasted image 20260527220030.png]]
a)
Nahoře hledame 3 z 6 to jsou moznosti perlivych vod, dole 3 z 10 moznosti vsech vod
$$
\frac{\binom{6}{3}}{\binom{10}{3}}=0.167
$$
b)
$$ 
\frac{\binom{6}{1} * \binom{4}{2}}{\binom{10}{3}} = 0.300

$$
![[Pasted image 20260528082255.png]]
![[Pasted image 20260528082338.png]]
![[Pasted image 20260528082345.png]]

![[Pasted image 20260528082442.png]]
Hledáme 11 možností, 0 - 10 čísel. 
$$
\frac{\text{moje trefená} \times \text{cizí netrefená}}{\text{všechna vylosovaná}}
$$
$$ 
\frac{\binom{10}{i} * \binom{70}{20-i}}{\binom{80}{20}}
$$
```
for i = 0:10

nchoosek(10,i)*nchoosek(70,20-i)/nchoosek(80,20)

end

```

![[Pasted image 20260528083402.png]]
(eso  * zbytek) / celkem
```
nchoosek(4,1)*nchoosek(28,2)/nchoosek(32,3)
```

Geometrická pravděpodobnost:

![[Pasted image 20260528083753.png]]

$$ P = \frac{S_{\text{kruh}}}{S_{\text{čtverec}}} = \frac{\pi \cdot r^2}{a^2} = \frac{\pi \cdot 1^2}{3^2} = \frac{\pi}{9} \approx 0{,}3491 $$
![[Pasted image 20260528083913.png]]!
![[Pasted image 20260528084009.png]]
60^2 celková "plocha", (60-15)^2 "plocha setkání" / celkvovou plochou

Vlastnosti pravděpodobnosti, nezávislost jevů, Bayesova věta
![[Pasted image 20260528084139.png]]
![[Pasted image 20260528084131.png]]
![[Pasted image 20260528084218.png]]
Vlevo v Př19
![[Pasted image 20260528090058.png|631]]
