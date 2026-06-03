![[Pasted image 20260601102040.png]]
```
%Matejův test

A = [35,141];

B = [52,149];

C = [62,189];

D = [113];

E = [145];

F = [16,174];

G = [];

H = [85];

I=[135];

%tady vlastně porucha nastala ve 35 takže 141 - 35 = 106 a pak že 200 -141

%= 59 do dobíhal

x = [35, 106, 59, 52, 97, 51, 62, 127, 11, 113, 87, 145, 55, 16, 158, 26, 200, 85, 115, 135, 65, 200];

cens = [0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 1];

[params, ci] = wblfit(x, 0.05, cens)

%H0:vyrobky nedegradují

%HA: vyrobky degradují

%Koukneme na interval ci_b a 1 v něm není takže zamítáme
```
Příklad 1: Na vesnické pouti je automat, kde je 500 mincí 1Kč, 500 mincí 2 Kč a 400 mincí 5 Kč, které jsou náhodně promíchány. Účastník hry zaplatí 100 Kč a automat zcela náhodně vyhodí 35 ks mincí, které hráč vyhraje 1) Určete pravděpodobnost, že hráč obdrží v mincích 120 Kč a více 2) určete pravdepodobnost pomoci presneho vypoctu, ze hrac vyhraje prave 172 nebo 175 Kč. 
```
%přiklad s mincemi

hodnoty = [1,2,5]

pravd = [500/1400,500/1400,400/1400]

mu_1 = sum(hodnoty.*pravd)

E_x2 = sum((hodnoty.^2).*pravd)

var_1 =E_x2-mu_1^2

%přepočítáme na jednu minci

n = 35

mu_celk =n*mu_1

sigma_celk = sqrt(n*var_1)

%Vypočet

p_vysledek = 1-normcdf(120,mu_celk,sigma_celk)

%b)Když zadání požaduje přesný výpočet konkrétní částky, musíme zjistit, jakými kombinacemi

%mincí ji lze složit, a použít kombinatorické číslo (nchoosek). Vytáhnout musíme přesně 35

%mincí.

%● Pro 175 Kč: Jediná možnost je vytáhnout všech 35 mincí pětikorun (35 ∙ 5 = 175).

%● Pro 172 Kč: Musíme mít 34 pětikorun a jednu dvoukorunu (34 ∙ 5 + 1 ∙ 2 = 172).

% Celkový počet všech možných výběrů 35 mincí z 1400

vsechny_moznosti = nchoosek(1400, 35);

% Možnosti pro 175 Kč (35 pětikorun ze 400 dostupných)

p_175 = nchoosek(400, 35) / vsechny_moznosti;

% Možnosti pro 172 Kč (34 pětikorun ze 400, 1 dvoukoruna z 500, 0

%jednokorun z 500)

p_172 = (nchoosek(400, 34) * nchoosek(500, 1) * nchoosek(500, 0))

vsechny_moznosti;

p_presna = p_175 + p_172
```
Zkoumali jsme zivotnost 20 ks shodných vyrobku a zaznamenali jsme nasledujici hodnoty
x = [110 340 520 590 670 850 1020 1050 1110 1190 1340 1420 1560 1710 1840 1950 2120 2910 3760 4490];

Předpokládejte, že doba do poruchy je popsána exponenciálním rozdělením.
1) Určete jeho parametry
2) Zjistěte pravděpodobnost, že výrobek přežije 1000 hodin provozu
3) Předpokládejte, ze systém je slozen ze 4 těchto identických vyrobku. Systém je provozuschopny, jestliže alespoň 3 z nich jsou v provozuschopnem stavu. Zjistete pravdepodobnost, ze systém bude provozuschopny v case 1000 hodin. Vyrobky v poruse nelze jednotlive vymenit.
```
x = [110 340 520 590 670 850 1020 1050 1110 1190 1340 1420 1560 1710 1840 1950 2120 2910 3760 4490];

muhat = expfit(x);

lambda = 1/muhat;

p = 1-expcdf(1000,muhat);

vysledek = 1 - binocdf(2,4,p);
```

