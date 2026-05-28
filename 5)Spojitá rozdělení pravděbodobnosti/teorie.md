# Spojitá rozdělení pravděpodobnosti – přehled

## Jak vybrat správné rozdělení?

|Situace|Rozdělení|
|---|---|
|Konstantní pravděpodobnost na intervalu|Rovnoměrné|
|Doba do **první** poruchy, konstantní intenzita|Exponenciální|
|Doba do poruchy s degradací / časnými poruchami|Weibullovo|
|Doba do **k-té** poruchy|Erlangovo (Gamma)|
|Součet mnoha nezávislých vlivů|Normální|
|Součin mnoha nezávislých vlivů|Logaritmicko-normální|

---

## 5.1 Rovnoměrné rozdělení `unif`

- Konstantní hustota na intervalu `<a, b>`
- **EX** = (a+b)/2, **DX** = (b−a)²/12, šikmost = 0
- Použití: generování náhodných čísel, simulace

```matlab
unifrnd(a,b,m,n)   % náhodná čísla
unifcdf(x,a,b)     % distribuční funkce
unifpdf(x,a,b)     % hustota pravděpodobnosti
unifinv(p,a,b)     % inverzní funkce (kvantil)
unifit(data)       % odhad parametrů
```

---

## 5.2 Exponenciální rozdělení `exp`

- Doba do **první události** Poissonova procesu
- Parametr: **μ** (střední hodnota) nebo **λ = 1/μ** (intenzita)
- **Bez paměti** – intenzita poruchy nezávisí na stáří
- **EX** = μ, **DX** = μ², šikmost = 2, špičatost = 6
- Použití: nedegradujíci výrobky, teorie front

```matlab
exprnd(mu,m,n)
expcdf(x,mu)
exppdf(x,mu)
expinv(p,mu)
expfit(x,0.05,cens,freq)   % cens: 0=porucha, 1=ukončeno časem
```

---

## 5.3 Weibullovo rozdělení `wbl`

- Obecnější než exponenciální, popisuje i degradaci
- Parametry: **a** (měřítko), **b** (tvar)
    - b = 1 → exponenciální
    - b < 1 → časné poruchy
    - b > 1 → poruchy z opotřebení
- **EX** = a·Γ(1 + 1/b)
- Použití: životnost výrobků obecně

```matlab
wblrnd(a,b)
wblcdf(t,a,b)
wblpdf(t,a,b)
wblinv(p,a,b)
wblfit(x,0.05,cens,freq)   % vrací [a, b]
wblstat(a,b)               % [střední hodnota, rozptyl]
wblplot(data)              % grafické ověření
```

---

## 5.4 Erlangovo (Gamma) rozdělení `gam`

- Doba do **k-té události** v Poissonově procesu
- Parametry: **k** (počet událostí), **b = 1/λ** (měřítko)
- **EX** = k/λ, **DX** = k/λ²
- Použití: když čekáme na více po sobě jdoucích poruch

```matlab
gamrnd(k,b)
gamcdf(t,k,b)
gampdf(t,k,b)
gaminv(p,k,b)
gamfit(data)       % vrací [k, b]
gamstat(k,b)
```

---

## 5.5 Normální rozdělení `norm`

- Nejpoužívanější rozdělení, symetrické
- Parametry: **μ** (střední hodnota), **σ** (směrodatná odchylka)
- **Pozor:** MATLAB bere σ, ne σ²!
- Šikmost = 0, špičatost = 3
- Pravidlo 3σ: 99,73 % dat leží v intervalu ⟨μ−3σ, μ+3σ⟩

|Interval|Pravděpodobnost|
|---|---|
|⟨μ±1σ⟩|68,27 %|
|⟨μ±2σ⟩|95,45 %|
|⟨μ±3σ⟩|99,73 %|

```matlab
normrnd(mu,sigma)
normcdf(x,mu,sigma)
normpdf(x,mu,sigma)
norminv(p,mu,sigma)
normfit(data)       % vrací [mu, sigma]
normstat(mu,sigma)
```

---

## 5.6 Normované normální rozdělení

- Speciální případ: **μ = 0, σ² = 1**
- Transformace: **Z = (X − μ) / σ**
- Využití: porovnání různých normálních rozdělení, tabulky

