![[Pasted image 20260527201344.png]]
$\frac{1}{10} * \frac{1}{9} = 0.0111$

![[Pasted image 20260527201747.png]]
Jelikož zde jsou 3 liché a 2 sudé tím pádem $\frac{2}{5}= 0.4$

Variace
	-Záleží na pořadí 
Permutace 
	-Přeskládání 
Kombinace 
	 -Nezaleží na pořadí, vybíráme skupinu

![[Pasted image 20260527201912.png]]
Zde záleží na pořadí a hráči se nebudou opakovat použijeme Variaci
$$V_k^n = \frac{n!}{(n-k)!} = \frac{10!}{(10-4)!}= 10*9*8*7=5040$$

![[Pasted image 20260527202400.png]]
Zde se čísla opakují a záleží na pořadí je rozdíl 123456 654321
$$
V^{\prime n}_k  = n^k = 6^5 = 7666
$$
![[Pasted image 20260527202646.png]]
Vybíráme část, proto to neni permutace, zalezi na poradi, neopakuji se

10 * 9 * 8 * 7 * 6 * 5 = 151200 

![[Pasted image 20260527203300.png]]
Tohle je permutace s vícero prvky neboli opakováním
$$  
P_n = \frac{n!}{n_1! \cdot n_2! \cdot \ldots \cdot n_k!} =\frac{12!}{3! * 4! *5!}=   

$$
**![[Pasted image 20260527204340.png]]
zde je vzorec pro permutace bez opakování - musí být vybrány všechny**

![[Pasted image 20260527203659.png]]
![[Pasted image 20260527204246.png]]
![[Pasted image 20260527204258.png]]
a) zde můžeme usoudit že se budou pohlednice opakovat takže jednoduše v matlabu
$$K'(10, 7) = \binom{7 + 10 - 1}{10} = \binom{16}{10}$$
```
nchoosek(17-1,10);
```
b)
$$K'(10, 7) = \binom{7 + 5 - 1}{5} = \binom{11}{5}$$
```
nchoosek(11,5);
```
c) zde se to už  neopakuje 
$$K(5, 7) = \binom{7}{5}$$
```
nchoosek(7,5)
```
![[Pasted image 20260527204025.png]]
selský rozum každej poslal 7 takže 7 * 8 = 56 

![[Pasted image 20260527204046.png]]
12 týmů každý hraje 11 zapasu, 12 * 11, ted ale kazdy zapas zapocitan 2x proto /2
$$\binom{12}{2} = \frac{12 \times 11}{2 \times 1} = 66$$
```
nchoosek(12,2)
```

Kombinační pravidlo součinu
![[Pasted image 20260527204441.png]]
a)normálně 
$$
\frac{1}{6} * \frac{1}{6} * \frac{1}{6} = 0.0046
$$
b) Ta 6 protože vlastně stejných čísel může být 6
$$
\frac{1}{6} * \frac{1}{6} * \frac{1}{6} * 6 = 0.02777
$$
c) Zde si musíme říct že vlastně vždy musí být 2 šestky  a jedna jiná takže
 takže to může byt (6 6 X,6 X 6, X 6 6) a za x muže být 1-5  takže výsledek je 
 protože 216 = 6 * 6 * 6 a 15 = 3 pozice kde muze byt cislo 1-5, takze 15 = (3 nad 1) * 5
$$
 \frac{15}{216}
$$
![[Pasted image 20260527205313.png]]
$$\binom{8}{5} * \binom{8}{4}$$
```
nchoosek(8,5) * nchoosek(8,4);
```

![[Pasted image 20260527205408.png]]
a)
$$
\frac{4}{32} * \frac{4}{32} * \frac{4}{32} * \frac{4}{32} =  2.4414e-04
$$
b)
$$
\frac{4}{32} * \frac{3}{31} * \frac{2}{30} * \frac{1}{29} =  2.7809e-05
$$
![[Pasted image 20260527205651.png]]
Poskladaní všech moznosti prikladu pomocí kombinačních čísel
$$m = \binom{10}{3} = \frac{10 \times 9 \times 8}{3 \times 2 \times 1} = 120$$
a) Vybíráme kombinaci prikladu 3 z 5 znamych, vydelime poctem vsech moznosti
$$m_a = \binom{5}{3} = 10 \quad P_a = \frac{10}{120} = 0.0833 $$
b) Vybere 2 z 5 znamych, pak 1 z 5 neznamych, vynasobime protoze potrebujeme kombinaci vsech moznosti znamych * neznamych 
$$
\frac{\binom{5}{2} * \binom{5}{1}}{120}  = 0.4167 
$$
![[Pasted image 20260527210706.png]]
a) Spočteme dohromady (20) a dame nad kolik je moznosti (6) 

```
nchoosek(20,6)
```
b) dole celkový možný variant a nahoře pro každej výběr 
$$  
P =  
\frac{\binom{5}{2} \times \binom{15}{4}}  
{\binom{20}{6}}  
=  
\frac{13650}{38760}  
\approx 0.352  
$$
![[Pasted image 20260527212155.png]]
$$  
\frac{\binom{5}{0}\binom{15}{6}}{\binom{20}{6}}  +  \frac{\binom{5}{1}\binom{15}{5}}{\binom{20}{6}}  +  \frac{\binom{5}{2}\binom{15}{4}}{\binom{20}{6}}  +  \frac{\binom{5}{3}\binom{15}{3}}{\binom{20}{6}}  +  \frac{\binom{5}{4}\binom{15}{2}}{\binom{20}{6}}  +  \frac{\binom{5}{5}\binom{15}{1}}{\binom{20}{6}}  = 1  
$$
Sčítání pravděpodobností

![[Pasted image 20260527212231.png]]
jsou 4 spodci a 4 filci take 8 žaludovych karet, ale musime odebrat spodka a filka z zaludu
$$
\frac{4}{32}+ \frac{4}{32}+ \frac{6}{32} = 0.4375
$$
![[Pasted image 20260527212727.png]]
Pole je 8x8, tim padem vybere pro 5 vezi z 8 sloupcu a 8 radku a to tam musime rozdat ty veze proto 5!
$$  
\binom{8}{5}*\binom{8}{5}*5!  
=  
56 \cdot 56 \cdot 120  
=  
376320  
$$
![[Pasted image 20260527212828.png]]
5 chapcu z 15, 5 holek z 10
$$\binom{15}{5}*\binom{10}{5}=3003 \cdot 252=756756
$$