Příklad 3:
Zkoumali jsme vliv rozpustnosti latky v 5 pripravenych roztocich v zavislosti na jeho teplote. Zjistili jsme nasledujici hodnoty.
                               10°C       15°C       20°C       25°C       30°C       35°C       40°C       50°C                     

                               0.084     0.087     0.087     0.091     0.093     0.094     0.096     0.097    

                               0.083     0.084     0.088     0.092     0.094     0.098     0.102     0.103    

                               0.087     0.085     0.083     0.086     0.089     0.092     0.094     0.097    

                               0.086     0.086     0.086     0.088     0.089     0.092     0.095     0.098    

                               0.087     0.089     0.091     0.093     0.094     0.095     0.096     0.097  

Otestujte na hladině významnosti 5%, zda existuje vliv teploty na rozpustnost látky. POkud ano, provedte naslednou analyzu. Prepokladejte normalitu dat. Otestujte predpokald shody rozptylu ve všech vyberech.

```
%příklad 3

x = [0.084,0.083,0.087,0.086,0.087,0.087,0.084,0.085,0.086,0.089,0.087,0.088,0.083,0.086,0.091,0.091,0.092,0.086,0.088,0.093,0.093,0.094,0.089,0.089,0.094,0.094,0.092,0.092,0.092,0.095,0.096,0.102,0.094,0.095,0.096,0.097,0.103,0.097,0.098,0.097]';

groups=[ones(5,1);2*ones(5,1);3*ones(5,1);4*ones(5,1);5*ones(5,1);6*ones(5,1);7*ones(5,1);8*ones(5,1)];

[p,anovatab,stats]= anova1(x,groups,"on");

[p,stats]= vartestn(x,groups,"Display","on","TestType","Bartlett");
```
Příklad 4:
Máte naměřeny následující data.
x=[5, 2, 4, 1, 3, 6, 7, 8, 9, 11, 13, 15, 17]
y=[179, 19, 100, 5, 48, 293, 448, 649, 901, 1587, 2554, 3849, 5522]

1) Učiňte proložení dat nelineární regresí modelem y = ax^4 + bx^3 + cx^2 + dx + e. Zjistěte, zda na hladině významnosti 5% všechny parametry jsou potřeba, pokud nikoli, příslušné parametry vylučte a zjednodušte model. Zduvodnete výsledky. 
2) Na hladině významnosti 5% otestujte u výsledného modelu, zda posunuti (konstanta) muze byt rovna 2.
3) Pro naměřená data zjistěte, zda je lepší model y = ax^3 + bx^2 nebo y = ae^(bx). Zdůvodněte.
```
x=[5, 2, 4, 1, 3, 6, 7, 8, 9, 11, 13, 15, 17];

y=[179, 19, 100, 5, 48, 293, 448, 649, 901, 1587, 2554, 3849, 5522];

%A)

modelfun=@(b,x)((b(1).*x.^4)+(b(2).*x.^3)+(b(3).*x.^2)+(b(4).*x)+b(5));

beta0=[1,1,1,1,1];

nlm = fitnlm(x,y,modelfun,beta0);

%jelikož u b(2) as b(3) a b(5)je pvalue < 0.05 tak zde jsou jedinné povinné zbytek

%může být 0

% vysledek pro a tedy y = 0.9953*x^3+2.1563*x^2+2.4682

%b)

int_b_min=2.4682-tinv(0.975,9)*0.85653;

int_a_min=2.4682+tinv(0.975,9)*0.85653;

%pval = 2*... oboustranný interval

%pval = 2* tcdf ... statistika jde na studentovo rozdělení

%pval = 2* tcdf((x-mu)/sigma,pocet stupnu volnosti)

pval=2*tcdf((2-2.4682)/0.85653,9);

%příjmáme jelikož pvalue je větší než 0.05

%c)

modlefun = @(b,x)(b(1).*x.^3+b(2).*x.^2);

beta0 =[1,1];

nlm = fitnlm(x,y,modlefun,beta0);

modlefun = @(b,x)(b(1).*exp(b(2).*x));

beta0 =[1,1];

nlm =fitnlm(x,y,modlefun,beta0);

%první je lepší jelikož R-Squared vyšlo 100% a druhého vyšlo 98.9%
```
Příklad 5:
10 lidi se rozhodlo, ze bude behat z Jablonce do Liberce a zaznamenávat si casy. První mereni provedli 1. ledna, druhy výsledek 1. února.

