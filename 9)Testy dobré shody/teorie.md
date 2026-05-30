Zde je přehledný, stručný a srozumitelný výtah z kapitoly **Testy dobré shody**. Tento tahák ti poslouží k rychlému pochopení toho, jak ověřit, z jakého rozdělení data pocházejí, a jaké funkce k tomu v Matlabu použít.

## 1. Princip testů dobré shody

Zatímco předchozí kapitoly předpokládaly, že data mají určité rozdělení (např. normální), **testy dobré shody** slouží k tomu, abychom tento předpoklad statisticky ověřili.

- **$H_0$ (Nulová):** Teoretické (předpokládané) a empirické (naměřené) rozdělení se shodují.
    
- **$H_A$ (Alternativní):** Teoretické a empirické rozdělení se neshodují.
    

### Hlavní přístupy:

1. **$\chi^2$ (Chí-kvadrát) test dobré shody:** Srovnává **skutečné četnosti** ($O_i$) s **očekávanými četnostmi** ($E_i$) v jednotlivých intervalech/kategoriích.
    
2. **Kolmogorov-Smirnovův test:** Sleduje **maximální vertikální rozdíl** mezi teoretickou a empirickou distribuční funkcí.
    

## 2. $\chi^2$ test dobré shody

Používá se pro diskrétní data (kategorie, hod kostkou) nebo spojitá data rozdělená do intervalů.

### Klíčové podmínky a vlastnosti:

- **Podmínka velkého výběru:** V každé skupině/intervalu musí být očekávaná četnost **$E_i > 5$**. Pokud není, musí se sousední intervaly sloučit!
    
- Při výrazném slučování intervalů klesá počet stupňů volnosti (`df`), což může zkreslit výsledek (Matlab na to upozorní varováním: _Warning: After pooling, some bins still have low expected counts..._). V takovém případě je lepší použít Kolmogorov-Smirnovův test.
    

### Funkce v Matlabu: `chi2gof`

`[h, p, stats] = chi2gof(x, 'Parametr', Hodnota, ...)`

- **Porovnání s konkrétním rozdělením (`'cdf'`):**
    
    - Pro normální rozdělení: `'cdf', {@normcdf, mean(x), std(x)}`
        
    - Pro exponenciální rozdělení: `'cdf', {@expcdf, 100}`
        
- **Porovnání relativních četností (např. kostka):**
    
    - Zadávají se parametry `'expected'` (vektor očekávaných četností), `'edges'` (hranice intervalů) a `'frequency'` (skutečně naměřené četnosti).
        

## 3. Kolmogorov-Smirnovův (K-S) test

Tento test je vhodný pro **spojitá rozdělení**. Je založen na hledání největšího rozdílu mezi grafy distribučních funkcí.

### A. Jednovýběrový test (`kstest`)

Ověřuje, zda data pocházejí z přesně definovaného spojitého rozdělení, jehož parametry předem **známe**.

- **Matlab:** `[h, p, ksstat, cv] = kstest(x, CDF)`
    
    - _CDF_ je matice o 2 sloupcích: 1. sloupec = data `x`, 2. sloupec = hodnoty teoretické distribuční funkce (např. vypočtené pomocí `normcdf`).
        

### B. Lillieforsův test (`lillietest`)

Speciální a velmi používaná modifikace K-S testu. Používá se, pokud chceme ověřit, zda data mají normální nebo exponenciální rozdělení, ale **neznáme jejich parametry** (Matlab si je odhadne z dat sám).

- **Časté využití:** Ověření normality dat před spuštěním t-testu nebo ANOVy.
    
- **Matlab:** `[h, p, kstat, critval] = lillietest(x, alpha, 'Distr')`
    
    - `'Distr'` může být `'norm'` (normální) nebo `'exp'` (exponenciální).
        

### C. Dvouvýběrový test (`kstest2`)

