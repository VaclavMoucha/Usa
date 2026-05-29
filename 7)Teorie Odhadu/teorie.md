## 1. Úvod do teorie odhadu

V praxi máme k dispozici pouze **náhodný výběr (data o rozsahu $n$)** a z něj počítáme výběrové charakteristiky (např. výběrový průměr $\bar{x}$). Cílem teorie odhadu je určit, kde se s vysokou pravděpodobností nachází **skutečný parametr** celého základního souboru.

- **Vliv rozsahu výběru ($n$):** Čím menší je množství dat, tím více výběrová střední hodnota kolísá. S rostoucím $n$ klesá rozptyl výběrového průměru podle vztahu:
    
    $$D(\bar{X}) = \frac{D(X_i)}{n}$$
    

## 2. Bodové odhady

Bodový odhad je jedno konkrétní číslo (statistika $T$), které aproximuje neznámý parametr $\Theta$. Aby byl bodový odhad kvalitní, musí splňovat 4 základní vlastnosti:

- **Nestrannost (Nevychýlenost):** Střední hodnota odhadu se rovná skutečnému parametru: $E(T) = \Theta$.
    
- **Konzistentnost:** S rostoucím rozsahem výběru ($n \to \infty$) klesá pravděpodobnost velké chyby k nule.
    
- **Vydatnost (Eficiencie):** Má ze všech nestranných odhadů nejmenší rozptyl ($\lim_{n\to\infty} D(T_n) = 0$).
    
- **Robustnost:** Odhad není výrazně ovlivněn odlehlými hodnotami či hrubými chybami (např. medián vs. min/max).
    

## 3. Intervalové odhady (Intervaly spolehlivosti)

Určují interval $\langle T_d; T_h \rangle$, ve kterém s předem zvolenou **spolehlivostí $1-\alpha$** leží skutečný parametr $\Theta$.

- **Hladina významnosti $\alpha$:** Pravděpodobnost, že skutečný parametr leží _mimo_ interval. Obvykle se volí $\alpha = 0{,}05$ (95% spolehlivost).
    
- **Vztah k datům:** Čím menší $\alpha$ (vyšší spolehlivost), tím je interval širší. Pro **2x užší interval** je potřeba mít **4x více dat**.
    

### Typy intervalů:

1. **Oboustranný:** Hledáme dolní i horní mez. Na každou stranu odsekáváme chybu $\frac{\alpha}{2}$.
    
2. **Jednostranný (Levostranný / Pravostranný):** Omezuje parametr pouze z jedné strany (v Matlabu značeno jako `'left'` pro interval $(-\infty; T_h\rangle$ a `'right'` pro $\langle T_d; \infty)$).
    

> **Pozor na Matlab:** Označení `'left'` a `'right'` v Matlabu neodpovídá českému slovnímu pojmenování (v Matlabu volba `'left'` testuje hypotézu, zda je průměr menší, což generuje pravostrannou/horní mez).

## 4. Odhady pro 1 výběr (Klíčové vzorce a Matlab)

### A. Střední hodnota $\mu$ (Normální rozdělení)

Předpokladem pro oba testy je, že data pocházejí z normálního rozdělení.

- **Případ 1: Rozptyl $\sigma$ je ZNÁMÝ** (Vzácný případ, využívá kvantily normovaného normálního rozdělení $z$)
    
    - _Oboustranný interval:_ $\langle\bar{x} - \frac{\sigma}{\sqrt{n}}z_{1-\frac{\alpha}{2}}; \bar{x} + \frac{\sigma}{\sqrt{n}}z_{1-\frac{\alpha}{2}}\rangle$
        
    - _Matlab:_ `[h,p,ci] = ztest(x, m, sigma, alpha, tail)`
        
- **Případ 2: Rozptyl $\sigma$ je NEZNÁMÝ** (Běžný případ, používá se výběrová odchylka $s$ a kvantily Studentova rozdělení $t$)
    
    - _Oboustranný interval:_ $\langle\bar{x} - \frac{s}{\sqrt{n}}t_{1-\frac{\alpha}{2}}(n-1); \bar{x} + \frac{s}{\sqrt{n}}t_{1-\frac{\alpha}{2}}(n-1)\rangle$
        
    - _Matlab:_ `[h,p,ci] = ttest(x, m, alpha, tail)`
        

### B. Rozptyl $\sigma^2$ a Směrodatná odchylka $\sigma$

Používá $\chi^2$ (Chí-kvadrát) rozdělení s $n-1$ stupni volnosti. Tento interval **není symetrický**.