1. ledna: [84, 85, 92, 94, 97, 99, 102, 105, 110, 134]
2. února: [83, 84, 94, 95, 98, 101, 99, 102, 107, 129]

Ověřte na hladině významnosti 5%, že v unoru je cas behu u lidi nižší nez v lednu. Casy jsou uvedeny v minutach. Počasí v obou terminech bylo shodne beze snehu. Zamyslete se nad prepoklady pouziti testu, tedy pokud jsou. Uvedte hlavni výsledky a testovane hypotezy.

Otestujte na hladine vyznamnosti 5%, zda prumerny cas behu z JnN do Lb byla v ledn
```
leden= [84, 85, 92, 94, 97, 99, 102, 105, 110, 134];

unor= [83, 84, 94, 95, 98, 101, 99, 102, 107, 129];

%H0: časy v unoru jsou nižší než v lednu HA: časy v lednu jsou nižní než v

%únoru

%zde pro a použiju ttest;

c = leden -unor;

[h,p]= lillietest(c);

[h,p,ci,stats]= ttest(c,0,0.05,"right");

%Na hladině významnosti 5% H0 příjmame že časy jsou nižší v únoru než v

%lednu, pvalue, 0.1144 >0.05

%b)

%H0: stredniHodnota = 100 HA: stredniHodnota != 100

[h,p]= lillietest(leden)

[h,p,ci,stats ]=ttest(leden,100,0.05,"both")

%H0 příjmame na hladině významnosti 5%, pval = 0.9660
```
1. Máte data x, odstraňte odlehlé hodnoty (bez boxplot), jsou z norm. rozdělení? Jsou z norm. rozd. s mu=60, sigma=10? Vygenerujte 50 hodnot z rozdělení s mu=60, sigma=10, porovnejte, zda distribuční funkce je stejná s x. Může být směrodatná odchylka x rovna 20?, Data: x=[52,54,55,56,57,58,58,59,59,60,61,62,62,63,64,64,64,65,66,67,68,68,69,72,73,75,77,79,82,85,87,89,92,95,131,168,195]
```
x=[52,54,55,56,57,58,58,59,59,60,61,62,62,63,64,64,64,65,66,67,68,68,69,72,73,75,77,79,82,85,87,89,92,95,131,168,195];

n = length(x);

dolni = quantile(x,0.25)-1.5*iqr(x);

horni = quantile(x,0.75)+1.5*iqr(x);

n = length(x);

for i = n:-1:1

if x(i) < dolni || x(i) > horni

x(i) = [];

end

end

boxplot(x);

[h,p,kstat,cv] = lillietest(x,0.05,"norm")

%b)

a(:,1)=x';

a(:,2)=normcdf(a(:,1),60,10);

[h,p,ksstat,cv]= kstest(x,a);

%c

y = x'

data = normrnd(60,10,1,50)'

[h,p, stat]=kstest2(y,data)

%d

[h,p,stat]= vartest(x,400)
```

2. Máte 108 žolíkových karet, vytáhnu si 12, jaká je šance že mám 4 esa? Vytáhnu si 12, jaká je šance že mám pouze karty od 2 do 10?,
```
%pr2

hygepdf(4,108,4,12)

hygepdf(12,108,32,12)
```
3. 12 strojů se porouchalo v časech, 8 ne. Předpokládejte, že jsou z Weibullova rozdělení, zjistěte parametry. Může být beta rovná 2? Jsou data z exponenciálního rozdělení?, Data: T = [680, 720, 760, 790, 820, 850, 880, 920, 940, 960, 980, 990]

