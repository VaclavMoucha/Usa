## 1. Úvod do regresní analýzy

Zatímco v matematické analýze je vztah $y = f(x)$ přesný, ve statistice pracujeme se **stochastickou (náhodnou) závislostí**. Pro jednu hodnotu $x$ můžeme naměřit různé hodnoty $y$ (např. závislost váhy na výšce člověka).

- **Cíl regrese:** Proložit naměřená data $(x_i, y_i)$ vhodnou funkcí tak, aby se minimalizovala chyba měření.
    
- **Metoda nejmenších čtverců (MNČ):** Nejčastější přístup. Minimalizuje **součet kvadrátů reziduí** (rozdílů mezi naměřenou a modelem odhadnutou hodnotou).
    

## 2. Lineární regresní model

Statistický zápis modelu s jednou vysvětlující proměnnou:

$$y_i = a \cdot x_i + b + \varepsilon_i$$

- $x_i$: Nezávislá (vysvětlující) proměnná, **regresor**.
    
- $y_i$: Závislá (vysvětlovaná) proměnná, **regresand**.
    
- $a, b$: **Regresní koeficienty** ($a$ = směrnice přímky, $b$ = posun na ose $y$).
    
- $\varepsilon_i$: **Náhodná složka** (chyba) $i$-tého měření.
    
- $e_i = y_i - Y_i$: **Reziduum** (rozdíl mezi pozorovanou hodnotou $y_i$ a odhadem z modelu $Y_i$).
    

### Základní předpoklady modelu (Klíčové u zkoušky!)

1. **Normalita chyb:** Náhodné chyby $\varepsilon_i$ mají normální rozdělení.
    
2. **Nulová střední hodnota:** $E(\varepsilon_i) = 0$ (chyby se vzájemně neposouvají jedním směrem).
    
3. **Homoskedasticita:** Rozptyl náhodných chyb je konstantní $D(\varepsilon_i) = \sigma^2$.
    
4. **Lineární nezávislost:** Model nesmí vykazovat multikolinearitu (např. v $y = ax + bx + c$ nelze jednoznačně určit $a$ a $b$).
    

### Matematické vyjádření parametrů (z MNČ)

Cílem je minimalizovat funkci $\varphi = \sum e_i^2 = \sum (y_i - ax_i - b)^2$ pomocí parciálních derivací podle $a$ a $b$ položených rovnu nule. Výsledné vzorce:

$$a = \frac{\sum_{i=1}^{n} (x_i - \bar{x}) \cdot y_i}{\sum_{i=1}^{n} (x_i - \bar{x})^2}$$

$$b = \bar{y} - a \cdot \bar{x}$$

## 3. Maticový způsob výpočtu

Používá se pro vícenásobnou regresi nebo polynomy vyššího řádu (např. parabola $y = ax^2 + bx + c$).

$$\mathbf{b} = (\mathbf{F}'\mathbf{F})^{-1} \cdot \mathbf{F}' \cdot \mathbf{y}$$

- $\mathbf{b}$: Vektor hledaných parametrů $\begin{pmatrix} a \\ b \\ c \end{pmatrix}$.
    
- $\mathbf{F}$: **Matice modelu** obsahující hodnoty nezávislých proměnných (včetně sloupce jedniček pro absolutní člen $c$).
    
- $\mathbf{y}$: Sloupcový vektor naměřených hodnot závislé proměnné.
    

## 4. Výpočet a interpretace výsledků v Matlabu

V Matlabu se používá funkce `fitlm` (pro lineární/polynomiální modely) nebo `fitnlm` (pro obecné nelineární modely).

### Výstupní tabulka z `fitlm` / `fitnlm` a co v ní sledovat:

1. **Estimated Coefficients (Odhadované koeficienty):**
    
    - **Estimate:** Samotný odhad hodnoty parametru ($a, b, c$).
        
    - **SE (Standard Error):** Směrodatná odchylka odhadu parametru.
        
    - **pValue:** Testuje hypotézu $H_0: \text{parametr} = 0$. Pokud je $\mathbf{p\text{-value}} < \alpha$ (obvykle 0.05), parametr je **statisticky významný** a do modelu patří. Pokud je vysoká, parametr můžeme z modelu vyhodit.
        
2. **Kvalita celého modelu:**
    
    - **R-squared (Koeficient determinace $r^2$):** Udává, jaká část rozptylu dat je vysvětlena modelem. Nabývá hodnot $\langle 0; 1 \rangle$. Model je obvykle považován za dobrý, pokud $r^2 > 0.8$.
        
    - **F-statistic vs. constant model:** Testuje stabilitu modelu proti modelu, který by obsahoval pouze konstantu ($H_0: \text{všechny parametry kromě konstanty jsou nulové}$). Nízká $p\text{-value}$ u F-statistiky znamená, že model jako celek má smysl.
        
    - **Root Mean Squared Error (RMSE):** Odhad směrodatné odchylky reziduí. Čím menší, tím přesnější proložení.
        

## 5. Verifikace a úprava modelu

Po prvním výpočtu je nutné provést zpětnou kontrolu:

- **Přeparametrování (Overfitting):** Pokud zvolíme příliš vysoký stupeň polynomu (např. 5. stupeň pro 10 bodů), koeficient $r^2$ sice bude blízko 1, ale model bude vykazovat vysoké $p\text{-value}$ u jednotlivých koeficientů a Matlab může vyhodit varování: `Warning: The Jacobian at the solution is ill-conditioned...`.
    
- **Řešení:** Zjednodušit model odebráním nevýznamných parametrů (s vysokou $p\text{-value}$).
    

### Testování konkrétní hodnoty koeficientu

Chceme-li otestovat, zda je parametr roven určité konkrétní hodnotě (např. $H_0: a = \alpha$), použijeme testovací kritérium $T$, které má Studentovo rozdělení:

$$T = \frac{a - \alpha}{S_a}$$

Pokud vypočítané $T$ leží v kritickém oboru (mimo interval spolehlivosti získaný např. pomocí `coefCI`), $H_0$ zamítáme.

## 6. Nepolynomiální (nelineární) regrese

Používá se pro modely, které nelze vyjádřit jako polynom (např. $y = \sin(ax + b)$ nebo $y = a \cdot e^{bx}$). V Matlabu se zadává pomocí `@` (např. `modelfun = @(b,x) b(1) + sin(b(2)*x)`).

**⚠️ Zásadní úskalí u zkoušky:** Výpočet probíhá **numericky (iteračně)** a výsledek kriticky závisí na volbě **počátečního odhadu parametrů (`beta0`)**.

- **Případ 1 (Správný start):** Pokud je `beta0` blízko reálnému řešení, algoritmus najde globální minimum $\implies$ nízké RMSE, $r^2 \approx 1$.
    
- **Případ 2 (Špatný start):** Pokud je `beta0` daleko, algoritmus uvízne v lokálním minimu nebo se ztratí kvůli periodicitě funkcí ($\sin(x)$ vs $-\sin(-x)$) $\implies$ vysoké RMSE, mizerné (nebo i záporné) upravené $r^2$. U nelineární regrese je vždy nutný inženýrský nadhled a kontrola grafu!