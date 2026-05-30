Zde je přehledný a strukturovaný výtah teoretických základů z tvých podkladů. Text je rozdělen do logických bloků a zbaven balastu, aby se z něj dobře učilo na zkoušku.

## 1. Úvod do analýzy závislostí

Analýza závislostí zkoumá, zda jsou dva statistické znaky ($X$ a $Y$) na sobě nezávislé, nebo zda mezi nimi existuje vztah (např. vliv vzdělání na výši mzdy).

Volba metody závisí na typu dat:

- **Diskrétní hodnoty (kategoriální data):** Kontingenční tabulky.
    
- **Spojité hodnoty:** Kovariance, Pearsonův a Spearmanův korelační koeficient.
    

## 2. Kontingenční tabulky

Používají se pro **vizualizaci a testování závislosti diskrétních (kategoriálních) znaků**.

- **Struktura:** Řádky reprezentují hodnoty znaku $X$, sloupce hodnoty znaku $Y$. Buňky obsahují **empirické (naměřené) četnosti $O_{ij} = n_{ij}$**. Okrajové buňky (marginální četnosti) obsahují součty řádků ($n_{i.}$) a sloupců ($n_{.j}$). Celkový počet pozorování je $n$.
    

### Princip testování (Test nezávislosti $\chi^2$)

Testuje se, zda je výskyt kombinací znaků čistě náhodný (nezávislost), nebo zda vykazuje strukturu (závislost).

- **Hypotézy:**
    
    - $H_0$: Znaky $X$ a $Y$ jsou statisticky **nezávislé**.
        
    - $H_A$: Znaky $X$ a $Y$ jsou statisticky **závislé**.
        
- **Teoretické (očekávané) četnosti $E_{ij}$:** Četnosti, které bychom v tabulce čekali, pokud by platila nulová hypotéza (úplná nezávislost).
    
    $$E_{ij} = \frac{n_{i.} \cdot n_{.j}}{n}$$
    
- **Testovací kritérium $K$:**
    
    $$K = \sum_{i=1}^{r} \sum_{j=1}^{s} \frac{(O_{ij} - E_{ij})^2}{E_{ij}}$$
    
    Pokud $H_0$ platí, má veličina $K$ rozdělení $\chi^2$ (Chí-kvadrát) s $(r-1) \cdot (s-1)$ stupni volnosti.
    
- **Podmínky dobré shody:** Žádná $E_{ij}$ nesmí být $< 2$ a alespoň 80 % $E_{ij}$ musí být $> 5$.
    

## 3. Kovariance

Stanovuje **míru lineární závislosti** dvou spojitých náhodných veličin. Jde o „smíšený rozptyl“ dvou vektorů.

- **Vlastnosti hodnot:**
    
    - $cov(X, Y) > 0$: Obě veličiny současně rostou nebo klesají (přímá lineární závislost).
        
    - $cov(X, Y) < 0$: Jedna veličina roste, druhá klesá (nepřímá lineární závislost).
        
    - $cov(X, Y) \approx 0$: Veličiny se lineárně neovlivňují.
        
- **Klíčová pravidla:**
    
    - Pokud jsou $X, Y$ nezávislé $\implies cov(X, Y) = 0$.
        
    - **⚠️ Pozor (Obráceně to neplatí):** Pokud je $cov(X, Y) = 0$, neznamená to automaticky, že jsou veličiny nezávislé (může mezi nimi být jiná než lineární závislost, např. kvadratická).
        

## 4. Pearsonův korelační koeficient ($\rho$)

Používá se pro **spojité hodnoty**, u kterých předpokládáme **normální rozdělení**. Na rozdíl od kovariance je škálovaný, takže se lépe interpretuje.

- **Definice:** Je normován pomocí směrodatných odchylek do intervalu $\langle -1; 1 \rangle$.
    
    $$\rho = \frac{cov(X, Y)}{s(X) \cdot s(Y)}$$
    
- **Vlastnosti:**
    
    - $\rho = 1$: Dokonalá přímá lineární závislost.
        
    - $\rho = -1$: Dokonalá nepřímá lineární závislost.
        
    - $\rho = 0$: Veličiny jsou **nekorelované** (lineárně nezávislé, ale mohou vykazovat jinou závislost).
        

### Testování lineární závislosti

- **Hypotézy:** $H_0: \rho = 0$ (nekorelované) vs. $H_A: \rho \neq 0$ (korelované).
    
- **Testovací kritérium $T$:** Má Studentovo $t$-rozdělení s $n-2$ stupni volnosti.
    
    $$T = \frac{\rho \cdot \sqrt{n-2}}{\sqrt{1 - \rho^2}}$$
    

## 5. Spearmanův korelační koeficient ($r_s$)

Používá se pro **spojité hodnoty, které nemají normální rozdělení** (neparametrický test).

- **Princip:** Nepracuje přímo s naměřenými hodnotami, ale s jejich **pořadím** ($R_{Xi}$ a $R_{Yi}$) od nejmenší po největší. Sleduje, zda se při růstu jedné veličiny zvyšuje/snižuje pořadí druhé veličiny.
    
- **Definice:**
    
    $$r_s = 1 - \frac{6 \cdot \sum_{i=1}^{n} (R_{Xi} - R_{Yi})^2}{n \cdot (n^2 - 1)}$$
    
- **Vlastnosti:**
    
    - Při shodném pořadí obou veličin je $r_s = 1$. Při zcela opačném pořadí je $r_s = -1$.
        
    - Pokud je v datech hodně shodných hodnot, provádí se korekce (odečítají se opravné koeficienty $T_X$ a $T_Y$).
        

## 💡 Rychlá pomůcka pro rozhodování u zkoušky

| **Typ dat**                                           | **Předpoklad**       | **Vhodná metoda**                        |
| ----------------------------------------------------- | -------------------- | ---------------------------------------- |
| **Kategoriální / Diskrétní** (např. Ano/Ne, Vzdělání) | Žádný                | **Kontingenční tabulka** ($\chi^2$ test) |
| **Spojitá** (např. Výška, Hmotnost)                   | Normální rozdělení   | **Pearsonův koeficient** ($\rho$)        |
| **Spojitá** (např. Výška, Hmotnost)                   | Nenormální rozdělení | **Spearmanův koeficient** ($r_s$)        |