```
%př 3

T = [680, 720, 760, 790, 820, 850, 880, 920, 940, 960, 980, 990];

cens = [0,0,0,0,0,0,0,0,0,0,0,0];

[ci_a,ci_b] = wblfit(T,0.05,cens)

%ci_a =

%

% 901.4278 10.3780

%

%

%ci_b =

%

% 851.0942 6.5445

% 954.7381 16.4572

%b)v beta rozmezí není 2

%c) v beta neobsahuje 1 takže zamítám

%pr4
```

4. Pro převod z B do A se používá lin. regrese. Jaký jsou koeficienty? Může být b = 0? Může být a = 1.85?, Data: B = [148,175,312,354,387,412,423,454,485,521] A = [310,361,629,718,781,828,851,911,979,1052]
```
B = [148,175,312,354,387,412,423,454,485,521];

A = [310,361,629,718,781,828,851,911,979,1052];

vysl = fitlm(B,A)

%vysledek je y= 13.428x + 1.9847

%b nemůže být nula jelikož pval < 0.05

coefCI(vysl);

%ans =

%

% 5.8355 21.0207

% 1.9650 2.0044

%

% a =<5.8355,21.0207> A SE NEMŮŽE ROVNAT 1.85 NENÍ V INTERVALU

%B = <1.965,2.0044>
```
5. V roce 2024 jsme se zeptali 1234 lidi zda by volili stranu NE, 8.62 % volilo že ano, v roce 2025 jsme se zeptali na totéž 1141 lidí, 41 že ano. Je obliba strany stejná?
```
%pr5

n1 = 1234;

x1 = n1/100*8.62;

n2 =1141;

x2 =41;

p1 = x1/n1;

p2 = x2/n2;

T = (p1-p2) / sqrt((p1*(1-p1)/n1) + (p2*(1-p2)/n2));

pval = 2*min(normcdf(T,0,1), 1-normcdf(T,0,1))
```
![[Pasted image 20260601121031.png]]
![[Pasted image 20260601123256.png]]

```
%pr 3

x=[30,43,2,33,28,11,20,28,60,52,11,55,32,24,22,23,39,27,32,35,38,41,42,144,57,11,6];

f(:,1)=x';

f(:,2)=normcdf(x',10,10);

[h,p,ci,stat]= kstest(x,f);

%pvalue = 2.5364e-11 Na hladiněš významnosti zamítáme H0, že data pochází z

% normálního rozdělení N(mu=10,sigma^2=100)

[h,p]= lillietest(x);

[p,h,stat]= signtest(x,25)

%příjmáme H0 že median je roven 25
```

![[Pasted image 20260601131726.png]]

```
%př4

for i=0:5

hygepdf(i,40,5,5)

expected(i+1) = hygepdf(i, 40, 5, 5) * 520

end

%pr2

observed = [270, 192, 54, 3, 1, 0];

[h, p] = chi2gof(0:5, 'Ctrs', 0:5, 'Frequency', observed, 'Expected', expected)

%hypotézu příjmáme

p= hygepdf(5,40,5,5)

100/p

n = ceil(log(0.01) / log(1 - p))
```
![[Pasted image 20260601132522.png]]
```
%pr5

T20 = [28,32,35,37,41,42,44,45,46,48,51,52,54,56,58,62,65,68,72,76,82,85,98,121,154,187];%ano

T30 = [27,31,34,35,36,37,39,41,42,44,45,48,52,54,58,61,63,65,66,71,79,82,85,97,114,132,158];%ne

T40 = [25,28,31,32,35,39,42,44,48,49,51,52,53,55,59,62,65,66,72,79,85,91,97,112,134,165];%ano

T50 = [28,29,32,35,37,39,42,44,48,51,52,54,56,59,62,65,68,74,79,85,91,101,112,119,123];%ne

T60 = [14,17,19,21,22,24,25,27,29,32,34,37,38,41,42,43,46,47,48,51,52,54,55,56];%ano

[h,p] = lillietest(T20)

[h,p] = lillietest(T30)

[h,p] = lillietest(T40)

[h,p] = lillietest(T50)

[h,p] = lillietest(T60)

T = [T20,T30,T40,T50,T60];

G = [ones(1,length(T20)),2*ones(1,length(T30)),3*ones(1,length(T40)),4*ones(1,length(T50)),5*ones(1,length(T60))];

[p,anovat,stats]= kruskalwallis(T,G,"on")

multcompare(stats)
```



