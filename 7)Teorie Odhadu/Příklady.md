| Situace                               | Funkce / přístup                                                  | Kdy použít                                             |
| ------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------ |
| Střední hodnota μ / x̄                |                                                                   |                                                        |
| Máš raw data, σ neznámá               | `ttest(x,[],'Alpha',a)`                                           | Nejčastější případ — σ se odhaduje z dat → t-rozdělení |
| Máš raw data, σ **známá předem**      | `ztest(x,[],sigma,'Alpha',a)`                                     | Vzácné — σ je dána výrobcem nebo normou                |
| Nemáš raw data (jen n, x̄, s)         | Ručně: `t = tinv(0.975, n-1)`  <br>`dolni = xbar - t*(s/sqrt(n))` | Když dostaneš jen průměr a odchylku, ne seznam čísel   |
| Velký výběr (n > 30), σ neznámá       | Ručně: `z = norminv(0.975)`  <br>`dolni = xbar - z*(s/sqrt(n))`   | t-rozdělení se blíží normálnímu, lze použít z          |
| Rozptyl / směrodatná odchylka σ² / s² |                                                                   |                                                        |
| Máš raw data                          | `vartest(x, sigma2, 'Alpha', a)`                                  | Testuje / odhaduje σ² pomocí χ²-rozdělení              |
| Nemáš raw data (jen n, s²)            | Ručně: `chi2inv(0.025, n-1)` a `chi2inv(0.975, n-1)`              | Vzorec: (n-1)s² / χ²                                   |
| Relativní četnost p                   |                                                                   |                                                        |
| Máš raw data (počty)                  | `binofit(pocet, n, alfa)`                                         | Přesnější metoda, když máš počty úspěchů               |
| Ručně (profesor preferuje)            | `p ± norminv(1-a/2) * sqrt(p*(1-p)/n)`                            | Vždy když profesor chce vzorec explicitně              |
| Medián M — data nejsou normální       |                                                                   |                                                        |
| Intervalový odhad mediánu             | Ručně: `median(x) ± 1.57*iqr(x)/sqrt(n)`                          | Když data nejsou z normálního rozdělení                |
| Znaménkový test mediánu               | `signtest(x, M0)`                                                 | Testuje jestli medián = M₀, bez předpokladu normality  |
| Dva výběry                            |                                                                   |                                                        |
| Shoda středních hodnot                | `ttest2(x, y)`                                                    | Dva **nezávislé** výběry                               |
| Párový test (stejné kusy)             | `ttest(x(1,:), x(2,:))`                                           | Měření **před/po** na stejných kusech                  |
| Shoda rozptylů                        | `vartest2(x, y)`                                                  | Vždy před ttest2 — zjisti jestli jsou rozptyly stejné  |
| Speciální rozdělení                   |                                                                   |                                                        |
| Exponenciální rozdělení               | `expfit(t, alfa, cens, freq)`                                     | Cenzorovaná data (ne všechny výrobky se pokazily)      |
| Weibullovo rozdělení                  | `wblfit(x, alfa)`                                                 | Data o poruchovosti s degradací                        |
![[Pasted image 20260529085547.png]]
```
%pr2

x=[0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1];

m = mean(x)

v = var(x)

s = std(x)

sk = skewness(x)

ku = kurtosis(x)

fprintf('Střední hodnota: %.4f\n', m)

fprintf('Rozptyl: %.4f\n', v)

fprintf('Sm. odchylka: %.4f\n', s)

fprintf('Šikmost: %.4f\n', sk)

fprintf('Špičatost: %.4f\n', ku)

% Co se stane po vynásobení 10?

x10 = x * 10;

fprintf('\n--- Po vynásobení 10 ---\n')

fprintf('Střední hodnota: %.4f\n', mean(x10))

fprintf('Rozptyl: %.4f\n', var(x10))

fprintf('Sm. odchylka: %.4f\n', std(x10))

fprintf('Šikmost: %.4f\n', skewness(x10))

fprintf('Špičatost: %.4f\n', kurtosis(x10))
```
![[Pasted image 20260529090812.png|437]]
```
%pr3

x = [987, 1001, 993, 994, 993, 1005, 1007, 999, 995, 1002];

%pak tady sledujeme ci rozmezí < a , b >

%pro minimalní je right, pro maximalní je left a pro strední je both

[h,p,ci,stats] = ttest(x,[],'Alpha',0.05)

[h,p,ci,stats] = ttest(x,[],0.1)

[h,p,ci,stats] = ttest(x,[],0.05,"right")
```
![[Pasted image 20260529092137.png]]
```
%pr4

n = 12

xbar = 44

s = 4

t = tinv(0.95,n-1)

dolni = xbar - t * (s / sqrt(n))

horni = xbar + t * (s / sqrt(n))
```
![[Pasted image 20260529092854.png]]
prostě vzorce
![[Pasted image 20260529100759.png]]

