## 1. Základní princip a pojmy

Při testování hypotéz ověřujeme na základě dat z výběru, zda platí určité tvrzení o celém základním souboru.

### Nulová ($H_0$) a Alternativní ($H_A$) hypotéza

- **$H_0$ (Nulová):** Vyjadřuje stav „beze změny“, „neexistuje vliv“ nebo „rovnost“. **Vždy obsahuje rovnítko** ($=$, $\le$, $\ge$). Považujeme ji za pravdivou, dokud nemáme silný důkaz pro opak.
    
- **$H_A$ (Alternativní):** Popírá nulovou hypotézu (to, co chceme prokazovat).
    

### Typy testů podle směru (Matlab parametr `tail`)

- **Oboustranný (`'both'`):** $H_0: \theta = \theta_0$ vs. $H_A: \theta \neq \theta_0$
    
- **Levostranný (`'left'`):** $H_0: \theta \ge \theta_0$ vs. $H_A: \theta < \theta_0$
    Když chci vědět jestli H1 je vetší než H0
- **Pravostranný (`'right'`):** $H_0: \theta \le \theta_0$ vs. $H_A: \theta > \theta_0$
	Když chci vědět jestli H0 je vetší než H1

### Rozhodování pomocí $p\text{-value}$

V moderní statistice (a v Matlabu) se rozhoduje podle vypočtené hodnoty $p\text{-value}$ ve srovnání s hladinou významnosti $\alpha$ (nejčastěji $\alpha = 0{,}05$):

- **$p\text{-value} < \alpha \implies$ Zamítáme $H_0$** (Prokázali jsme alternativu $H_A$).
    
- **$p\text{-value} \ge \alpha \implies$ Nezamítáme $H_0$** (Nemáme dost důkazů na změnu).
    

### Chyby při testování

- **Chyba I. druhu ($\alpha$):** $H_0$ platí, ale my ji chybně zamítneme (hladina významnosti, typicky 5 %).
    
- **Chyba II. druhu ($\beta$):** $H_0$ neplatí, ale my ji nezamítneme.
    
- _Platí:_ Snižováním $\alpha$ roste $\beta$. Pro snížení obou chyb současně potřebujeme více dat.
    

## 2. Jednovýběrové a párové testy (1 výběr)

Ověřujeme parametry jednoho souboru vůči konstantě, nebo porovnáváme dvojice dat „před a po“ na stejném objektu.

### A. Test rozptylu ($\sigma^2$)

- **Předpoklad:** Normální rozdělení dat.
    
- **Matlab:** `[h,p] = vartest(x, v)` (kde `v` je testovaný rozptyl).
    

### B. Test střední hodnoty ($\mu$)

- **Předpoklad:** Normální rozdělení dat.
    
- **Matlab:** `[h,p] = ttest(x, m, alpha, tail)` (testuje, zda se průměr rovná `m`).
    

### C. Párový t-test

- Používá se, když máme závislá data (např. pevnost oceli _před_ kalením a _po_ kalení na stejných vzorcích).
    
- **Princip:** Spočítá se sloupec rozdílů (`změna = po - před`) a na ten se pustí klasický `ttest` vůči nule.
    
- **Matlab:** `[h,p] = ttest(po - před, 0, alpha, tail)` nebo `ttest(po, před)`
    

### D. Neparametrické testy (Když data NEJSOU z normálního rozdělení)

Testují **medián** místo střední hodnoty.

- **Znaménkový test (`signtest`):** Velmi jednoduchý, pouze počítá, kolik hodnot je nad a pod testovaným mediánem. Sleduje znaménka. Vhodný i pro párový test: `signtest(x, y)`.
    
- **Wilcoxonův test (`signrank`):** Silnější než znaménkový test. Bere v úvahu i velikost odchylek (přiřazuje jim pořadí). Předpokládá symetrické rozdělení.
    

## 3. Dvouvýběrové testy (2 nezávislé výběry)

Porovnáváme dva různé, na sobě nezávislé soubory (např. životnost výrobků od výrobce A vs. výrobce B).

> **Klíčový postup:** Před testem středních hodnot **musíme vždy nejprve otestovat shodu rozptylů** (`vartest2`), abychom věděli, jaký typ t-testu použít.

### A. Test shody rozptylů ($\sigma_1^2 = \sigma_2^2$)

- **Matlab:** `[h,p] = vartest2(x, y)`
    

### B. Test shody středních hodnot ($\mu_1 = \mu_2$)

- **Předpoklad:** Normální rozdělení.
    
