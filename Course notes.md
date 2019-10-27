# Kryptering 3

## Sannolikhetsteori

### Beteckningar

Utfallsrum - $\Omega$ (en ändlig mängd).

Anta att $Pr:2^\Omega\to\R$ och $p:\Omega\to\R$ uppfyller $0\leq Pr(A)\leq1$ för $A\in2^\Omega$ och $0\leq p(\omega)\leq 1$ för alla $\omega\in\Omega$ samt $Pr(A)=\sum_{p\in\Omega}p(\omega)$ för alla $A\in\Omega$ samt $Pr(\Omega)=\sum_{\omega\in\Omega}p(\omega)=1$.

$(\Omega, Pr)$ är ett *diskret sannolikhetsrum*.

En delmängd $A\subseteq\Omega$ är en *händelse*.

Med $2^\Omega$ menas potensmängden för $\Omega$, d.v.s. mängden av alla delmängder till $\Omega$. Om $\Omega$ är $\Omega=\{1,2,3\}$ är $2^\Omega=\{\empty,\{1\},\{2\},\{3\},\{1,2\},\{1,3\},\{1,2\},\{2,3\},\{1,2,3\}\}$. 

$X$ kallas här en _stokastisk variabel_ (även _slumpvariabel_). Man kan inte förutsäga värdet - det är beroende på "slumpen". Man kan ha flera stokastiska variabel per utfallsrum.

Med $X(\omega)$ menas en funktion vars värde inte är känt utan beror på "slumpen".

Skrivsätten $X\leq x$ och $X=x$ motsvarar mängderna $\{\omega\in\Omega:X(\omega)\leq x\}$ respektive $\{\omega\in\Omega:X(\omega)=x\}$.

Vidare är $p_X(x)=Pr(X=x)$ och $Pr(X\leq x)=\sum_{y\leq x}p_X(y)$.

Med $A^c$ menas komplementet till mängden $A$.

Betingad sannolikhet tecknas $Pr(B|A)$.

### Sats

$$
\begin{align}
(a)\;& Pr(A)=1-Pr(A^c)\\
(b)\;& Pr(\empty)=0\\
(c)\;& Pr(A\cup B)=Pr(A)+Pr(B)-Pr(A\cap B)\\
(d)\;& A\cap B = \empty \Rightarrow Pr(A\cup B) = Pr(A) + Pr(B)\\
\end{align}
$$

### Betingad sannolikhet

Tecknas $Pr(B|A)$.

Om $Pr(A)>0$ (d.v.s $A≠\empty$) så är $Pr(B|A)=\frac{Pr(A\cap B)}{Pr(A)}$.

Sannolikheten att $B$ inträffar med förutsättningen att $A$ inträffat.

#### Bayes sats

$$
Pr(B|A)=\frac{Pr(A|B)Pr(B)}{Pr(A)}
$$

##### Bevis

$$
\begin{align}
Pr(B|A)=\frac{Pr(A|B)Pr(B)}{Pr(A)}\Rightarrow&\\
& Pr(B|A)Pr(A)=Pr(A\cap B) \\
& Pr(B|A)Pr(B)=Pr(B\cap A) \\
& Pr(B|A)Pr(A)=Pr(A|B)Pr(B)
\end{align}
$$

##### Exempel (Lotto)

$$
\Omega=\{1,2,...,35\}\\
A=\{1,2,...,7\}\\
B=\{2,4,...,34\}\\
$$


$$
\begin{align}
Pr(A\cap B)&=Pr(X\in\{2,4,6\})\\
&=\sum_{x\in\{2,4,6\}}p_X(x)\\
&=p(2)+p(4)+p(6)\\
&=\frac{1}{35}+\frac{1}{35}+\frac{1}{35}\\
&=\frac{3}{35}
\end{align}
$$

$$
Pr(B|A)=\frac{Pr(A\cap B)}{Pr(a)}=\frac{3/35}{7/35}=\frac{3}{7}\\
Pr(A|B)=\frac{Pr(A\cap B)}{Pr(B)}=\frac{3/35}{17/35}=\frac{3}{17}\\
\frac{Pr(A|B)Pr(B)}{Pr(A)}=\frac{(3/7)*(7/35)}{17/35}=\frac{3}{17}
$$


När man vet den ena betingade sannolikheten kan man alltså beräkna den andra via Bayes sats.

## Informationsteori

Claude E. Shannon publicerade en serie artiklar 1948 och 1949. Lade grunden för den moderna synen på kryptering.

### Beteckningar

$M$ är alla klartexter (så som alfabetet, alla möjliga block om åtta karaktärer).

Med $C$  menas alla kryptogram.

Alla nycklar betecknas med $K$.

$M$, $C$ och $K$ är stokastiska variabler som beskriver val av klartext, kryptogram och nyckel.

Vidare har vi en serie funktioner:
$$
p_M(m)=Pr(M=m)\\
p_C(c)=Pr(C=c)\\
p_K(k)=Pr(K=k)\\\;\\
e:K\times M\mapsto C\\
d:K\times C\mapsto M
$$
Om vi samlar $(M, C, K, e, d)$ får vi ett kryptosystem.

#### Exempel - monoalfabetiskt substitutionskrypto

Vi har det svenska alfabetet, $M=C=\{a,b,...,ö\}$. Då är mängden möjliga nycklar $K=\{\text{alla permutationer på }(a,b,...,ö)\}$. Sannolikheten att ett tecken dyker upp kan exempelvis ges av $p_M(a)=0.090,\;p_M(f)=0.019,\;p_M(x)=0.001$. För summan av alla dessa sannolikheter gäller $p_M(a)+p_M(b)+...+p_M(ö)=1$. Sannolikheten att en viss nyckel används bestäms av $p_K(k)=\frac{1}{29!}$.

### Perfekt sekretess

Ett kryptosystem har perfekt sekretess om $Pr(M=m|C=c)=Pr(M=m)$ för alla $m\in M$ samt alla $c\in C$. Klartexten är alltså oberoende av kryptogrammet. Det vill säga, kryptogrammet läcker ingen information om klartexten. Man kan slarvigt skriva $p(m|c)=p(m)$. 

Bayes sats ger att $p(m|c)p(c)=p(c|m)p(m)$. Genom att använda detta kan vi skriva
$$
p(m|c)=p(m)
\\\iff\\
\frac{p(c|m)p(m)}{p(c)}=p(m)
\\\iff\\
p(c|m)=p(c)
$$
Man kan således definiera perfekt sekretess som $p(c|m)=p(c)$ - att sannolikheten att vi har ett kryptogram för en klartext är densamma som sannolikheten för att vi har ett kryptogram.

Vidare är
$$
Pr(C=c|K=k)=Pr(M=d_k(c))
$$

$$
\begin{align}
p(c)&=\sum_{k\in K}Pr(C=c|K=k)Pr(K=k)\\
&=\sum_{k\in K}Pr(M=d_k(c))Pr(K=k)
\end{align}
$$



#### Exempel - monoalfabetiskt substitutionskrypto

Var god se föregående exempel för monoalfabetiskt substitutionskrypto.

Med ett val av nyckel gäller:
$$
Pr(C=a|K=k)=Pr(M=d_k(a)=f)=0.019
$$

#### Sats - Vernamchiffret

Vernamchiffret (one time pad, diplomatchiffret, blankettchiffret) har perfekt sekretess.

##### Bevis

Låt $M=\{0,1,...,n-1\}=C=K$. Krypteringsfunktionen $e(x)=x+k\;(mod\;n)$ och dekrypteringsfunktionen $d(x)=x-k\;(mod\;n)$.

För val av nyckel gäller $p(k)=\frac{1}{n}$. Det vill säga en likformig fördelning. 

Vi vill visa att $p(m|c)=p(m)\iff p(c|m)=p(c)$.

