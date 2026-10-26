---
title: "Root Locus Construction Rules"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "Root Locus"
level: BSc
status: drafted
confidence: 0
tags: [control-theory, root-locus, ma2008b, exam]
---
## Definition
Evans' rules sketch the [[Root Locus]] of $1+KG(s)H(s)=0$, $K\ge0$, with $n$ open-loop poles $p_i$ and $m$ zeros $z_j$ ($n\ge m$), without solving the characteristic equation for every $K$. The homework (Tarea 1, Módulo 4) asks for each of: poles and zeros, real-axis regions, asymptotes, breakaway/break-in points, gain $K$ and $\omega$ at the imaginary-axis crossing, and angles of departure/arrival.

## Properties
### Rule 0 — plot poles (×) and zeros (○)
The locus has $n$ branches, starts at the poles ($K=0$), ends at the zeros or at infinity ($K\to\infty$), and is symmetric about the real axis.

### Rule 1 — real-axis segments
Take a test point $s_0$ on the real axis. Complex-conjugate pairs contribute angles that cancel; real poles/zeros to the **left** of $s_0$ contribute $0°$; each real pole/zero to the **right** contributes $\pm180°$. The angle condition therefore holds iff
$$\#\{\text{real poles and zeros to the right of }s_0\}\text{ is odd.}$$

### Rule 2 — asymptotes
For large $|s|$, $G(s)H(s)\approx\dfrac{1}{(s-\alpha)^{n-m}}$. Applying the angle condition, $-(n-m)\angle(s-\alpha)=\pm180°(2N+1)$, so the asymptote angles are
$$\gamma=\frac{\pm180°(2N+1)}{n-m},\qquad N=0,1,\dots,n-m-1,$$
where $r=n-m$ is the **relative degree**. The asymptotes meet the real axis at the **centroid**
$$\alpha=\frac{\sum_{i=1}^n\operatorname{Re}(p_i)-\sum_{j=1}^m\operatorname{Re}(z_j)}{n-m}.$$
*Derivation (the slides leave it as homework).* Write $\dfrac{1}{GH}=\dfrac{s^n+a_1s^{n-1}+\dots}{s^m+b_1s^{m-1}+\dots}$ with $a_1=-\sum p_i$ and $b_1=-\sum z_j$. Polynomial long division gives
$$\frac1{GH}=s^{n-m}+(a_1-b_1)s^{n-m-1}+\dots$$
Compare with $(s-\alpha)^{n-m}=s^{n-m}-(n-m)\alpha\,s^{n-m-1}+\dots$: matching the second coefficient, $-(n-m)\alpha=a_1-b_1=-\sum p_i+\sum z_j$, hence $\alpha=\frac{\sum p_i-\sum z_j}{n-m}$ (imaginary parts cancel in conjugate pairs).

### Rule 3 — angles of departure (arrival)
Place a test point infinitesimally close to a complex pole $p_k$ and apply the angle condition; the unknown angle $\psi$ of the vector from $p_k$ is
$$\psi_{\text{dep}}=180°-\sum_{i\neq k}\angle(p_k-p_i)+\sum_j\angle(p_k-z_j),$$
and, for a complex zero $z_k$,
$$\psi_{\text{arr}}=180°-\sum_{j\neq k}\angle(z_k-z_j)+\sum_i\angle(z_k-p_i).$$

### Rule 4 — imaginary-axis crossing
Substitute $s=j\omega$ into $1+KG(s)H(s)=0$ and set real and imaginary parts to zero; solve for $\omega$ and $K$. Equivalently, use the [[Routh-Hurwitz Criterion]]: the $K$ that makes the $s^1$ row vanish is the critical gain, and the auxiliary polynomial of the $s^2$ row gives $\omega$.

### Rule 5 — breakaway and break-in points
On the real axis, $K(s)=-\dfrac{1}{G(s)H(s)}$ reaches a local maximum between two adjacent poles (branches leave) or a local minimum between two zeros (branches arrive). So candidates solve
$$\frac{dK}{ds}=0,$$
and a candidate is a breakaway/break-in point **only if it lies on the locus**, i.e. $K(s)$ is real and positive there (for real candidates: it is on a Rule-1 segment). Complex solutions are valid only if $K$ evaluated there is real and positive.

## Examples
**Tarea 1 (a).** $\dfrac{K(s+0.2)}{s^2(s+3.6)}$: poles $0,0,-3.6$; zero $-0.2$; $n-m=2$.
- Real axis: only $(-3.6,-0.2)$ (points in $(-0.2,0)$ have two poles to the right — even).
- Asymptotes $\pm90°$ from $\alpha=\frac{-3.6-(-0.2)}{2}=-1.7$.
- $K=-\frac{s^2(s+3.6)}{s+0.2}$; $\frac{dK}{ds}=0\iff(3s^2+7.2s)(s+0.2)-(s^3+3.6s^2)=0\iff s(2s^2+4.2s+1.44)=0$, so $s=0$ (the double pole) and $s=\frac{-4.2\pm\sqrt{6.12}}{4}=-0.4315,\,-1.6685$, both on the segment with $K=2.548$ and $K=3.662>0$ — a break-in and a breakaway point.
- Branches leave the double pole at $\pm90°$, return to the axis at $-0.4315$; one goes to the zero, the other meets the branch from $-3.6$ at $-1.6685$ and both leave along the $\pm90°$ asymptotes.
- $j\omega$ crossing: $D=s^3+3.6s^2+Ks+0.2K$; Routh $s^1$ entry $\frac{3.6K-0.2K}{3.6}>0$ for all $K>0$ → no crossing; stable for all $K>0$.