Ověřuje, zda **dva nezávislé výběry** pocházejí ze **shodného** (jakéhokoliv) rozdělení ($H_0: F(x) = F(y)$). Srovnává dvě empirické distribuční funkce mezi sebou.

- **Matlab:** `[h, p, kstext] = kstest2(x, y, alpha)`
    

## 🎯 Rychlý přehled: Kdy jakou funkci použít?

| **Typ úlohy / dat**                     | **Co chci ověřit**                                           | **Matlab funkce**                       |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| **Diskrétní data / četnosti kategorií** | Zda je kostka férová / zda data odpovídají poměrům           | `chi2gof` (s parametrem `'expected'`)   |
| **Spojitá data rozdělená do intervalů** | Shodu s rozdělením (např. s exponenciálním)                  | `chi2gof` (s parametrem `'cdf'`)        |
| **1 výběr vs. ZNÁMÉ rozdělení**         | Shodu s rozdělením o přesných parametrech (např. $N(10, 5)$) | `kstest`                                |
| **1 výběr vs. NEZNÁMÉ rozdělení**       | Zda mají data normalitu (pro t-test) nebo exp. rozdělení     | `lillietest` (volba `'norm'` / `'exp'`) |
| **2 nezávislé výběry**                  | Zda mají oba soubory stejné rozdělení / distribuční funkci   | `kstest2`                               |
Pro debili jako já kterej si nepamatuje jak se značí každa chujovina 
# Přehled statistických veličin

| Statistická veličina          |                  Teorie / Populace                  | Výběr z dat | Matlab ekvivalent            | Význam / Poznámka                                             |
| :---------------------------- | :-------------------------------------------------: | :---------: | :--------------------------- | :------------------------------------------------------------ |
| **Rozsah výběru**             |                         $N$                         |     $n$     | `length(x)`, `numel(x)`      | Počet naměřených hodnot (velikost vektoru).                   |
| **Střední hodnota / Průměr**  |                  $\mu$ nebo $E(X)$                  |  $\bar{x}$  | `mean(x)`                    | Očekávaná hodnota vs. aritmetický průměr.                     |
| **Rozptyl**                   |               $\sigma^2$ nebo $D(X)$                |    $s^2$    | `var(x)`                     | Míra variability (kvadrát odchylek od průměru).               |
| **Směrodatná odchylka**       |                      $\sigma$                       |     $s$     | `std(x)`                     | Odmocnina z rozptylu (stejná jednotka jako data).             |
| **Medián**                    |               $x_{0.5}$ nebo $Med(X)$               | $\tilde{x}$ | `median(x)`                  | Prostřední hodnota (50% kvantil) po seřazení.                 |
| **Modus**                     |                      $Mod(X)$                       |  $\hat{x}$  | `mode(x)`                    | Nejčastěji se vyskytující hodnota v datech.                   |
| **Pravděpodobnost / Četnost** |                  $\pi$ nebo $P(A)$                  |     $p$     | `p` nebo `pval`              | Teoretická pravděpodobnost vs. relativní četnost ($p = k/n$). |
| **Hladina významnosti**       |                      $\alpha$                       |      —      | `alpha`                      | Pravděpodobnost chyby I. druhu (standardně 0.05).             |
| **Síla testu**                |                     $1 - \beta$                     |      —      | —                            | Pravděpodobnost, že správně zamítneš neplatnou H0.            |
| **Kvantil rozdělení**         | $z_{1-\alpha}$, $t_{1-\alpha}$, $\chi^2_{1-\alpha}$ |      —      | `norminv`, `tinv`, `chi2inv` | Hraniční body rozdělení pro testování hypotéz.                |
| **Distribuční funkce**        |                       $F(x)$                        |  $F_n(x)$   | `normcdf`, `ecdf(x)`         | Kumulativní pravděpodobnost $P(X \le x)$.                     |
| **Hustota pravděpodobnosti**  |                       $f(x)$                        |      —      | `normpdf`, `exppdf`          | Funkce popisující tvar spojitého rozdělení.                   |