# Výběrové charakteristiky – přehled

## Pravděpodobnost vs. Statistika

|Pravděpodobnost|Statistika|
|---|---|
|Střední hodnota E(X), μ|Výběrový průměr X̄|
|Rozptyl D(X), σ²|Výběrový rozptyl s²|
|Směrodatná odchylka σ|Výběrová směrodatná odchylka s|
|Pravděpodobnost jevu π|Relativní četnost p|
|Medián x₀.₅|Výběrový medián|

---

## Vlastnosti střední hodnoty a rozptylu

|Vzorec|Slovně|
|---|---|
|E(X₁ + X₂) = E(X₁) + E(X₂)|Střední hodnoty se sčítají|
|D(X₁ + X₂) = D(X₁) + D(X₂)|Rozptyly se sčítají (jen nezávislé!)|
|E(aX) = a·E(X)|Konstanta se vynásobí|
|D(aX) = a²·D(X)|Konstanta se umocní|

---

## Výběrový průměr

Z n nezávislých měření X₁, X₂, … Xₙ:

- **E(X̄) = μ** – průměr výběru = střední hodnota
- **D(X̄) = σ²/n** – čím více dat, tím menší rozptyl průměru

---

## Zákon velkých čísel

Čím více měření, tím blíže je výběrový průměr ke skutečné střední hodnotě.

---

## Centrální limitní věta (CLV)

Součet nebo průměr velkého počtu nezávislých náhodných veličin má **přibližně normální rozdělení** – bez ohledu na původní rozdělení.

**Požadavek:** n ≥ 30 (nebo n ≥ 15 pro symetrická data bez odlehlých hodnot)

### Součet n veličin:

```
ΣXᵢ ~ N(n·μ, n·σ²)
```

### Průměr n veličin:

```
X̄ ~ N(μ, σ²/n)
```

### Matlab:

```matlab
% Součet
normcdf(x, n*mu, sqrt(n)*sigma)

% Průměr
normcdf(x, mu, sigma/sqrt(n))
```

---

## Relativní četnost

- p = počet úspěchů / n
- **E(p) = π**, **D(p) = π·(1−π)/n**
- Předpoklad: n > 9 / (p·(1−p))

```matlab
% P(p < x)
normcdf(x, pi, sqrt(pi*(1-pi)/n))
```

---

## Rozdíl výběrových průměrů

Dva nezávislé výběry s μ₁, σ₁² a μ₂, σ₂²:

- **E(X̄₁ − X̄₂) = μ₁ − μ₂**
- **D(X̄₁ − X̄₂) = σ₁²/n₁ + σ₂²/n₂**

```matlab
mu_diff = mu1 - mu2;
sigma_diff = sqrt(sigma1^2/n1 + sigma2^2/n2);
normcdf(x, mu_diff, sigma_diff)
```

---

## Statistická rozdělení

### χ² (chí kvadrát) – `chi2`

- Součet čtverců normovaných normálních veličin
- Parametr: **n** (stupně volnosti)
- E(X) = n, D(X) = 2n
- Použití: testování rozptylu, nezávislosti, shody rozdělení

```matlab
chi2cdf(x, n)
chi2inv(p, n)
```

### Studentovo t-rozdělení – `t`

- Parametr: **n** (stupně volnosti)
- E(X) = 0, symetrické kolem 0
- Pro n > 30 se blíží normovanému normálnímu rozdělení
- Použití: testování střední hodnoty, když **neznáme σ**

```matlab
tcdf(x, n)
tinv(p, n)
```

### Fisher-Snedecorovo F-rozdělení – `f`

- Parametry: **m, n** (stupně volnosti)
- Nesymetrické, pouze kladné hodnoty
- Použití: testování shody rozptylů, ANOVA

```matlab
fcdf(x, m, n)
finv(p, m, n)
```

---

## Kdy použít které rozdělení?

|Situace|Rozdělení|
|---|---|
|Průměr / součet velkého výběru|Normální (CLV)|
|Testování střední hodnoty, σ neznámé|Studentovo t|
|Testování rozptylu|χ²|
|Porovnání dvou rozptylů|Fisher-Snedecor F|
