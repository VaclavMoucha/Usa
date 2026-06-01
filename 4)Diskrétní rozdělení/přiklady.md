**![[Pasted image 20260530190714.png]]
**
![[Pasted image 20260528120142.png]]
**Binomické rozdělení:**

- Výběr **s vracením** (nebo nekonečná populace)
- Pravděpodobnost úspěchu p je **stále stejná** při každém tahu
- Např. hážeš mincí 10× — vždy 50% šance na hlavu

---

**Hypergeometrické rozdělení:**

- Výběr **bez vracení** z konečné populace
- Pravděpodobnost se **mění** s každým tahem
- Např. z balíčku karet taháš bez vracení — po každém tahu se mění počet karet
binomické
![[Pasted image 20260528101450.png]]
- zde vracime použijeme bino a pravděpodobnostní jelikož přesně 2x realná hodnota
- druhá otazka se jakoby neurčitá hodnota alespon 4 takže použijeme binocdf pro distribuční funkci 
```
binopdf(2,5,1/2)

1-binocdf(3.5,5,1/2)
```
![[Pasted image 20260528104011.png]]
Zde zase vracime a použijeme bino a podle konkretních hodnot použije bud pdf nebo cdf
```

binopdf(10,25,0.49)

1-binocdf(9.5,25,0.49)

1-binocdf(15,25,0.49)

d=0;

pravd=0;

for i=0:25

p=binopdf(i,25,0.49);

if p>pravd

pravd=p;

d=i;

end

end

d
```
![[Pasted image 20260528104434.png]]
```
binopdf(0,20,0.1)

1- binocdf(5,20,0.1)
```
hypergeometricke
![[Pasted image 20260528104900.png]]
![[Pasted image 20260528105158.png]]
```
hygepdf(2,32,4,3)

binopdf(2,3,1/8)
```
![[Pasted image 20260528105426.png]]
```
hygepdf(5,200,10,30)

binopdf(5,10,30/200)

vysledek=0;

p=0;

for i=0:10

pravd=hygepdf(i,200,10,30);

if pravd>p

vysledek=i;

p=pravd;

end

end

vysledek
```

![[Pasted image 20260528105925.png|523]]
```
hygepdf(22,17000,10000,30)

hygepdf(8,17000,7000,30)
```
geomertricke
![[Pasted image 20260528110634.png]]
geopdf(4,1/6)
```

geopdf(4,1/6)
```
![[Pasted image 20260528110331.png]]
```
for i=0:1000

%vyhraje první hráč, celkem lichý počet pokusů

P1=P1+geopdf(2*i,1/6);

%vyhraje druhý hráč, celkem sudý počet pokusů

P2=P2+geopdf(2*i+1,1/6);

end

P1

P2
```
![[Pasted image 20260528110847.png]]
```
geopdf(4,0.1)

geocdf(3.5,0.1)

1-geocdf(6.5,0.1)

```
negativně binomické
![[Pasted image 20260528111303.png]]
```
%a) desátý dárce bude právě 3. úspěšný

vysl_a=nbinpdf(7,3,0.35)

%b)bude potřeba do 9 dárců včetně

vysl_b=nbincdf(6.5,3,0.35);

vysl_b=1-vysl_b

%c)

vysl_c=nbincdf(7.5,3,0.35)-nbincdf(2.5,3,0.35)
```
Multinoimické
![[Pasted image 20260528111716.png]]
```
%ad a

%nezáleží kolik bude es, králů atd. Jsou dvě skupiny, proto binomické

%rozdělení

pravd_a=binopdf(8,10,16/32)

%ad b

%musí být právě 2 esa, 3 krále, 2 filci, 1 spodek a 2 ostatní. Více než 2

%skupiny, proto multinomické rozdělení

pravd_b=mnpdf([2,3,2,1,2],[4/32,4/32,4/32,4/32,16/32])

%ad ca

%hypergeometrické rozdělení. Jsou dvě skupiny

pravd_ca=hygepdf(8,32,16,10)

%ad cb

pravd_cb=nchoosek(4,2)*nchoosek(4,3)*nchoosek(4,2)*nchoosek(4,1)*nchoosek(16,2)/nchoosek(32,10)
```
Poissonovo
![[Pasted image 20260528113608.png]]
![[Pasted image 20260528112933.png]]
```
lambda = 10/100*20;

poisspdf(0,lambda)

poisspdf(2,lambda)

1-poisscdf(5,lambda)
```
![[Pasted image 20260528113509.png]]
tu jedničku tam píšeš podle toho jestli menší nebo větší
```
lambda = 5/10;

lambda2 = lambda * 25*2;

poisscdf(11.5,lambda2)

poisspdf(20,lambda2)

1-poisscdf(25,lambda2)
```
![[Pasted image 20260528114133.png]]
```
lambda = 600/60*1.5;

1-poisscdf(30,lambda)
```
Aproximace binomického a hypergeometrického rozdělení na Poissonovo
![[Pasted image 20260528114710.png]]
```
%binomické rozdělení
vysledek_a=binocdf(520.5,1000,0.5)-binocdf(479.5,1000,0.5)

%poissonovo rozdělení

%lambda=0.5*1000 pokusů

vysledek_b=poisscdf(520.5,500)-poisscdf(479.5,500)
```
![[Pasted image 20260528115733.png]]

```
hygepdf(2,49,6,6)

binopdf(2,6,6/49)

poisspdf(2,36/49)
```