- **Matlab:** `[h,p] = ttest2(x, y, alpha, tail, vartype)`
    
    - Pokud rozptyly vyly shodné ($p \ge 0{,}05$ ve `vartest2`): `vartype = 'equal'`
        
    - Pokud se rozptyly liší ($p < 0{,}05$ ve `vartest2`): `vartype = 'unequal'`
        

### C. Neparametrický test mediánů (Mann-Whitney / Wilcoxon)

- Pokud data nemají normální rozdělení, testujeme shodu mediánů pomocí pořadí prvků.
    
- **Matlab:** `[h,p] = ranksum(x, y, 'tail', 'both')`
    

## 4. Vícevýběrové testy (3 a více výběrů)

### A. Test shody rozptylů pro více skupin

Chceme ověřit, zda mají všechny skupiny stejný rozptyl ($H_0: \sigma_1^2 = \sigma_2^2 = \dots = \sigma_k^2$).

- **Matlab:** `[p,stats] = vartestn(data, skupina, 'TestType', 'Bartlett')` (vyžaduje normalitu).
    
- **Matlab:** `[p,stats] = vartestn(data, skupina, 'TestType', 'LeveneQuadratic')` (robustní vůči nenormalitě).
    

### B. Jednofaktorová ANOVA (Analýza rozptylu)

Testuje shodu středních hodnot více skupin ($H_0: \mu_1 = \mu_2 = \dots = \mu_k$).

- **Předpoklady:** Nezávislost, normalita a shodné rozptyly všech skupin.
    
- **Matlab:** `[p,anovatab,stats] = anova1(data, skupina)`
    

### C. Kruskal-Wallisův test

Neparametrická obdoba ANOVy. Testuje shodu mediánů pro více souborů, pokud data nemají normální rozdělení.

- **Matlab:** `[p,anovatab,stats] = kruskalwallis(data, skupina)`
    

### D. Metody mnohonásobného porovnávání (`multcompare`)

Pokud ANOVA nebo Kruskal-Wallis **zamítnou** $H_0$ ($p < 0{,}05$), víme, že _některé_ skupiny se liší. Které to jsou konkrétně, zjistíme navazující funkcí:

- **Matlab:** `multcompare(stats)` (v grafu hned vidíš, které dvojice se překrývají a které ne. Pokud interval v tabulce rozdílů **neobsahuje nulu**, je mezi těmito dvěma skupinami statisticky významný rozdíl).
    

## 5. Dvouvýběrová a vícefaktorová ANOVA

Používá se, pokud jsou data ovlivněna **dvěma nebo více faktory současně** (např. testujeme životnost výrobku v závislosti na teplotě _A_ vlhkosti).

- Sleduje se vliv faktoru 1 (řádky), vliv faktoru 2 (sloupce) a jejich **interakce** (zda se vlivy faktorů navzájem zesilují/mění).
    
- **Matlab (Vyvážený model - matice dat):** `[p,table,stats] = anova2(X, reps)` (kde `reps` je počet opakování v buňce).
    
- **Matlab (Obecný/Nevyvážený model - dlouhé vektory):** `[p,table,stats] = anovan(y, {g1, g2}, 'model', 'interaction')`
    

## 🎯 Geniální tahák: Jaký test vybrat? (Finální rozhodovací tabulka)

| **Počet výběrů** | **Co testuji**                             | **Data jsou NORMÁLNÍ**           | **Data NEJSOU normální (Neparametrické)**      |
| ---------------- | ------------------------------------------ | -------------------------------- | ---------------------------------------------- |
| **1 výběr**      | Rozptyl ($\sigma^2$)                       | `vartest`                        | —                                              |
|                  | Střední hodnotu / Medián                   | `ttest`                          | `signtest` nebo `signrank`                     |
|                  | Párová data (před/po)                      | `ttest(po, pred)`                | `signtest(po, pred)` nebo `signrank(po, pred)` |
| **2 výběry**     | Shodu rozptylů ($\sigma_1^2 = \sigma_2^2$) | `vartest2`                       | —                                              |
|                  | Shodu stř. hodnot / Mediánů                | `ttest2` (volba _equal/unequal_) | `ranksum` (Mann-Whitney)                       |
| **3+ výběry**    | Shodu rozptylů                             | `vartestn` (Bartlett)            | `vartestn` (Levene)                            |
|                  | Shodu stř. hodnot / Mediánů                | `anova1`                         | `kruskalwallis`                                |
| **Více faktorů** | Kombinovaný vliv (např. teplota + vlhkost) | `anova2` nebo `anovan`           | `friedman` (jen vyvážená)                      |