```matlab
norminv(0.9, 0, 1)   % = 1.2816 (90% kvantil)
```

---

## 5.7 Logaritmicko-normální rozdělení `logn`

- Vznikne jako e^X, kde X je normálně rozdělené
- Data převodem přes logaritmus chováme jako normální
- Nesymetrické, vhodné pro multiplikativní vlivy
- Použití: velikost částic, finanční data, biologické veličiny

```matlab
lognrnd(mu,sigma)
logncdf(x,mu,sigma)
lognpdf(x,mu,sigma)
logninv(p,mu,sigma)
lognfit(data)       % vrací [mu, sigma] logaritmů
lognstat(mu,sigma)
```

---

## 5.8 Grafické ověření rozdělení

|Metoda|Příkaz|Co sledovat|
|---|---|---|
|Empirická distribuční funkce|`cdfplot(x)`|Tvar průběhu|
|Weibullův pravděp. papír|`wblplot(data)`|Body leží na přímce → Weibull|
|Normální pravděp. papír|`normplot(data)`|Body leží na přímce → Normální|
|Obecný pravděp. papír|`probplot('normal',data)`|Typ dle zvoleného rozdělení|
|QQ plot|`qqplot(data)`|Přímka → normální; konvexní → kladná šikmost|
|Krabicový graf|`boxplot(x)`|Symetrie, rozptyl, odlehlá data|
# Popisná statistika – přehled

## Míry polohy (kde leží data)

| Název                        | Značka                             | Vzorec / popis                  | K čemu                                   |
| ---------------------------- | ---------------------------------- | ------------------------------- | ---------------------------------------- |
| **Střední hodnota** (průměr) | μ - muu(EX) (populace), x̄ (výběr) | součet / počet                  | Těžiště dat                              |
| **Medián**                   | x̃ nebo Me                         | prostřední hodnota po seřazení  | Střed dat, odolný vůči odlehlým hodnotám |
| **Modus**                    | Mo                                 | nejčastěji se opakující hodnota | Nejpravděpodobnější hodnota              |
| **Kvantil**                  | x_p                                | hodnota, pod níž leží p % dat   | Rozdělení dat na části                   |
| **Kvartily**                 | Q1, Q2, Q3                         | 25 %, 50 %, 75 % kvantil        | Q2 = medián                              |

---

## Míry variability (jak jsou data rozptýlená)

| Název                      | Značka                        | Vzorec                             | K čemu                                              |
| -------------------------- | ----------------------------- | ---------------------------------- | --------------------------------------------------- |
| **Rozptyl**                | σ² (DX)(populace), s² (výběr) | průměr čtverců odchylek od průměru | Celková variabilita, ale ve čtverci jednotek        |
| **Směrodatná odchylka**    | σ nebo s                      | √rozptyl                           | Variabilita ve stejných jednotkách jako data        |
| **Variační koeficient**    | CV                            | s / x̄ · 100 %                     | Relativní variabilita, srovnání různých souborů     |
| **Mezikvartilové rozpětí** | IQR                           | Q3 − Q1                            | Rozpětí prostředních 50 % dat, odolné vůči odlehlým |
| **Rozpětí**                | R                             | max − min                          | Celkový rozsah dat                                  |

---

## Míry tvaru rozdělení

|Název|Značka|Hodnota|Interpretace|
|---|---|---|---|
|**Šikmost**|a nebo γ₁|= 0 symetrické|> 0 ocas vpravo, < 0 ocas vlevo|
|**Špičatost**|b nebo γ₂|normální = 3 (nebo 0 po odečtení 3)|> 3 ostřejší vrchol, < 3 plošší|

---

## Rychlé pravidlo (normální rozdělení)

|Interval|% dat|
|---|---|
|μ ± 1σ|68 %|
|μ ± 2σ|95 %|
|μ ± 3σ|99,7 %|

---

## Matlab

```matlab
mean(x)       % střední hodnota
median(x)     % medián
mode(x)       % modus
var(x)        % rozptyl (výběrový)
std(x)        % směrodatná odchylka
iqr(x)        % mezikvartilové rozpětí
skewness(x)   % šikmost
kurtosis(x)   % špičatost
prctile(x,p)  % p-tý percentil (kvantil)
```