**Tarea 1 (b) / Module 4–5 exam.** $\dfrac{K(s+9)}{s(s^2+4s+11)}$: poles $0,\,-2\pm j\sqrt7$ ($\pm2.6458j$); zero $-9$.
- Real axis: $(-9,0)$. Asymptotes $\pm90°$ from $\alpha=\frac{(0-2-2)-(-9)}{2}=+2.5$ — in the RHP, so the complex branches eventually cross into it.
- Crossing: $D=s^3+4s^2+(11+K)s+9K$. Routh: $4(11+K)>9K\iff K<8.8$; at $K=8.8$, $4s^2+79.2=0\Rightarrow\omega=\sqrt{19.8}=4.4497$. **Stable for $0<K<8.8$.**
- Departure from $-2+2.6458j$: angles from pole $0$: $127.09°$; from $-2-2.6458j$: $90°$; from zero $-9$: $20.70°$. $\psi=180°-127.09°-90°+20.70°=-16.38°$ ($=343.62°$).
- Breakaway: $dK/ds=0$ has roots $-13.03$ and $-1.236\pm1.507j$, but $K(-13.03)=-416<0$ and $K$ at the complex roots is not real — **none lies on the locus**, so this locus has no breakaway points. (The course script printed all three as "breakaway points" — it does not check membership.)

**Tarea 1 (c).** $\dfrac{K(s+2)}{s^2-4s+139}$: open-loop poles $2\pm11.619j$ (unstable); zero $-2$; $n-m=1$ → one asymptote at $180°$.
- Real axis: $(-\infty,-2)$. Break-in: $dK/ds=0\Rightarrow s^2+4s-147=0\Rightarrow s=-2\pm\sqrt{151}$; only $-14.288$ is on the locus ($K=32.6$).
- Departure from $2+11.619j$: $180°-90°+\angle(4+11.619j)=180°-90°+71.0°=161.0°$.
- $D=s^2+(K-4)s+139+2K$ ⇒ stable iff $K>4$; at $K=4$, $\omega=\sqrt{147}=12.12$. The script's "maximum K is 4" is really the **minimum** stabilizing gain.

**Tarea 1 (d).** $\dfrac{K}{s(s+3)(s+4)(s+8)}$: real axis $(-3,0)$ and $(-8,-4)$; asymptotes $\pm45°,\pm135°$ from $\alpha=-15/4=-3.75$; breakaway $-1.0174$ (in $(-3,0)$) and $-6.7248$ (in $(-8,-4)$). The third root of $dK/ds=0$, $-3.5078$, lies in $(-4,-3)$, which is **not** on the locus ($K=-3.94<0$). Routh on $s^4+15s^3+68s^2+96s+K$: $\omega^2=96/15=6.4$ ($\omega=2.5298$) and $K_{\max}=68(6.4)-6.4^2=394.24$.

**Actividad 2.** $\dfrac{K}{s(s+2)(s^2+2s+5)}$: poles $0,-2,-1\pm2j$; asymptotes $\pm45°,\pm135°$ from $\alpha=-1$.
- $K=-(s^4+4s^3+9s^2+10s)$; $\frac{dK}{ds}=-(4s^3+12s^2+18s+10)=-2(s+1)(2s^2+4s+5)=0$ ⇒ $s=-1$ ($K=4$) and $s=-1\pm j\sqrt{1.5}=-1\pm1.2247j$, where $(s+1)^2=-1.5$ gives $s(s+2)=-2.5$, $s^2+2s+5=2.5$ and $K=6.25>0$ — **all three are genuine** breakaway points.
- Departure from $-1+2j$: angles from $0$: $116.57°$, from $-2$: $63.43°$, from $-1-2j$: $90°$ ⇒ $\psi=180°-270°=-90°$: the branch heads straight **down** to meet the other at $-1+1.2247j$. (The submitted script output says $+90°$ at the upper pole and $270°$ at the lower one — the signs are swapped.)
- Crossing: imaginary part $-4\omega^3+10\omega=0\Rightarrow\omega=1.5811$; real part $\omega^4-9\omega^2+K=0\Rightarrow K=16.25$.

## See also
[[Root Locus]], [[Routh-Hurwitz Criterion]], [[BIBO Stability and Pole Location]], [[Frequency Response]]