```
%pr7

z = norminv(0.975);

n = 80;

xbar = 12.01;

sigma = 0.04;

dolni = xbar - z * (sigma / sqrt(n))

horni = xbar + z * (sigma / sqrt(n))

%b

t = tinv(0.975,n-1)

dolni = xbar - t * (sigma / sqrt(n))

horni = xbar + t * (sigma / sqrt(n))
```
![[Pasted image 20260529094922.png]]
```
%pr8

x = [987, 1001, 993, 994, 993, 1005, 1007, 999, 995,1002];

%a

[h,p,ci,stats]= vartest(x,100,0.05,"both")

%b

[h,p,ci,stats]= vartest(x,100,0.05,"left")
```
![[Pasted image 20260529095617.png]]
Pozor tad yje zase hodně vzorců :((
![[Pasted image 20260529100728.png]]
```
%PR9

n = 100;

prumer = 150;

rozptyl = 16;

sigma = sqrt(rozptyl);

t =norminv(0.975)

dolni = prumer -t *(sigma /sqrt(n))

horni = prumer + t *(sigma /sqrt(n))

chiDolni = chi2inv(0.025,n-1)

chiHorni = chi2inv(0.975,n-1)

hornii = ((n-1)*sigma^2)/chiDolni

dolnii =((n-1)*sigma^2)/chiHorni
```
![[Pasted image 20260529100858.png]]
![[Pasted image 20260529105339.png|160]]
```
%pr 10

z = norminv(0.975);

p = 0.12;

n = 400;

dolni = p - z * sqrt((p*(1-p)/n));

horni = p + z * sqrt((p*(1-p)/n));

n2 = 1600

dolni = p - z * sqrt((p*(1-p)/n2));

horni = p + z * sqrt((p*(1-p)/n2));

%ňebo se dá taky takto

pocetUspechu = 12*4; %jelikož 1 % z 400 je 4 a procent bylo 12

[phat,pci]= binofit(192,1600,0.05)
```
![[Pasted image 20260529110518.png]]
![[Pasted image 20260529110751.png]]
```
z = norminv(0.975);

p=0.2;

sirka =0.02;

n = ceil((2 * z * sqrt(p*(1-p)) / sirka)^2)
```
![[Pasted image 20260529110942.png]]
```
x=[37,61,98,135,162,194,222,235,256,287,317,345,400,412,484,495,510,528,612,711,787,843,911,987,1014,1218,1512];

n = length(x)

dolni =median(x)-1.57*iqr(x)/sqrt(n)

horni =median(x)+1.57*iqr(x)/sqrt(n)
```
![[Pasted image 20260529111944.png]]![[Pasted image 20260529112551.png]]
```
%16a

Tporuch = [80,160,240,320,400,560,720,800,900,960] ;

t = [Tporuch,1000];

% cens 0 = porucha , cens 1 = cenzorováné , freq 1 = porucha , 40 jich

% došlo normalně

cens=[0,0,0,0,0,0,0,0,0,0,1];

freq=[1,1,1,1,1,1,1,1,1,1,40];

%par sřední hodnota , io intervalový odhad

[par, io] = expfit(t, 0.05, cens, freq)

%16b

x = importdata("P0716b.mat");

[par,ci] = wblfit(x,0.05)
```
![[Pasted image 20260529112648.png]]
![[Pasted image 20260529113112.png]]

```
%pr 17

x20=[3.96,4.03,4.07,4.12,4.16,4.18,4.20,4.22,4.23,4.24,4.24,4.25,4.29,4.32,4.35,4.38,4.41,4.44];

x50=[4.02,4.07,4.11,4.16,4.22,4.28,4.32,4.36,4.40,4.42,4.46,4.48,4.51,4.52,4.54,4.58,4.62,4.73];

[h,p,ci,stats]= vartest2(x20,x50,0.01)
```
![[Pasted image 20260529113055.png]]
![[Pasted image 20260529113153.png]]
```
%19

t1980=[243,251,257,257,259,261,263,265,284,293];

t2015=[191,193,193,195,195,195,197,198,199,202,202,203,204,205,207,208];

[h,p,ci,stats]= ttest2(t1980,t2015,0.01)
```
![[Pasted image 20260529113330.png]]

![[Pasted image 20260529114122.png]]
```
%pr21;

alfa = 0.05;

n1 = 800;

n2 = 600;

x1= 24;

x2=14;

p1 = x1/n1;

p2 = x2/n2;

p = (x1+x2)/(n1+n2)

Ci=(p1-p2)-sqrt(p*(1-p)*(1/n1+1/n2))*norminv((1-alfa/2),0,1)

ci2 = (p1-p2)+sqrt(p*(1-p)*(1/n1+1/n2))*norminv((1-alfa/2),0,1)D
```
![[Pasted image 20260529114158.png]]
```
alfa = 0.05;

n1 = 845;

n2 = 541;

x1= 60;

x2=57;

p1 = x1/n1;

p2 = x2/n2;

p = (x1+x2)/(n1+n2)

Ci=(p2-p1)-sqrt(p*(1-p)*(1/n1+1/n2))*norminv((1-alfa/2),0,1)

ci2 = (p2-p1)+sqrt(p*(1-p)*(1/n1+1/n2))*norminv((1-alfa/2),0,1)
```