- _Oboustranný interval pro rozptyl:_ $\langle\frac{(n-1)s^2}{\chi^2_{1-\frac{\alpha}{2}}(n-1)}; \frac{(n-1)s^2}{\chi^2_{\frac{\alpha}{2}}(n-1)}\rangle$
    
- _Odhad pro $\sigma$:_ V Matlabu samostatná funkce není. Spočítá se interval pro rozptyl a hodnoty se **odmocní**.
    
- _Matlab:_ `[h,p,ci] = vartest(x, v, alpha, tail)`
    

### C. Relativní četnost $\pi$ (Pro velká data $n > 30$)

Vychází z bodového odhadu pravděpodobnosti $p = \frac{x}{n}$. Není v Matlabu přímo implementován, nutno počítat ručně.

- _Oboustranný interval:_ $\langle p - \sqrt{\frac{p(1-p)}{n}}z_{1-\frac{\alpha}{2}}; p + \sqrt{\frac{p(1-p)}{n}}z_{1-\frac{\alpha}{2}}\rangle$
    

### D. Medián $x_{0{,}5}$ (Pro nenormální rozdělení)

Využívá interkvartilové rozpětí ($IQR = x_{0{,}75} - x_{0{,}25}$).

- _Vzorec:_ $x_{0{,}5} \pm 1{,}57 \cdot \frac{IQR}{\sqrt{n}}$
    

## 5. Odhad rozsahu výběru ($n$)

Určuje, kolik měření (respondentů) potřebujeme, abychom dosáhli požadované maximální šířky intervalu $\Delta_{max}$ (nebo přesnosti $\pm \text{chyba}$, kde šířka je dvojnásobek chyby).

- **Pro známý rozptyl $\sigma$:** $n \ge \left(\frac{2\sigma}{\Delta_{max}} \cdot z_{1-\frac{\alpha}{2}}\right)^2$
    
- **Pro neznámý rozptyl (odhad $s$):** $n \ge \left(\frac{2s}{\Delta_{max}} \cdot t_{1-\frac{\alpha}{2}}\right)^2$
    
- **Pro relativní četnost (volby):** $n \ge \frac{4p(1-p)}{\Delta_{max}^2} \cdot z_{1-\frac{\alpha}{2}}^2$
    

## 6. Odhady pro 2 výběry

### A. Poměr rozptylů $\frac{\sigma_1^2}{\sigma_2^2}$

Používá se k ověření, zda mají dva výběry shodný rozptyl (předpoklad pro dvouvýběrový t-test). Využívá Fisher-Snedecorovo $F$-rozdělení.

- _Matlab:_ `[h,p,ci] = vartest2(x, y, alpha, tail)`
    

### B. Rozdíl středních hodnot $\mu_1 - \mu_2$

Před výpočtem je nutné vědět (otestovat pomocí `vartest2`), zda jsou rozptyly obou souborů shodné či nikoliv.

- _Matlab:_ `[h,p,ci] = ttest2(x, y, alpha, tail, vartype)`
    
    - Pro shodné rozptyly: `vartype = 'equal'` (využívá Studentovo rozdělení s $n_1+n_2-2$ stupni volnosti).
        
    - Pro neshodné rozptyly: `vartype = 'unequal'` (Welchova aproximace stupňů volnosti).
        

> Pokud výsledný interval spolehlivosti rozdílu **obsahuje nulu** (např. $\langle -3{,}5; 2{,}5 \rangle$), znamená to, že mezi středními hodnotami obou výběrů **není statisticky významný rozdíl**.

## 7. Rychlý rozcestník funkcí v Matlabu

|**Cíl odhadu**|**Počet výběrů**|**Funkce v Matlabu**|
|---|---|---|
|**Střední hodnota ($\mu$)** – známé $\sigma$|1 výběr|`ztest`|
|**Střední hodnota ($\mu$)** – neznámé $\sigma$|1 výběr|`ttest`|
|**Rozptyl ($\sigma^2$) / Odchylka ($\sigma$)**|1 výběr|`vartest` (pro $\sigma$ odmocnit výsledek)|
|**Parametry nenormálních rozdělení**|1 výběr|`poissfit`, `expfit`, `wblfit`, `normfit`|
|**Empirická distribuční funkce**|1 výběr|`ecdf` / `cdfplot`|
|**Poměr rozptylů ($\sigma_1^2 / \sigma_2^2$)**|2 výběry|`vartest2`|
|**Rozdíl středních hodnot ($\mu_1 - \mu_2$)**|2 výběry|`ttest2` (volba `'equal'` / `'unequal'`)|