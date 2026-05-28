# Diskrétní rozdělení pravděpodobnosti  
  
Diskrétní rozdělení používáme tehdy, když náhodná veličina nabývá pouze určitých oddělených hodnot.  
  
Např:  
- počet studentů,  
- počet poruch,  
- počet hodů,  
- počet úspěchů.  
  
Diskrétní hodnoty jsou:  
- konečné,  
- nebo spočetně nekonečné.  
  
---  
  
# Jak poznat diskrétní náhodnou veličinu  
  
Hodnoty jsou:  
- celé,  
- oddělené,  
- spočetné.  
  
Např:  
- 0,1,2,3,...  
- počet aut,  
- počet zákazníků,  
- počet vadných výrobků.  
  
---  
  
# Pravděpodobnostní funkce  
  
Pravděpodobnostní funkce:  
  
$$  
P(X=x_i)=p(x_i)  
$$  
  
udává pravděpodobnost, že náhodná veličina nabude přímo hodnoty \(x_i\).  
  
---  
  
# Distribuční funkce diskrétní veličiny  
  
$$  
F(x)=\sum_{x_i \le x} p(x_i)  
$$  
  
Distribuční funkce udává pravděpodobnost, že náhodná veličina bude menší nebo rovna \(x\).  
  
---  
  
# Bernoulliho rozdělení  
  
Používá se:  
- pro jeden pokus,  
- existují pouze 2 výsledky.  
  
Např:  
- ano/ne,  
- úspěch/neúspěch,  
- panna/orel.  
  
## Pravděpodobnosti  
  
$$  
P(X=1)=p  
$$  
  
$$  
P(X=0)=1-p  
$$  
  
## Kdy použít  
  
Když:  
- existuje pouze jeden pokus,  
- pouze dva možné výsledky.  
  
---  
  
# Binomické rozdělení  
  
NEJDŮLEŽITĚJŠÍ diskrétní rozdělení.  
  
Používá se:  
- při opakování Bernoulliho pokusu,  
- počítá počet úspěchů z \(n\) pokusů.  
  
## Podmínky  
  
Musí platit:  
- pevný počet pokusů \(n\),  
- stejné \(p\),  
- nezávislé pokusy,  
- pouze úspěch/neúspěch.  
  
## Vzorec  
  
$$  
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}  
$$  
  
## Co znamenají symboly  
  
- \(n\) = počet pokusů  
- \(k\) = počet úspěchů  
- \(p\) = pravděpodobnost úspěchu  
  
## Kdy použít  
  
Když zadání obsahuje:  
- „z \(n\) pokusů“  
- „kolikrát nastane“  
- „počet úspěchů“  
  
## Typické příklady  
  
- počet šestek při 10 hodech,  
- počet vadných výrobků,  
- počet úspěšných studentů.  
  
---  
  
# Geometrické rozdělení  
  
Používá se:  
- když hledáme počet pokusů do prvního úspěchu.  
  
## Vzorec  
  
$$  
P(X=k)=(1-p)^{k-1}p  
$$  
  
## Kdy použít  
  
Když zadání obsahuje:  
- „do prvního úspěchu“  
- „kolik pokusů než“  
- „první výhra“  
  
## Typické příklady  
  
- počet hodů do první šestky,  
- počet pokusů do první poruchy.  
  
---  
  
# Poissonovo rozdělení  
  
Používá se:  
- pro počet výskytů za čas nebo prostor.  
  
## Typické použití  
  
- počet aut za hodinu,  
- počet poruch za den,  
- počet zákazníků za minutu.  
  
## Vzorec  
  
$$  
P(X=k)=\frac{\lambda^k e^{-\lambda}}{k!}  
$$  
  
## Co znamená \(\lambda\)  
  
Průměrný počet výskytů.  
  
Např:  
- průměrně 5 zákazníků za hodinu,  
- průměrně 2 poruchy za den.  
  
## Kdy použít  
  
Když zadání obsahuje:  
- počet událostí za čas,  
- intenzitu výskytu,  
- počet jevů v intervalu.  
  
---  
  
# Hypergeometrické rozdělení  
  
Používá se:  
- při výběru bez vracení.  
  
## Nejdůležitější znak  
  
❗ Bez vracení ❗  
  
## Typické příklady  
  
- tahání karet,  
- koule z osudí,  
- kontrola výrobků.  
  
---  
  
# Rozdíl Binomické vs Hypergeometrické  
  
## Binomické rozdělení  
  
- s vracením,  
- pravděpodobnost se nemění,  
- nezávislé pokusy.  
  
## Hypergeometrické rozdělení  
  
- bez vracení,  
- pravděpodobnost se mění,  
- závislé pokusy.  
  
---  
  
# Jak poznat správné rozdělení  
  
| Situace | Rozdělení |  
|---|---|  
| Jeden pokus ano/ne | Bernoulli |  
| Počet úspěchů z n pokusů | Binomické |  
| Počet pokusů do prvního úspěchu | Geometrické |  
| Počet výskytů za čas | Poissonovo |  
| Výběr bez vracení | Hypergeometrické |  
  
---  
  
# Nejčastější chyby  
  
## Binomické vs Hypergeometrické  
  
Rozhodující otázka:  
  
> Vrací se prvky?  
  
- ANO → binomické  
- NE → hypergeometrické  
  
---  
  
# Důležité vzorce  
  
## Binomické rozdělení  
  
$$  
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}  
$$  
  
## Geometrické rozdělení  
  
$$  
P(X=k)=(1-p)^{k-1}p  
$$  
  
## Poissonovo rozdělení  
  
$$  
P(X=k)=\frac{\lambda^k e^{-\lambda}}{k!}  
$$