För varje kryptogram $c$ finns det en nyckel $k$ så att $m=d_k(c)$ för alla klartexter $m\in M$. Det vill säga $M=\{d_0(c),d_1(c),...,d_{n-1}(c)\}$. Det betyder att $M=d_k(c)$ och $M=d_{k'}(c)$ är oberoende då $k≠k'$. Det ger att $\sum_{k\in K}Pr(M=d_k(c))=1$ vilket i sin tur ger att $p(c)=\sum_{k\in K}Pr(M=dk(c))Pr(K=k)$.

Vi har nu
$$
\begin{align}
p(c)&=\sum_{k\in K}Pr(M=d_k(c))Pr(K=k)\\
&=\sum_{k\in K}Pr(M=d_k(c))\frac{1}{n}\\
&=\frac{1}{n}\sum_{k\in K}Pr(M=d_k(c))=\frac{1}{n}
\end{align}
$$
Frekvensanalys är alltså oanvändbart.

Vi har också att $p(c|m)=\frac{1}{n}$ eftersom för varje klartext $m$ finns det exakt en nyckel $k$ sådan att $c=e_k(m)$.

Det visar att $p(c)=\frac{1}{n}=p(c|m)$, vilket skulle visas.

#### Sats

Om ett kryptosystem har perfekt sekretess så är antal nycklar minst lika många som antalet möjliga klartexter, $|K|\geq |M|$. Om antalet nycklar är mindre än antal meddelande så har vi ej perfekt sekretess, $|K|\lt|M|$.

#### Lemma

Antag att $|M|=|C|=|K|$ och att kryptosystemet har perfekt sekretess. Låt $K_{m,c}=\{k\in K:e_k(m)=c\}$. Då gäller följande:
$$
\begin{align}
(a)\;& m≠n\Rightarrow K_{m,c}\cap K_{n,c}=\empty\\
(b)\;& |K_{m,c}|=1\;\forall\;m\in M\vee c\in C\\
\end{align}
$$

#### Sats

Antag att $|M|=|C|=|K|$ och att kryptosystemet har perfekt sekretess. Låt $K_{m,c}=\{k\in K:e_k(m)=c\}$. Då gäller följande:
$$
\begin{align}
(a)\;& p(k)=\frac{1}{|K|} \\
(b)\;& |{k\in K:c=e_k(m)}|=1\;\forall\;m\in M\vee c\in C\\
\end{align}
$$

### Entropi

Man kan ställa sig frågan "hur mycket information om klartexten eller nyckeln avslöjar ett kryptogram?".

$X$ är en stokastisk variabel (s.v.). Låt $x_1, x_2,...,x_n$ vara alla utfall för $X$. Vidare är $p_1,p_2,...,p_n$ sannolikheterna för $x_k$.

Entropin för $X$ ges av $H(X)=H(p_1,p_2,...,p_n)$ om funktionen uppfyller tre villkor.

1. $H$ ska vara kontinuerlig
2. $A(n)=H(\frac{1}{n},\frac{1}{n},...,\frac{1}{n})$ ska vara strängt växande
   * $A(2)=H(\frac{1}{2},\frac{1}{2})$
   * $A(3) = H(\frac{1}{3},\frac{1}{3},\frac{1}{3})$
3. $X$ är en stokastisk variabel som kan delas upp i $X_1$ och $X_2$ med sannolikheten $q_1$ respektive $q_2$. Då är $H(X)=q_1H(X_1)+q_2H(X_2)$
   * För $X$ gäller $\{a, b, c, d\}$ med $p_1=Pr(X=a)=\frac{1}{3}$, $p_2=\frac{1}{4}$, $p_3=\frac{1}{6}$, $p_4=\frac{1}{4}$
   * Om utfallen är $X_1:\{a,b,c\},d$ och $X_2:a,b,c$ är $q_1=1$ och $q_2=\frac{1}{3}+\frac{1}{4}+\frac{1}{6}=\frac{3}{4}$
   * $H(X)\underbrace{=}_\text{vill}H(\frac{1}{3},\frac{1}{4},\frac{1}{6},\frac{1}{4})=1*H(\frac{3}{4},\frac{1}{4})+\frac{3}{4}H(\frac{4}{9},\frac{1}{3},\frac{2}{9})$

![image-20190909161009612](/Users/alexgustafsson/Library/Application Support/typora-user-images/image-20190909161009612.png)

#### Lemma

Låt $r$ vara ett positivt heltal. Då är $A(n^r)=rA(n)$.

Jämför med $log(x^a)=a\log(x)$.

#### Sats

Det finns enbart en funktion som uppfyller alla tre krav för entropin ovan, nämligen:
$$
H(p_1,p_2,...,p_n)=-K\sum_{k=1}^{n}p_k*\log p_k\;K\geq0\;(K=1)
$$
Om $p_k = 0$ så antas $p_k * \log p_k=0$.

#### Bevis

Låt $m,n,s,t$ vara positiva heltal. Lemma ger $A(s^m)=mA(s)$ och $a(t^n)=nA(t)$. Antag att $s>1$ och $t>1$. Välj $m$ så att
$$
s^m\leq t^n \leq s^{m+1}\\
\iff\\
m\log s \leq n\log t \lt (m+1)\log s\\
\iff\\
\frac{m}{n}\leq\frac{\log t}{\log s}\leq \frac{m}{n}+\frac{1}{n}\\
\iff\\
0\leq\frac{\log t}{\log s}-\frac{m}{n}\lt \frac{1}{n}\\
$$
Sätt $\epsilon=\frac{2}{n}>0$. För stora $n$ är $\epsilon$ litet.
$$
\left|\frac{\log t}{\log s}-\frac{m}{n}\right|\lt\frac{\epsilon}{2}
$$
För kravet $A(n)$ är strängt växande får vi
$$
A(s^m)\leq A(t^n)\lt A(s^{m+1})\\
\iff\\
mA(s)\leq nA(t)\lt (m+1)A(s)\\
\iff\\
\frac{m}{n}\leq\frac{A(t)}{A(s)}\lt\frac{m}{n}+\frac{1}{n}\\
\iff\\
\left|\frac{A(t)}{A(s)}-\frac{m}{n}\right|
$$
Triangelolikheten $|x+y|\leq|x|+|y|$ ger oss
$$
\left|\frac{A(t)}{A(s)}-\frac{\log t}{\log s}\right|=\left|\frac{A(t)}{A(s)}-\frac{m}{n}+\frac{m}{n}-\frac{\log t}{\log s}\right|\\
\leq\\
\left|\frac{A(t)}{A(s)}-\frac{m}{n}\right|+\left|\frac{m}{n}-\frac{\log t}{\log s}\right|\\
\lt\\
\frac{\epsilon}{2}+\frac{\epsilon}{2}=\epsilon
$$
Parantes: eftersom $d$ ej beror på $n$ medan $\epsilon$ gör det och att vi kan göra $\epsilon$ hur litet som helst, måste $d=0$. Alltså är
$$
\frac{A(t)}{A(s)}=\frac{\log t}{\log s}
$$
Håll $s$ konstant och sätt $K=\frac{A(s)}{\log s}$. Då är
$$
\left|\frac{A(t)}{A(s)}-\frac{\log t}{\log s}\right|\lt\epsilon\\
\iff\\
\underbrace{\left|\frac{1}{A(s)}\right|}_{L}*\left|A(t)-\underbrace{\frac{A(s)}{\log s}}_{K}*\log t\right|\lt\epsilon\\
\iff\\
L\left|A(t)-K\log t\right|\lt\epsilon
$$
För stora $m$ är $\epsilon$ litet, men olikheten uppfyll ($t$ beror ej på $n$). Alltså är
$$
A(t)=K\log t
$$
Låt $X$ vara en stokastisk variabel med $n$ olika utfall med sannolikheterna $p_1$, $p_2$,...,$p_n$ där $p_i=\frac{m_i}{m}$ och $m=m_1+m_2+...+m_n$.

Låt $Y$ vara en stokastisk variabel för likformig sannolikhet bland de $m$ utfallen.
$$
H(Y)=H(p_1,p_2,...,p_n)+\sum_{i=1}^n p_iH(\frac{1}{m_i},\frac{1}{m_i},...,\frac{1}{m_i})\\
=H(x)+\sum_{i=1}^n p_iA(m_i)=H(x)+\sum_{i=1}^n p_i K \log m_i
$$
Det ger att
$$
\sum_{i=1}^n p_i K \log m = H(X)+\sum_{i=1}^n p_i K \log m_i\\
\iff\\
H(x)=\sum_{i=1}^n(p_i K \log m-p_i K \log m_i)\\
\iff\\
-\sum_{i=1}^n p_i K \log\frac{m_i}{m}\\
=-K\sum_{i=1}^n p_i\log p_i
$$

## Gitter

*Lattice* på engelska.

### Vektorrum

Låt $V$ vara en icke-tom mängd och definiera skalärmultiplikation och addition så att $au\in V$ och $u+v\in V$ där $a\in \mathbb{F}$ ($\mathbb{F}$ är en kropp) och $u,v\in V$. Om följande uppfylls för alla $u,v,w\in V$ och alla $a,b\in\mathbb{F}$, så får vi kalla $V$ för ett vektorrum. Det vill säga, kraven på ett vektorrum är följande:
$$
\begin{align}
(a)\quad&u+v=v+u\\
(b)\quad&u+(v+w)=(u+v)+w\\
(c)\quad&a(bu)=(ab)u\\
(d)\quad&1*u=u\\
(e)\quad&\exist\empty\in V: u+\empty=\empty+u=u\\
(f)\quad&(a+b)u=au+bu\\
(g)\quad&a(u+v)=au+av\\
(h)\quad&\forall u\in V \;\exists u'\in V : u+u' = u'+u = \empty\\
\end{align}
$$

#### Sats

$\empty\in V$ är entydigt bestämd.

##### Bevis

Antag att $\empty_1$ och $\empty_2$ upffyller $(e)$. Då är
$$
\empty_1=\empty_1+\empty_2=\empty_2
$$

#### Sats

* Varje vektorrum, utom nollrummet $\{\empty\}$  har en bas

* Varje bas till ett vektorrum har lika många vektorer

### Definitioner

Låt $v_1,v_2,...,v_m\in V$. Då är en *linjärkombination* $a_1v_1+a_2+v_2+...+a_mv_m$ där $a_1,a_2,...,a_m\in\mathbb{F}$.

*Linjärt oberoende* om $a_1v_1+...+a_mv_m=0$ endast har $a_1=a_2=...=a_m=0$ som lösning.

$v_1,v_2,...,v_m$ är en *bas* för $V$ om de är linjärt oberoende och om alla $v\in V$ kan skrivas som $v=a_1v_1+a_2v2+...+a_mv_m$.

Låt $u_1v\in V$. *Skalärprodukten* av $u$ och $v$ betecknas $\langle u, v \rangle$ som är en skalär, det vill säga tillhör $\mathbb{F}$. Följande ska vara uppfyllt:
$$
\begin{align}
(a)\quad& \langle u, u \rangle \in \mathbb{R}\\
(b)\quad& \langle u, u \rangle \geq 0, u=0 \iff \langle u, u \rangle = 0\\
(c)\quad& \langle u + v, w \rangle =\langle u, w \rangle + \langle v, w \rangle\\
(d)\quad& \langle au, v \rangle = a\langle u, v \rangle\\
(e) \quad& \langle u, v \rangle = \langle v, u \rangle
\end{align}
$$
Normalen, $||u||=\sqrt{\langle u, u, \rangle}=\sqrt{x_1^2+x_2^2+...+x_n^3}$. 

##### Exempel - skalärprodukt

$$
\langle u, v \rangle = \langle (x_1,x_2,...,x_n),(y_1,y_2,...,y_n)\rangle = \\
x_1y_1+x_2y_2+...+x_ny_n
$$

### Gitter

Låt $m\geq n $ och låt $v_1,v_2,...,v_n$ vara linjärt oberoende vektorer i $\mathbb{R}^m$.Då kallas följande mängd för ett *gitter*:
$$
\begin{align}
L&=L(v_1,v_2,...,v_n)\\
&=\{a_1v_1 + a_2v_2 + ... + a_nv_n : a_k\in \mathbb{Z}\}
\end{align}
$$

#### Exempel 

Vi kommer bara åt vissa punkter. Se bilden nedan.

Låt $v_1=(1,0)$ och $v_2=(2,1)$ i $\mathbb{R}^2$.

![image-20190911161224299](/Users/alexgustafsson/Library/Application Support/typora-user-images/image-20190911161224299.png)
$$
\begin{align}
L&=L(v_1,v_2)\\
&=\{a_1v_1+a_2v_2:a_1,a_2\in\mathbb{Z}\}\\
&=\{a_1(1,0)+a_2(2,1):a_1,a_2\in\mathbb{Z}\}\\
&=\{(a_1+2_a2,a_2):a_1,a_2\in\mathbb{Z}\}
\end{align}
$$
Även $w_1=(3,2)$ och $w_2=(1,1)$ är en bas för $L$ ty $w_1=-v_1+2v_2$ och $w_2=-v_1+v_2$ (samtidigt). Basbytesmatrisen ges då av
$$
A=\left(\begin{array}{cc}
-1&-1\\
2&1
\end{array}\right)
$$
Vidare är $det(A)=(-1)*1-2(-1)=1$.

Mängden $\mathcal{F}=\mathcal{F}(v_1,v_2,...,v_n)=\{t_1v_1+t_2v_2+...+t_nv_n:0\leq t_k \leq 1\}$ kallas för *fundamental parallellepipeden* för $L$ med avseende på $v_1,v_2,...,v_n$.

#### Sats

Sambandet mellan två baser för ett gitter ges av en basbytesmatris $A$ med heltalselement. Vidare gäller att determinanten $\det(A)=\pm 1$.

#### Sats

Låt $L$ vara ett gitter av dimension $n$ och $\mathcal{F}$ dess fundamentala parallelepiped. Då kan varje $w\in\mathbb{R}^n$ skrivas på formeln $w=t+v$ där $t\in\mathcal{F}$ och $v\in L$ på ett entydigt sätt.

### Klassiska problem med gitter

Det finns två problem som används för kryptering med gitter. Dessa är främst svåra att lösa i höga dimensioner.

#### Shortest Vector Problem (SVP)

Finn en vektor $v$ i $L\backslash\{\empty\}$ som minimerar $||v||$.

#### Closest Vector Problem (CVP)

Givet en vektor $w\in\mathbb{R}^m\backslash L$ finn den vektor $v\in L$ som minimerar $||v-w||$.

### Sats

Låt $v_i=(r_{i,1},r_{i,2},...,r_{i,n}), i=1,2,...,n$.
$$
F=\left(\begin{array}{cccc}
r_{1,1}&r_{1,1}&...&r_{1,n}\\
r_{2,1}&r_{1,1}&...&r_{1,n}\\
...&...&...&...\\
r_{n,1}&r_{n,1}&...&r_{n,n}\\
\end{array}\right)
$$
Vidare är volymen $\text{vol}\;\mathcal{F}=|\det F|$.

I två dimensioner är detta alltså samma sak som arean.

### Varianter på SVP och CVP

#### Shortest Basis Problem (SBP)

Finn en bas $v_1,v_2,...,v_n$ för $L$ så att $\max(||v_1||,||v_2||,...,||v_n||)$ eller $||v_1||+||v_2||+...+||v_n||$ är så liten som möjlig.

#### Approximate Shortest Vector Problem (apprSVP)

Minimera $v$ så att
$$
||v||\leq\psi(n) * ||v_\text{shortest}||,\;v\in L
$$
Med $v_\text{shortest}$ menas resultatet från SVP.

#### Approximate Closest Vector Problem (apprCVP)

Minimera $v$ så att
$$
||w-v||\leq\psi(n)||v_\text{closest}-w||
$$
med $v_\text{closest}$ menas resultatet från CVP.

### Sats (Hermitc)

Varje gitter $L$ med dimensionen $n$ innehåller en vektor $v≠0$ sådan att $||v||\leq\sqrt{n}(\det L)^{1/n}$ där $\det L$ är $\det (v_1\;v_2\;...\;v_n)$.

### Hadmard-förhållandet

_Hadmard-förhållandet_ för basen $B=(v_1,v_2,...,v_n)$ ges av $\mathcal{H}=\left(\frac{\det L}{||v_1||*||v_2||*...*||v_n||}\right)^{1/n}$.

#### Sats

$$
0\leq\mathcal{H}(B)\leq1
$$

Ju närmare $\mathcal{H}(B)$ är $1$ desto mer ortogonal är basen $B$.

### Topologi

Låt $S$ vara en delmängd till $\mathbb{R}^n$.

Om $||v||\lt r \;\forall\; v\in S, r\;\text{konstant}$ så säges $S$ vara *begränsad*.

Om $-v\in S$ då $v\in S$ så säges $S$ vara  _symmetrisk_.

Om varje vektor på linjesegmentet mellan $u$ och $v$ där $u,v\in S$ också tillhör $S$ så säges $S$ vara _konvex_.

Låt $c\in S$ och $r\gt 0$. Den _slutna bollen med centrum i $c$ och radien $r$_ ges av $B_r(c)=\{v\in\mathbb{R}^n:||c-v||\leq r\}$. 

$S$ är _sluten_ om det för varje $c\in \mathbb{R}^n$ gäller att om $B_r(c)\cap S≠\empty$ för alla $r\gt 0$, så $c\in S$.

### Minkowskis sats

$L$ är ett gitter av dimension $n$. $S\subset \mathbb{R}^n$ där $S$ är symmetriskt som uppfyller
$$
\text{vol}(S)\gt 2^n\det L
$$
då finns det $v\in L\backslash\{0\}$ som tillhör $S$.

### Babais algoritm

#### SVP

Låt $v=a_1v_1+a_2v_2+...+a_nv_n$ vara våra basvektorer. Vi vill minimera $||v||$ där $v≠0$. Om basen ä4 ortogonal, dvs. $<v_i,v_j>=0$ då $i≠j$. Då är
$$
\begin{align}
||v||^2=<v,v>\\
&=<a_1v_1+...+a_nv_n,a_1v_1+...a_nv_n>\\
&=<a_1<v_1,a_1v_1+...+a_nv_n> \\
&+<a2_v2+...+a_nv_n,a_1v_1+...+a_nv_n>\\
&=...\\
&=a_1^2<v_1,v_1>+...+a_n^2<v_n,v_n>\\
&=a_1^2||v_1||^2+a_2^2||v_2||^2+...+a_n^2||v_n||^2
\end{align}
$$
Om $v_k$ är den kortaste basvektorn sätter vi $a_k=1$ och övriga $a_i=0$.

Låt $x\in\mathbb{R}$. Då betecknar $\lfloor{x}\rceil$ det närmaste heltalet till $x$. Exempelvis är $\lfloor 1.2 \rceil=1$, $\lfloor 3.5 \rceil=4$.

#### Algoritm

Låt $L=L(v_1,v_2,...,v_n$) vara gitter $w\in\mathbb{R}^n\backslash L$. Om $B=(v_1,v_2,...;v_n)$ är tillräckligt ortogonal så löser följande algoritm CVP.

1. Bestäm $t_1,t_2,...,t_n\in\mathbb{R}$ så att $w=t_1v_1+t_2v_2+...+t_nv_n$
2. Sätt $a_i\leftarrow\lfloor t_i\rceil$ där $i=1,2,...,n$
3. Returnera $v=a_1v_1+a_2v_2+...+a_nv_n$

##### Exempel

$$
v_1=(2,1),v_2=(-1,3)\\
\det L=\det\left(\begin{array}{c c}2&1\\-1&3\end{array}\right)=7\\
||v_1||=\sqrt{5}\\
||v_2||=\sqrt{10}\\
\mathcal{H}(B)=\left(\frac{\det L}{||v_1||*||v_2||}\right)^{1/2}=\sqrt{\frac{7}{5\sqrt{2}}}≈0.9949
$$

Vi ser att $B$ är väldigt nära att vara ortogonal.
$$
w=(17,21)=t_1v_1+t_2v_2=\frac{72}{2}v_1+\frac{25}{7}v_2\notin L\\
a_1=\lfloor t_1\rceil=10\\
a_2=\lfloor t_2\rceil=4
$$
Närmsta vektorn i $L$ till $w$ är
$$
v=a_1v_1+a_2v_2=10(2,1)+4(-1,3)=(16,22)
$$

## GGH

Ett asymmetriskt kryptosystem från 1997 av Oded Goldreich, Shafi Goldwasser, Shai Halevi.

Går att knäcka. Kryptogrammet läcker information om klartexten.

### Nyckelkonstruktion

Låt $n$ vara ett positivt heltal. Därefter välj $n$ linjärt oberoende vektorer $v_1, v_2,...,v_n\in\mathbb{Z}^n$ och $\mathcal{H}(v_1,v_2,...,v_n)$ nära $1$. Välj sedan en $n\times n$-matris  $U=(u_{i,j})$ med heltalselement och sådan att $\det U=\pm 1$.
$$
V=\left(\begin{array}{c}v_1\\v_2\\\vdots\\v_n\end{array}\right), W=UV
$$
Notera att om
$$
W=V=\left(\begin{array}{c}w_1\\w_2\\\vdots\\w_n\end{array}\right)
$$
så är
$$
\left\{
\begin{array}
ww_1&=u_{1,1}v_1+u_{1,2}v_2+...+u_{1,n}v_n\\
w_2&=u_{2,1}v_1+u_{2,2}v_2+...+u_{2,n}v_n\\
\vdots\\
w_n&=u_{n,1}v_1+u_{n,2}v_2+...+u_{n,n}v_n
\end{array}\right.
$$
Vi har att $L(v_1,v_2,...,v_n)=L(w_1,w_2,...,2_n)$ och kravet $\mathcal{H}(w_1,w_2,...,w_n)$ ska vara nära $0$.

**Publik nyckel**: $w_1,w_2,...,w_n$

**Privat nyckel**: $v_1,v_2,...,v_n$

### Kryptering

Ett meddelande kodas som en vektor
$$
m=(m_1,m_2,...,m_n)\in\mathbb{Z}^n
$$
så att $||m||\leq N$. Välj en efemär nyckel $r\in\mathbb{Z}^n\setminus L$.

Kryptogrammet $e\in\mathbb{Z}^n$ ges av
$$
e=mW+r
$$
Notera att $mW$ finns i gittret men att $mW+r$ lämnar gittret. Kan ses som en störning. Eve behöver lösa ett CVP.

### Dektryptering

Bestäm $t_1,t_2,...,t_n$ så att $e=t_1v_1+t_2v_2+...+t_nv_n$. Notera att talen ej kommer att vara heltal. Därför kan vi utnyttja Babais algoritm för att få $v=\lfloor t_1 \rceil v_1+\lfloor t_2 \rceil v_2+...+\lfloor t_n \rceil v_n$. Det ger att $v=mW$, vi har alltså "trollat bort" störningen $r$ och vi är nu återigen inom gittret. Vi har löst CVP. Klartexten kan nu fås med $m=vW^{-1}$.

### Exempel (3D)

**Nyckelkonstruktion**
$$
v_1=(5, 1, -3)\\
v_2=(1,-2,6)\\
v_3=(-3,7,1)\\
\mathcal{H}(v_1,v_2,v_3)≈0.94\\
V=\left(
\begin{array}{c c c}
5&1&-3\\
1&-2&6\\
-3&7&1
\end{array}
\right)\\
U=\left(
\begin{array}{c c c}
42&9&52\\
45&-5&63\\
-1&66&102
\end{array}
\right)\\
\det U=1\\
W=UV=\left(
\begin{array}{c c c}
45&424&-128\\
31&496&-102\\
-245&581&501
\end{array}
\right)\\
\mathcal{H}(w_1,w_2,w_3)≈0.01
$$
**Kryptering**
$$
m=(17, 3, 11)\\
r=(2,-1,1)\\
e=mW+r=(-1835,15086,3030)
$$
**Dekryptering**
$$
e=\frac{101432}{121}v_1+\frac{67557}{121}v_2+\frac{24144}{11}v_3\\
\lfloor\odot\rceil\Rightarrow\\
v=838v_1+558v_2+2195v_3\\
vW^{-1}=(838\;558\;2195)\frac{1}{242}\left(
\begin{array}{c c c}
-307758&286792&...\\
\vdots&\ddots&...\\
...&...&-9176
\end{array}
\right)=(17,3,11)\\
$$
Om Eve gör samma sak fast då $v\leftarrow w$ får hon
$$
e=a_1w_1+a_2w_2+a_3w_3\\
v=(-1746,14216,285...)\\
m'=(-3064,2874,-192)
$$
Detta då Eve får en "dålig bas".

## Polynomringar

Exempel på ringar $\mathbb{Z}$, $\mathbb{Z_m}$, där $m$ är sammansatt.

Typiskt för ringar: division fungerar inte alltid.

Låt $R$ vara en ring. Då betecknar $R[x]$ mängden av alla polynom med koefficienter ur $R$.

**Sats**: $R[X]$ är en ring.

### Divisionsalgoritmen

 Om $f(x)-g(x)=m(x)n(x)$ för något polynom $n(x)$, då skriver vi att $f(x)\equiv g(x)\mod m(x)$.

Låt $N$ vara ett positivt heltal och sätt
$$
\begin{align}
R&=\mathbb{Z}[x]\not(x^N-1)\\
&=\{a_{N-1}x^{N-1}+...+a_{N-2}x^{N-2}+a_{N-1}x+a_0:a_k\in\mathbb{Z}\}
\end{align}
$$
Det vill säga alla möjliga rester vi kan få när vi delar med $(x^N-1)$.

### Faltning

Låt $f,g\in R$. Det vill säga $f(x)=\sum_{i=0}^{N-1}a_ix^i$ och $g(x)=\sum_{i=0}^{N-1}b_ix^i$. Då motsvaras $fg$ av faltningen $f(x)*g(x)=(f*g)(x)=\sum_{k=0}^{N-1}c_kx^i$ där $. c_k=\sum_{i+j\equiv k\mod N}a_ib_j$. Notera att "stjärnan" skrivs som just det.

### Exempel

Låt $N=4$, $f(x)=a_3x^3+a_2x^2+a_1x+a_0$ och $g(x)=b_3x^3+b_2x^2+b_1x+b_0$.
$$
f(x)*g(x)=c_3x^3+c_2x^2+c_1x+x_0\\
c_0=a_0b_0+a_1b_3+a2_b2+a_3b_1\\
c_1=a_0b_1+a_1b_0+a_2b_3+a_3b_2\\
c_2=a_0b_2+a_1b_1+a_2b_0+a_3b_3\\
c_3=a_0b_3+a_1b_2+a_2b_1+a_3b_0
$$

### Reducering

Låt $q$ vara ett heltal större än $1$. Sätt $R_q=\mathbb{Z}_q[x]\not(x^N-1)$.

Låt $f(x)=\sum_{i=0}^{N-1}a_ix^i\in R$.

Sätt $a_i'\equiv a_i\mod q$ så att $a_i'\in\mathbb{Z}_q$ och sätt $f_q(x)=\sum_{i=0}^{N-1}a_i'x^i$ (reducering).

### Centrerad lyftning

Givet $f_q(x)=\overline{a}_{N-1}x^{N-1}+...+\overline{a}_2x^2+\overline{a}_1x+\overline{a}_0\in R_q$. Vi vill bestämma $f\in R$ så att $f$ reducerar $fq$ (alltid samma $f$ för aktuellt $fq$).

Sätt $a_k\equiv\overline{a}_k\mod q$ där $\frac{-q}{2}\lt a_k\leq \frac{q}{2}$.

#### Exempel

$$
f_{11}(x)=9x^4+7x^2+x+5\\
f(x)=-2x^4-4x^2+x+5
$$

## NTRU

1996, Hoffstein, Pipher, Silverman.

**N**-th degree **trun**cated polynmoial ring.

Låt $N$ vara ett heltal större än $1$. Låt $d_1$ och $d_2$ vara icke-negativa heltal. $\tau(d_1,d_2)$ är mängden av alla polynom ur $R$ så att exakt $d_1$ stycken av koefficienterna är $1$ och exakt $d_2$ stycken är $-1$ samt resten $0$.

**Exempel**: $x^5-x^4+x^2-x+1\in\tau(3,2)$.

### Nyckelkonstruktion

Välj $N$ och $p$ primtal samt ett positiva heltal $q$ och $d$ så att $\gcd(N,p)=1$ och $\gcd(p,q)=1$ och $q>(6d+1)p$. Välj $f(x)\in\tau(d+1, d)$ och $g(x)\in\tau(d, d)$.

Reduktion: $f_p(x)$ och $f_q(x)$.

Sätt $h_q(x)=f_q^{-1}(x)*g_q(x)$ där $f_q(x)*f_q^{-1}=1$ ty $f$ måste väljas så.

Publika parametrar: $N$, $p$ och $q$. Publik nyckel: $h_q$. Privat nyckel är $f$ och $g$.

### Kryptering

Välj en klartext som kodas som ett polynom $m_p(x)\in R_p$.

Centrerad lyftning $m(x)=\text{centrerad lyftning}(m_p(x))$.

Välj en (slumpmässig) efemär nyckel $r(x)\in\tau(d,d)$.

Kryptogrammet ges av $e(x)=ph_q(x)*r(x)+m(x)$ (reduktion). Notera att $*$ är faltning.

### Dekryptering

Bestäm polynomet $\overline{a}(x)=f_q(x)*e(x)$ i $R_q$ där $*$ innebär faltning. Gör en lyftning $a(x)=\text{centrerad lyftning}(\overline{a}(x))$. Bestäm $b(x)=f_p^{-1}(x)*a(x)$ i $R_p$.

Meddelandet ges av $m_p(x)=b(x)$.

Samtliga $*$ innebär här faltning.

### Exempel

$$
N=7,\;p=5,\;q=71,\;d=2\\
f(x)=x^6+x^5-x^3-x+1\in\tau(3,2)\\
g(x)=x^4-x^3+x-1\in\tau(2,2)\\
f^{-1}_5,\;f^{-1}_{71}\;\text{existerar}\\
f_5^{-1}(x)=x^4+3x^3+4x^2+3x\\
f_{71}^{-1}(x)=46x^6+50x^5+43x^4-56x^3+30x^2+12x+48\\
h_{71}(x)=f^{-1}_{71}*g_{71}(x)=49x^6+46x^5+49x^4+43x^3+57x^2+29x+11\\
m_5(x)=4x^5+2x^4+2x^3+3x+3\\
m(x)=\text{central lyftning}(m_5(x))=-x^5+2x^4+2x^3-2x-2\\
r(x)=x^6-x^3+x^2-1\\
e(x)=53x^6+15x^5+56x^4+51x^3+24x^2+11x+2
$$

## NTRU som ett gitter

Vi har en publik nyckeln $h(x)=h_0+h_1x+h_2x^2+...+h_{N-1}x^{N-1}$ och en privat nyckel $f\in\tau(d+1,d)$.

Representation som vektor: $\overline{h}=(h_0,h_1,h2,...,h_{N-1})\in\mathbb{Z}^N$.

Rotation: $x^1*h(x)=h_{N-1}+h{N-i+1}_x+...+h_{N-i-1}x^{N-1}$ där $*$ är faltning.  Exempel då $i=1$: $x*h(x)=h_{N-1}+h_0x+h_1x^2+h_2x^3h_+...+h_{N-2}x^{N-1}$.

Vi bildar följande matris:
$$
H=\left(\begin{array}{c}
h\\
x*h\\
x^2*h\\
\vdots\\
x^{N-1}*h
\end{array}\right)
=\left(\begin{array}{ccccc}
h0 & h_1 & h_2 & ... & h_{N-1}\\
h_{N-1} & h_0 & h_1 & ... & h_{N-2}\\
h_{N-2} & h_{N-1} & h_0 & ... & h_{N-3}\\&&
\vdots\\
h_1 & h_2 & h_3 & ... &h_0
\end{array}\right)
$$
Sätt $\overline{f}=(f_0,f_1,...,f_{N-1})$ och $\overline{g}=(g_0,g_1,...,g_{N-1})$.

Notera: På labben när vi "knäcker" NTRU kan det vara så att vi måste utföra en rotation för att få fram rätt. Man kan få fram olika kandidater där inte alla fungerar, så man bör därför testa mot klartexten.

Vidare sätt
$$
M_h^{\text{NTRU}}=\left(\begin{array}{cc}
I & H\\
0 & qI
\end{array}\right)=
\left(\begin{array}{cccccccc}
1 & 0 & 0 & ... & 0 & h_0 & h_1 & h_2 & ... & h_{N-1}\\
0 & 1 & 0 & ... & 0 & h_{N-1} & h_0 & h_1 & ... & h_{N-2}\\
0 & 0 & 1 & ... & 0 & h_{N-2} & h_{N-1} & h_0 & ... & h_{N-3}\\
&&&&&...&...\\
0 & 0 & 0 & ... & 1 & h_1 & h_2 & h_3 & ... & h_0\\
0 & 0 & 0 & ... & 0 & q & 0 & 0 & ... & 0\\
0 & 0 & 0 & ... & 0 & 0 & q & 0 & ... & 0\\
0 & 0 & 0 & ... & 0 & 0 & 0 & q & ... & 0\\
&&&&&...&...\\
0 & 0 & 0 & ... & 0 & 0 & 0 & 0 & ... & q\\
\end{array}\right)
$$
Vidare har vi att $\det M_h^{\text{NTRU}}q^N=q≠0$. Det vill säga att raderna i matrisen är linjärt oberoende. Vi kan alltså använda raderna för att generera ett gitter som är kopplat till detta krypto.

Låt $L_h^{\text{NTRU}}$ vara det gitter som genereras av raderna i $M_h^\text{NTRU}$.

Låt $\overline{u}=(u_1,u_2,...,u_N)$ och $\overline{v}=(v_1,v_2,...,v_N)$. Med skrivsättet $(\overline{u},\overline{v})$ så menas vektorn $u_1,u_2,...,u_N,v-1,v_2,...,v_N)\in\mathbb{Z}^2{}$.

### Sats

Låt $f,g,h\in R_q=\mathbb{q}[x]\not(x^N-1)$. Antag att $f(x)*h(x)\equiv g(x)\mod q$. Då gäller att $(\overline{f},-\overline{u})M_h^\text{NTRU}=(\overline{f},g)$ där $f(x)*h(x)=g(x)+qu(x)$. Alltså gäller $(\overline{f},\overline{g})\in L_h^\text{NTRU}$.

Det vill säga det finns i gittret.

## Gram-Schmidts ortogonaliseringsprocess (GSop)

Givet $v_1,v_2,...,v_n$ linjärt oberoende vektorer, men ej parvist ortogonala så vill vi bestämma $w_1,w_2,...,w_n$ som är linjärt oberoende och parvis ortogonala så att $v_1$ och $w_1$ spänner upp samma underum. Detsamma gäller för $v_1,v_2$ och $w_1,w_2$, $v_1,v_2,v_3$ och $w_1,w_2,w_3$ o.s.v.

### Algoritm

$$
\begin{align}
w_1\leftarrow v_1&\\
\forall i\in\{2,3,...,n\}:&\\
&\mu_{i,j}\leftarrow\frac{<v_i,w_j>}{||w_j||^2},\;j=1,2,...,i-1\\
&w_i\leftarrow v_i-\mu_{i,1}w_1-\mu_{i,2}w_2-...-\mu_{i,i-1}w_{i-1}
\end{align}
$$



## Lenstra-Lenstra-Lovász-algoritmen (LLL)

Låt $B=(v_1,v_2,...,v_n)$ vara en bas som genererar ett gitter $L$ och låt $B^*=(w_1,w_2,...,w_n)$ vara motsvarande bas efter att vi applicerat GSop.

Man säger att $B$ är _LLL-reducerad_ om radvektorerna i $B$ uppfyller följande två olikheter: $|\mu_{i,j}|\leq\frac{1}{2}$ och $||w_i||^2\geq (\frac{3}{4}-\mu_{i,i-1}^2)||w_{i-1}||^2$ för alla $i$ och $j$. Den sistnämnda kallas Lovász olikhet.

En LLL-reducerad bas är en bra bas, det vill säga $\mathcal{H}(B)$ är nära $1$.

### Algoritm

Givet $B=(v_1,v_2,...,v_n)$ bas för $L$.

1. $k\leftarrow 2$
2. för $j=k-1,...,2,1$
   1. $v_k\leftarrow v_k-\lfloor\mu_{k,j}\rceil v_j$
3. om $||w_k||^2\geq(\frac{3}{4}-\mu_{k,k-1}^2)||w_{k-1}||^2$
   1. $k\leftarrow k+1$ och gå till steg 5
4. Byt plats på vektorerna $v_{k-1}$ och $v_k$ och sätt $k\leftarrow\max(k-1,2)$
5. Avbryt om $k>n$, annars gå till steg 2

Så fort någon vektor $v_k$ ändras måste de $\mu_{i,j}$ och $w_j$ som berörs bestämmas på nytt med GSop.

## Linjär kryptoanalys

Används för att analysera symmetriska krypton. Känd klartext-attack. Togs fram av Mitsuru och Matsui 1993.

Med $\oplus$ menas vidare addition i $\mathbb{Z}_2$.

Indata: $x=(x_1,x_2,...),\;x_i\in\mathbb{Z}_2$. Utdata: $y=(y_1,y_2,...),\;y_i\in\mathbb{Z}_2$.

Vi vill hitta någon form av linjärapproximation $x_{i1}\oplus x_{i2}\oplus ... \oplus x_{ir}\oplus y_{i1} \oplus ... \oplus y_{js}=0$ som är vanlig eller ovanlig. Fallet $0=0$ anses trivialt och ointressant. Vi vill med detta knäcka bitar i nyckeln.

Låt $p$ beteckna sannolikheten att linjärapproximationen är uppfylld. Det *linjära sannolikhetsfelet* alt. *bias* $\epsilon$ ges av $\epsilon=p-\frac{1}{2}$. Vi vill att $|\epsilon|$ är stort. Notera att $-\frac{1}{2}\leq\epsilon\leq\frac{1}{2}$. Desto närmre bias är $0$ desto större är sannolikheten att linjärapproximationen är normalfördelat.

Till en början studerar vi två bitar, $x_1$ och $x_2$. Sannolikheten $Pr(x_i=x)=\left\{\begin{array} p_i\;x=0\\1-p_i\;x=1\end{array}\right.$

Från
$$
x_1\oplus x_2=0\iff x_1=x_2\\
x_1\oplus x_2=1\iff x_1≠x_2
$$
följer att
$$
Pr(x_1=a\and x_2=b)=\left\{\begin{array}{lr}
p_1p_2&a=0,b=0\\
(1-p_1)p_2&a=1,b=0\\
p_1(1-p_2)&a=0,b=1\\
(1-p_1)(1-p_2)&a=1,b=1
\end{array}\right.
$$
Det ger att 
$$
\begin{align}
p_{1,2}&=\\
&=Pr(x_1\oplus x_2=0)\\
&=Pr(x_1=x_2)\\
&=Pr(x_1=0\and x_2=0)+Pr(x_1=1\and x_2=1)\\
&=p_1p_2=(1-p_1)(1-p_2)
\end{align}
$$
Sätt $\epsilon_i=p_i-\frac{1}{2}$:
$$
\begin{array}
p_{1,2}&=\\
&=(\epsilon_1+\frac{1}{2})(\epsilon_2+\frac{1}{2})+(1-(\epsilon_1+\frac{1}{2}))(1-(\epsilon_2+\frac{1}{2}))\\
&=\frac{1}{2}+2\epsilon_1\epsilon_2\\
&=\epsilon_{1,2}+\frac{1}{2}\\
\end{array}
\\
\Rightarrow
\epsilon_{1,2}=2\epsilon_1\epsilon_2
$$

### Matsuis anhopningslemma

Om $x_i=0$ är oberoende för alla $i=1,2,...,n$ så är $p_{1,2,...,n}=Pr(x_1\oplus x_2\oplus .... \oplus x_n=0)=\frac{1}{2}+2\epsilon_1\epsilon_2*...*\epsilon_n$ och $\epsilon_{1,2,...,n}=2\epsilon_1\epsilon_2*...*\epsilon_n$.

## Kodningsteori

### Blockkoder

$A$ = alfabet. Låt $n$ och $k$ vara positiva heltal. Alice vill sända $x\in A^k$ ($x$ kallas för ett *ord*) till Bob. 

Hon använder en *kodningsavbildning* $E:A^k\rightarrow A^n$ och skickar $y=E(x)$, som kallas *kodord*. Bob använder *avkodningsavbildningen* $D:A^n\rightarrow A^k$, där $D(E(x))=x\forall x\in A^k$.

### Hammingmetrik

Låt $x,y\in A^n$ och $d(x,y)$ som ges av antal positioner där $x$ och $y$ skiljer sig åt. Exempelvis blir $d(001, 101)=1$. Detta kallas för Hammingavstånd eller Hammingmetrik.

Notera att $d(x, y)\geq 0$ kan skrivas som $d(x,y)=0\iff x=y$.

Vidare är $d(x,y)=d(y,x)$ och $d(x,y)\leq d(x,z)+d(y,z)$ (triangelolikheten).

Klotet med medelpunkt i $x$ och radien $r$ ges av $B_r(x)=\{y\in A^n : d(x, y)\leq r \}$.

Låt $C\subseteq A^n$ vara en kod. Man säger att $C$ kan upptäcka upp till $s$ fel om det för varje $c\in C$ gäller att $B_s$ endast innehåller ett kodord.

En kod $C$ säges kunna korrigera upp till $t$ fel om det för varje $x\in A^n$ gäller att $B_t(x)$ innehåller högst ett kodord.

Minimalavståndet definieras som $d(C)=\min(\{d(x,y):x,y\in C\and x≠y\})$. Om minimalavståndet $d(C)\geq s+1$ så kan $C$ upptäcka $s$ fel. Om $d(c)\geq 2t+1$ så kan $C$ rätta $t$ fel.

#### Exempel

$B_1(10011)=\{10011, 00011, 11011, 10111, 10001, 10010\}$.

### Linjära koder

Låt $q=p^f$ där $p$ är ett primtal och $f$ ett positivt heltal. Låt $\mathbb{F}_q$ vara den ändliga kroppen med $q$ element.
$$
\mathbb{F}_q^n=\{(v_1,v_2,...,v_n):v_i\in\mathbb{F}_q\}
$$
Låt $\overline{v}_1,\overline{v}_2,...,\overline{v}_k$ vara linjärt oberoende, d.v.s. $\lambda_1\overline{v}_1+\lambda_2\overline{v}_2+...+\lambda_k\overline{v}_k=\overline{0}$ har endast lösningen $\lambda_1=\lambda_2=...=\lambda_k=0$ då $k<n$.

Bilda
$$
C=\{a_1\overline{v}_1+a_2\overline{v}_2+...+a_k\overline{v}_k : a_i\in \mathbb{F}_q\}
$$
Om $a\in\mathbb{F}_q$ och $\overline{x},\overline{y}\in C$ så är $a\overline{x}\in C$ och $\overline{x}+\overline{y}\in C$.

Man kallar $C$ för en linjär kod av dimension $k$ och längden $n$.

Vi skriver $\overline{v}=(a_1,a_2,...,a_k)$.

*Hammingvikten* $\text{wt}(\overline{v})$ av en vektor definieras som antalet $a_i≠0$.  

Notera att Hammingavståndet $d(\overline{x},\overline{y})=\text{wt}(\overline{x}-\overline{y})$.

Sats: $d(C)=\min(\{\text{wt}(\overline{v}):\overline{v}\in C\and \overline{v}≠\overline{0}\})$.

### Binär linjär kod

Nu framöver använder vi oss av $\mathbb{F}_2=\{0,1\}\mod 2$. Låt $P$ vara en $k\text{x}(n-k)$-matrix. Bilda $G=(I_k\; P)$ ($k\text{x}n$-matris). Raderna i $G$ är linjärt oberoende. Alla kodord $c$ fås genom att för alla $x\in\mathbb{F}_2^k$ beräkna $\overline{c}=\overline{x}G$. $G$ kallas för en *generatormatris*.

### Sats

Låt $A$ vara en $(n-k)\text{x}n$-matris och $v\in\mathbb{F_2}^n$. Då gäller att $\overline{v}A^T=\overline{0}\iff v \in C$. Då kallas även $A$ för en kontrollmatris för koden $C$.

#### Sats

Låt $H=(-P^T\;I_{n-k})$ är en kontrollmatris till $C$ för linjära koder.

#### Exempel

$$
n=5,k=2,I_2=\left(\begin{array}{cc}
1 & 0 \\
0 & 1
\end{array}\right),P=\left(\begin{array}{ccc}
1 & 0 & 1\\
0 & 1 & 1
\end{array}\right),G=\left(\begin{array}{ccccc}
1 & 0 & 1 & 0 & 1 \\
0 & 1 & 0 & 1 & 1
\end{array}\right)
$$

Ord finns i $\mathbb{F}_2^2$ och kodord i $\mathbb{F}_2^5Ko$.

Kodningsavbildningen $xG,x\in\mathbb{F}_2^2$ ges av 
$$
\left(\begin{array}{ccc}
0&0
\end{array}\right)
\left(\begin{array}{ccc}
1 & 0 & 1 & 0 & 1\\
0 & 1 & 0 & 1 & 1
\end{array}\right)
=
\left(\begin{array}{ccc}
0 & 0 & 0 & 0 & 0
\end{array}\right)\\
\left(\begin{array}{ccc}
0&1
\end{array}\right)
\left(\begin{array}{ccc}
1 & 0 & 1 & 0 & 1\\
0 & 1 & 0 & 1 & 1
\end{array}\right)
=
\left(\begin{array}{ccc}
0 & 1 & 0 & 1 & 1
\end{array}\right)\\
\left(\begin{array}{ccc}
1 & 0
\end{array}\right)
\left(\begin{array}{ccc}
1 & 0 & 1 & 0 & 1\\
0 & 1 & 0 & 1 & 1
\end{array}\right)
=
\left(\begin{array}{ccc}
1 & 0 & 1 & 0 & 1
\end{array}\right)\\
\left(\begin{array}{ccc}
1 & 1
\end{array}\right)
\left(\begin{array}{ccc}
1 & 0 & 1 & 0 & 1\\
0 & 1 & 0 & 1 & 1
\end{array}\right)
=
\left(\begin{array}{ccc}
1 & 1 & 1 & 1 & 0
\end{array}\right)
$$
Hammingvikterna $\text{wt}$ ges av
$$
\text{wt}(00000)=0\\
\text{wt}(01011)=3\\
\text{wt}(10101)=3\\
\text{wt}(11110)=4\\
d(C)=\min(\{3,3,4\})=3
$$
Vi noterar att $3\geq 2+1$ och kan då säga att upp till två fel kan upptäckas. Vidare är $3\leq 2*1 + 1$ och vi kan alltså korrigera upp till ett fel.
$$
H=\left(\begin{array}{ccccc}
1 & 0 & 1 & 0 & 0\\
0 & 1 & 0 & 1 & 0\\
1 & 1 & 0 & 0 & 1
\end{array}\right)\\
\overline{v}=(11010)\notin C\\
\overline{v}H^T=(11010)\left(\begin{array}{ccccc}
1 & 0 & 1\\
0 & 1 & 1\\
1 & 0 & 0\\
0 & 1 & 0\\
0 & 0 & 1
\end{array}\right)=
(100)≠(000)\;(\text{dvs. ej kodord})
$$

### Rätta fel i linjära koder

Se tabell.

Exempelvis $\overline{v}_3+\overline{c}_3=00010+10101=10110\mod 2$.

Betrakta $\overline{v}_i$ som en störning av $\overline{c}_i$. Sätt $x=\overline{v_i}+\overline{c}_j$. Då är $xH^T=(\overline{v}_i+\overline{c}_j)H^T=\overline{v_i}H^T+\underbrace{\overline{c}_jH^T}_{=0}=\overline{v}_iH^T$. Det vill säga att den enda intressanta kolumnen är den första. Vi sätter $\text{s}(x)=xH^T$ som kallas syndromet för $x$.

#### Korrigeringsalgoritm

Indata: $x\in\mathbb{F}_2^n$.

1. $y\leftarrow \text{s}(x)$
2. Hitta $i$ (rad) i $y$ förekommer
3. Returnera $c\leftarrow x + \overline{v}_i$

## McElieces kryptosystem

Från 1978. Assymetriskt krypto.

#### Nyckelkonstruktion

Låt $G$ vara en $(n,k)$-kod likt beskrivet ovan. Låt $P$ vara en permutationsmatris (alltså inte det $P$ som finns i $H$ ) av ordning $n$ (d.v.s. exakt en etta i varje rad och kolonn). Vidare låt $S$ vara en inverterbar matris av ordning $k$. Sätt $G'=SGP$.

Den publika nyckeln är $G'$ tillsammans med information om hur många fel $t$ den kan korrigera. Privat nyckeln består av $G$, $S$ och $P$.

#### Kryptering

Klartexten $m\in\mathbb{F}_2^k$. Efemär nyckel ges av $e\in\mathbb{F}_2^n$ med som flest $t$ stycken ettor.

Kryptogrammet ges av $c=mG'+e$.

#### Dekryptering

1. $u\leftarrow cP^{-1}$
2. Finn det $\overline{v}\in C$ som är närmast $u$ 
3. Bestäm $\overline{w}$ så att $\overline{v}=\overline{w}G$
4. Returnera $\overline{w}S^{-1}$

$u=cPÅ^{-1}=(mG'+e)P^{-1}=mSGPP^{-1}+eP^{-1}=mSG+eP^{-1}$

$v=wG=(mS)G$

## Kroppsutvidningar

Låt $q=2^e$ där $e\in\mathbb{N}$ och låt $\mathbb{F}_q=GF(q)$. $GF$ är gallardkroppen.

Låt $\mathbb{F}_q\subseteq K$ och antag att $K$ är en kropp sådan att restriktionen av addition och multiplikation i $K$ till $\mathbb{F}_q$ motsvarar addition och multiplikation i $\mathbb{F}_q$.

Man kan skriva $(K, +, *)$ för att visa att addition och multiplikation är definierat. Vi har alltså även $(\mathbb{F}_q,+,*)$ för samma operatorer.

$\mathbb{F}_q$ kallas här för underkropp och $K$ för kroppsutvidgning, ett vektorrum över $\mathbb{F}_q$.

Låt $x,y\in K$ och $a\in \mathbb{F}_q$. Då kan vi definiera vektoradditionen $x+y$ och skalärmultiplikationen $ax$. 

Antag att $K$ är ändligtdimensionellt över $\mathbb{F}_q$.

Det existerar $\beta_1,\beta_2,...\beta_n\in K$ sådana att alla $x\in K$ kan skrivas entydigt på formen $x=x_1\beta_1+...+x_n\beta_n$ där $x_1,x_2,...,x_n\in \mathbb{F}_q$.

För vidare information, se kompendium från Robert Nyqvist.

## Talkroppssållet

Den snabbaste metoden för att faktorisera heltal. Pollard 1988.

Givet ett sammansatt, udda heltal $n$. Vi söker $x$ och $y$ så att $x^2\equiv y^2 \mod n$ och att $x\not\equiv y\mod n$. Då är $\gcd(x-y, n)$ en möjlig icke-trivial delare till $n$.

Låt $d$ vara ett positivt heltal så att $d>1$ och att $n>2^{d^2}$. Sätt $m=\lfloor{n^{1/d}\rfloor}$. Skriv $n$ i basen $m$, d.v.s. $n=c_dm+c_{d-1}m^{d-1}+...+c_2m^2+c_1m+c_0$ där $c_i\in\{0,1,...,m-1\}$. Vi har att $c_d=1$.

Sätt $f(t)=c_dt^d+c_{d-1}m^{d-1}+...+c_2t^2+c_1t+c_0$.

Notera att $f(m)=n$ , d.v.s. $f(m)\equiv 0 \mod n$. Sannolikt är $f(t)$ irreducibelt, d.v.s. det går går inte att skriva $f(t)=a(t)b(t)$ där $a(t)$ och $b(t)$ är polynom med heltalskoefficienter och båda av grad $≥1$.

Motivering: om det inte var fallet skulle $n=f(m)=\underbrace{a(m)}_{\in \mathbb{Z}}\underbrace{b(m)}_{\in \mathbb{Z}}$ ge ett heltal, vilket innebär att vi faktoriserat $n$. Vidare faktorisering är därför onödig.

Sätt $\gamma=(\frac{8}{n})^{1/3}+\epsilon,\;\epsilon>0$ och $B=\exp(\gamma(\log n)^{1/3}(\log \log n)^{2/3})$. Vi ska alltså studera de primtal som är mindre än $B$. Vidare är $d=\lfloor{(\frac{2}{\gamma})^{1/2}(\frac{\log n}{\log\log n})^{1/3}}\rfloor$.

### Ringutvidgningar

Låt $\alpha\in\mathbb{C}$ vara ett nollställe till $f(t)$, d.v.s. $f(\alpha)=0$. Låt $\alpha_1, \alpha_2, ...,\alpha_d$ vara samtliga nollställen till $f(t)$.

Då är $f(t)=(t-\alpha_1)(t-\alpha_2)...(t-\alpha_d)$.

Bilda $\mathbb{Z}_{[d]}=\{x_0+x_1\alpha^{d-1}+x_2\alpha^2+...+x_{d-1}\alpha^{d-1}:x_k\in\mathbb{Z}\}$.

Notera att $\alpha^d-1+c_{d}\alpha^{d-1}+...+c_2\alpha^2+c_1\alpha+c_0=0$ och att $\alpha^d=-c_{d-1}\alpha^{d-1}-...-c_2\alpha^2-c_1\alpha-c_0$.

Notera också att $\mathbb{Z}\subset\mathbb{Z}_{[d]}$. Alltså fungerar aritmetiken "som vanligt" om vi enbart använder heltalen.

Om $g(t)\in\mathbb{Z}_{[d]}$ så gäller att $g(\alpha)\in\mathbb{Z}_{[\alpha]}$. Så varje $\beta\in\mathbb{Z}_{[\alpha]}$ har minst ett polynom $g(t)\in\mathbb{Z}_{[t]}$ så att $g(\alpha)=\beta$.

Låt $\sigma:\mathbb{Z}_{[\alpha]}\rightarrow \underbrace{\mathbb{Z}/n\mathbb{Z}}_{\mathbb{Z}_n}$ enligt följande: $\sigma(\beta)=\sigma(g(\alpha))=g(m)\mod n$, d.v.s.  avbilda $\beta=g(\alpha)$ på $m$.

*  $\sigma(\beta_1+\beta_2)=\sigma(\beta_1)+\sigma(\beta_2)\mod n$
* $\sigma(\beta_1*\beta_2)=\sigma(\beta_1)*\sigma(\beta_2)\mod n$

Vi har att $\sigma(g(\alpha)^2)=\sigma(g(\alpha))^2$.

Antag att vi funnit en mängd $S$ av plynom $g(t)\in\mathbb{Z}_[t]$ sådana att $\prod_{g(t)\in S} g(\alpha)=\beta^2$ och att $\prod_{g(t)\in S}g(m)=y^2$.

#### Exempel

$S=\{g_1(t),g_2(t),g_3(t)\}$. $\prod_{g\in S}g(m)=g_1(m)g_2(m)g_3(m)$.

### Ringutvidningar forts.

Vidare är $\sigma(\beta)\equiv x\mod n$ för något heltal $x$. Då är i sin tur $x^2\equiv \sigma(\beta^2)=\sigma(\beta^2)=\sigma\left(\prod_{g\in S}g(\alpha)\right)=\prod_{g\in S}\sigma(g(\alpha))=\prod_{g\in S}g(m)=y^2\mod n$.

### Talkroppar och normer

En talkropp definieras på följande sätt: $\mathbb{Q}(\alpha)=\{x_0+x_1\alpha+x_2\alpha^2+...+x_{d-1}\alpha^{d-1}:x_k\in\mathbb{Q}\}$.

Låt $\beta\in\mathbb{Q}(\alpha)$. Då finns det ett polynom $g(t)\in\mathbb{Q}_{[t]}$ så att $g(\alpha)=\beta$.

Bilda $N:\mathbb{Q}(\alpha)\rightarrow\mathbb{Q}$ enligt följande: $N(\beta)=N(g(\alpha))=\prod_{i=1}^dg(\alpha_i)$ där $f(\alpha_1)=f(\alpha_2)=...=f(\alpha_d)=0$.

Då kallas $N(\beta)$ för normen av $\beta$.

* $N(\beta_1\beta_2)=N(\beta_1)N(\beta_2)$
* om $g(t)\in\mathbb{Z}_{[t]}$ så är $N(g(\alpha))\in\mathbb{Z}$ 

Låt $a$ och $b$ vara heltal där $gcd(a, b)=1$ och sätt $g(t)=a-bt\in\mathbb{Z}_{[t]}$.

Man säger att $a-b\alpha$ är $B$-milt om $N(g(\alpha))=N(a-b\alpha)$ är $B$-mild. Alla primtal som delar $N(a-b\alpha)$ är mindre än $B$.

Vi har att $N(a-b\alpha)=\prod_{i=1}^d(a-b\alpha_i)=b^d\prod_{i=1}^d(\frac{a}{b}-\alpha_i)=b^df(\frac{a}{b})$.

Vi söker en mängd $S=\{(a,b):a,b\in\mathbb{Z}\}$ vidare gäller att $gcd(a,b)=1$ och att $\prod_{(a,b)\in S}(a-b\alpha)$ är en kvadrat i $\mathbb{Z}_[\alpha]$ (det vill säga $\beta^2$). Då är $\prod_{(a,b)\in S}N(a-b\alpha)$ en kvadrat $\mathbb{Z}$ (d.v.s. $y^2$).

## Introduktion till gröbnerbaser

### Kort om ideal

$R$ är en ring, $I\subseteq R$. Om $ab\in I$ för alla $a\in R$ och alla $b\in I$ och $(I,+)$ är en grupp, så säges $I$ vara ett ideal till $R$.

Lått $\mathbb{F}$ vara en kropp och $I\subset F[X_1,X_2,...,x_m]$ ett ideal.

Låt $f_1,f_2,...,f_l\in\mathbb[\overline{X}]$ och låt $I$ vara de element som skrivs som en linjärkombination av $f_1,f_2,...,f_l$.

Denna mängd $I$ är ett ideal och man skriver $I=(f_1,f_2,...,f_l)$ och säger att $I$ genereras av $F=\{f_1,f_2,...,f_m\}$.

#### Hilberts nullstellensatz

Låt $\mathbb{F}$ vara en algebraiskt sluten kropp och $I$ ett icke-trivialt ideal till $\mathbb{F}[\overline{X}]$ med ett givet antal variabler. Då existerar det ett element $\overline{a}=(a_1,a_2,...,a_m)\in\mathbb{F}^m$ så att $f(\overline{a})=0$ för alla $f\in I$. 

### Sortering och reducering

Grad-lexikongrafisk ordning i först m.a.p. totalgrad och sedan i bokstavsordning.

Mn sägera att $f$ reduceras till $h\mod g$ i ett steg om $a_i\overline{X}^i$ är delbar med $lt(g)$ och $h=f-\frac{a_i\overline{X}^i}{lt(g)}g$. Med $lt(g)$ menas den ledande termen efter reducering.

Man skriver $f\rightarrow^g h$. Viktigt specialfall: $h=f-\frac{lt(f)}{lt(g)}g$ tack $lt(h)\lt lt(f)$.

#### Exempel

$$
f(X,Y,Z)=X^4+XY^2Z=XXXX+XYYZ=X^4+XY^2Z\\
f(X,Y,Z)=X^2Y-X^2Z+XYZ=XXY-XXZ+XYZ=X^2-X^2+XYZ
$$

$$
g_1=X^3-XZ, lt(g)=X^3\\
h_1=f-\frac{x^4}{x^3}g=X-XY+X^2Y+Y^2-xY^2-Z+YZ+XYZ-Z^2\\
g_2=XY^2+YZ,lt(g_2)=XY^2
...
$$

## Gröbnerbaser forts.

Låt $F=\{g_1,g_2,..,g_l\}\subseteq\mathbb{F}[\overline{X}]$ och $I=(g_1,g_2,...,g_l)$. Då säges $F$ vara en gröbnerbas för $I$ om det för varje $f\in I$ gäller att $lt(g_i)|lt(f)$ för alla $i=1,2,...,l$.

$S$-polynomet för $f$ och $g$ ges av $S(f,g)=\frac{L}{lt(t)}f-\frac{L}{lt(g)}g$ där $L=lcm(lt(f),lt(g))$.

### Exempel

$$
f=X^2Y-XZ+Y\\
g=XY^2+YZ\\
L=X^2Y^2\\
S(f,g)=\frac{X^2Y^2}{X^2Y}f-\frac{X^2Y^2}{XY^2}g=Y^2-2XYZ
$$

### Buchbergers sats

$F$ är en gröbnerbas om och endast om $S(g_i,g_j)$ reduceras till $0$ för varje $i≠j$ i ett eller flera steg.

### Sats

Reducera vare $S(g_i,g_j)$ till $h_{i,j}$ med hjälp av polynomen i $F$. Om $h_{i,j}≠0$ så läggs $h_{i,j}$ till $F$. Efterhand läggs polynomen $g_{l+1},g_{l+2},...,$ till. Upprepa tills dess att alla $S(g_i, g_j), i≠j$ reduceras till $0$.

Denna algoritm avbryter efter ett ändligt antal steg och $F$ är en gröbnerbas.

### Sats

En gröbnerbas $\{g_1,g_2,...,g_l\}$ säges vara minimal om varje $g_i$ är monisk, det vill säga den inledande termen har en etta som koefficient. Dessutom måste $lt(g_i)\not|lt(g_j)$ då $i≠j$.

Om t.ex. $lt(g_1)|lt(g_l)$ så kan vi ersätta $g_l$ med $h$ då $g_l\rightarrow^{g_1} h$. $h$ är en linjärkombination av $g_1,g_2,...,g_{l-1}$och $lt(h)\lt lt(g_l)$. Dessutom vet vi att $h\in I$.

En gröbnerbas är reducerad om varje $g_i$ är monisk och ingen term i $g_i$ är delbar med $lt(g_j)$ då $i≠j$.

Först reduceras $g_1$ med hjälp av $g_2,...,g_l$ till något $h_1$ som ersätter $g_1$. Reducera $g_2$ med hjälp av $h_1,g3,...,g_l$ till $h_2$. Ersätt $g_2$ med $h_2$. Forstätt för övriga $g_i$.