1)otestovat zda se prumern cas plavani zlepsil minimalne o 10 s otestuj na hladine vyznamnosti 5%
```
t1 = [86,94,98,112,118,121,10,98,90,178];

t2 = [74,83,91,100,102,117,92,88,86,142];

[h,p,stats] = lillietest(t1)

[h,p,stats]= lillietest(t2)

t3 = t2-t1;

[p,h]= signrank(t3,10,0.05,"tail","right")

%příjmáme hypotézu pvalue = 0.9639
```
![[Pasted image 20260601171201.png]]
P=2⋅21​⋅314​=314​≐0,129=12,9% 
% ta dvojka protože jsou 2 možnosti 

![[Pasted image 20260602175110.png]]
```
%% Příklad 3

freq = [0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1,1,2,2,2,2,2,2,2,3,3,3,3,4,4,5,8];

a=sum(freq)/length(freq);

sum2 = 2.5*a*2;

lambda = sum2;

1-poisscdf(5,lambda)

poissinv(0.999,5*lambda)
```

![[Pasted image 20260602175125.png]]
```
x1(1:292) = 1; % nad 50000 obyvatel (celkově 292)

x2(1:313) = 2; % 5000 - 50000 (celkově 313)

x3(1:395) = 3; % do 5000 obyvatel (celkově 395)

x = [x1, x2, x3];

y11(1:24) = 1;

y12(1:38) = 2;

y13(1:72) = 3;

y14(1:70) = 4;

y15(1:49) = 5;

y16(1:31) = 6;

y17(1:8) = 7;

y21(1:45) = 1;

y22(1:43) = 2;

y23(1:72) = 3;

y24(1:75) = 4;

y25(1:41) = 5;

y26(1:29) = 6;

y27(1:8) = 7;

y31(1:85) = 1;

y32(1:121) = 2;

y33(1:79) = 3;

y34(1:52) = 4;

y35(1:28) = 5;

y36(1:19) = 6;

y37(1:11) = 7;

y = [y11,y12,y13,y14,y15,y16,y17, y21,y22,y23,y24,y25,y26,y27, y31,y32,y33,y34,y35,y36,y37];

[tbl, chi2, p] = crosstab(x,y);
```
![[Pasted image 20260603170207.png]]

```
Tzacatek = [186,191,194,199,204,210,212,214,215,215,217,219,222,224,228,252,289,354];

Tnyni = [191, 189, 192, 197, 200, 208, 210, 206, 207, 204, 210, 212, 217, 221, 214, 240, 245, 289];

T = Tzacatek-Tnyni -5;

[h,p]=lillietest(T)

[p,h,stats]= signrank(T,0,"alpha",0.05,"tail","right")
```

![[Pasted image 20260603175229.png]]

```
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16];

y = [5, 25, 76, 170, 324, 550, 860, 1290, 1830, 2500, 3300, 4300, 5450, 6820, 8380, 10100];

modelfun=@(b,x)(b(1).*x.^4+b(2).*x.^3+b(3).*x.^2+b(4).*x+b(5));

beta0=[1,1,1,1,1];

nlm = fitnlm(x,y,modelfun,beta0)

ci = coefCI(nlm,0.05)

y_nove = modelfun(nlm.Coefficients.Estimate, [2.8, 4.2, 5.7])
```
