# Introduction
A Rust zkVM with a Modular Proof System. 

## How it works


# Commitments
## Merkle Tree
In a Merkle tree, the green nodes represent the values of the polynomial committed to by the prover (such as the polynomial values $a = f(0),b = f(1),c = f(2),d = f(3)$. Each committed hash value forms the leaf nodes of the Merkle tree (nodes 4, 5, 6, and 7 in the diagram). All other non-leaf nodes are the hash of the concatenation of their corresponding child nodes (for example, $\mathsf{hash}(\# 2) = \mathsf{hash}\left( {\mathsf{hash}(\# 4),\mathsf{hash}(\# 5)} \right)$. The root node is referred to as the Merkle root.

 

As illustrated in Fig 1, a distinctive feature of the Merkle tree is that any change in a single leaf node will result in a change in the Merkle root. Conversely, if it can be proven that the root hash remains constant, the entire tree must also be constant. This means that the leaf node values have not been modified.

## Polynomial Commitments Using Merkle Trees

**Commit:** Generate a Merkle root based on the values of the polynomial (like the four nodes shown in the diagram).

**Decommit:** Calculate a random point (such as node $c$) based on $root(f)$. The data transmitted is $\left( {root(f),c,path(c)} \right)$ where, $path(c)$ is the hash of nodes 7 and 2, serving as the verification path for node $c$.

**Verify:** Compute a new Merkle $root'$, using $\left( {c,path(c)} \right)$. Perform a consistency check by comparing $root'$ and the received Merkle root $root$. If $root'=root$, accept; otherwise, reject.


# Low-degree Detection
## Direct Tests
For a constant polynomial $f(x) = c$, at a fixed point ${z_1}$ and a random point $w$ calculated based on Fiat-Shamir, the verifier checks if 
$$ f({z_1}) = f(w). $$
If it is true, the verifier accepts that the degree of the polynomial $f(x)$ is less than 1. For a linear polynomial 
$$f(x)=bx+c$$
at fixed points $\left( {{z_1},f({z_1})} \right) $ and $\left( {{z_2},f({z_2})} \right)$ and a random point $w$ calculated based on Fiat-Shamir, the verifier checks if the third point $\left( {w,f(w)} \right)$ lies on the same line as $\left( {{z_1},f({z_1})} \right) $ and $\left( {{z_2},f({z_2})} \right)$. 

If this is the case, the verifier accepts that the degree of the polynomial $f(x)$ is less than 2. Extension: A polynomial $f(x)$ of degree $d$ or lower requires $d$ fixed points and one random point for verification. Given three points, a quadratic curve is determined, and a random point is selected for verification.

## Linear Combination Test
Suppose there are two polynomials $f(x)$ and $g(x)$ of degree at most $d$. Using the direct testing method above requires $2(d+1)$ points for execution testing. To optimize this testing method, use the Fiat-Shamir heuristic to compute a random number $\alpha$, and combine polynomials $f(x)$ and $g(x)$ as:
$$h(x) := f(x) + \alpha \cdot g(x).$$
This formula is called a linear combination. The prover constructs a Merkle tree based on the values of $h(x)$ and sends the Merkle root to the verifier. Then the verifier can verify the Merkle tree and only needs $d+1$ points to verify that the degree of $h(x)$ is less than $d$.
Note that the degree of $h(x)$ is $\max\{\deg(f), \deg(g)\}$.

## Polynomial Folding Lemma
Given that polynomial $f(x)$ have degree $d$, where $d={2^n}$. Let $g({x^2})$ be the even terms of $f(x)$, and $h({x^2})$ be the odd terms of $f(x)$. Then
$$
f(x)=g({{x}^{2}})+x\cdot h({{x}^{2}}). 
$$
The above formula is called the folding formula. Let $y={x^2}$, then for $y$, the degrees of polynomials $g(y)$ and $h(y)$ are $d/2$.

For example: Given a polynomial $f(x)$ of degree $d={2^3}$
$$
f(x) = {a_0} + {a_1}x + {a_2}{x^2} + {a_3}{x^3} + {a_4}{x^4} + {a_5}{x^5} + {a_6}{x^6} + {a_7}{x^7} + {a_8}{x^8}.
$$
The even and odd terms of $f(x)$ are $f(x) = g({x^2}) + x \cdot h({x^2})$
$$\begin{array}{l}
g({x^2}) = {a_0} + {a_2}{x^2} + {a_4}{x^4} + {a_6}{x^6} + {a_8}{x^8}\\
xh({x^2}) = {a_1}x + {a_3}{x^3} + {a_5}{x^5} + {a_7}{x^7} + 0{x^9}
\end{array}$$
Let $y={x^2}$, then
$$\begin{array}{l}
g(y) = {a_0} + {a_2}y + {a_4}{y^2} + {a_6}{y^3} + {a_8}{y^4}\\
h(y) = {a_1} + {a_3}y + {a_5}{y^2} + {a_7}{y^3} + 0{y^4}
\end{array}$$
Rewriting as
$$\begin{array}{l}
g(x) = {a_0} + {a_2}x + {a_4}{x^2} + {a_6}{x^3} + {a_8}{x^4}\\
h(x) = {a_1} + {a_3}x + {a_5}{x^2} + {a_7}{x^3} + 0{x^4}
\end{array}$$
Therefore, the degrees of $g(x)$ and $h(x)$ are both $d/2$. The original polynomial of degree $d$ is equivalent to the sum of odd and even terms, with degree decreased to $d/2$.	
Folding half each time, that is, $2$, can generalize the folding $2^n$, thus improving the folding efficiency.


## FRI
FRI is used to verify polynomial degree is less than $d$. By combining the above direct test, linear combination test, and polynomial Folding Lemma, it is possible to test the degree of a polynomial ${{f_0}}(x)$ of degree $d={2^n}$ in only $O(\log d)$ rounds.

------------------------------------
**Prover: In step 1,** 

(1) Commit to the degree $d$ polynomial ${{f_1}}(x)$ by computing its Merkle root $root({f_1})$.

(2) Compute the hash of the Merkle root to get a random number $z$:
$$z: = \mathsf{hash}\left( {root({f_1})} \right)$$
(3) Computing polynomial values ${f_1}(z),{f_1}( - z)$.

**Send:** $\{root({f_1}),{f_1}(z),{f_1}( - z),path({f_1}(z)),path({f_1}( - z))\}$

**Verifier:**

(1) Use the Merkle root $root({f_1})$ and path $path({f_1}(z))$ to verify the correctness of ${f_1}(z)$:
$$root({f_1}) = \mathsf{Merkle}\left( {{f_1}(z),path({f_1}(z))} \right)$$
(2) Similarly, verify ${f_1}(-z)$ using its path. If both checks pass, accept. Otherwise, reject.

------------------------------------

**Prover: In step 2,**

(1) According to the folding formula, the degree $d$ polynomial ${f_1}(x)$ can be expressed as:
$${f_1}(x) = {g_1}({x^2}) + x \cdot {h_1}({x^2})$$
Let this be Formula 1.

(2) Compute a hash based on the random number $z$ to obtain a new random number ${\alpha_2}$:
$${\alpha _2}: = \mathsf{hash}(z) = \mathsf{hash}\left( {\mathsf{hash}\left( {root({f_1})} \right)} \right)$$
(3) Construct a linear combination polynomial:
$${f_2}(x) = {g_1}(x) + {\alpha _2} \cdot {h_1}(x)$$
(4) Commit to the polynomial ${f_2}(x)$ by computing its Merkle root $root({f_2})$. Here ${f_2}(x)$ has degree $d/2$.

(5) Computing polynomial values ${{f}_{2}}(-{{z}^{2}})$.

**Send:** 
$\{root({f_2}),{f_2}( - {z^2}),path({f_2}({z^2})),path({f_2}( - {z^2}))\}$. 

Note that there is no need to send the value ${f_2}({z^2})$ since it can be computed directly.

**Verifier:**

(1) Hash the Merkle root $root({f_1})$ to obtain a random number $z$:
$$z: = \mathsf{hash}\left( {root({f_1})} \right).$$
(2) Using the data ${f_1}(z),{f_1}( - z)$ from Step 1, the random number $z$, and the folding formula (Formula 1), obtain:
$$\begin{array}{l}
{f_1}(z) = {g_1}({z^2}) + z \cdot {h_1}({z^2})\\
{f_1}( - z) = {g_1}({z^2}) - z \cdot {h_1}({z^2})
\end{array}$$
This allows solving equations to obtain ${{g}_{1}}({{z}^{2}}),{{h}_{1}}({{z}^{2}})$.

(3) Hash $z$ and $root({f_2})$ to obtain another random number ${\alpha_2}$:
$${\alpha _2}: = \mathsf{hash}(z,root({f_2}))$$
(4) Using ${g_1}({z^2}), {h_1}({z^2})$, the random ${\alpha_2}$, and the linear combination formula, compute:
$${f_2}({z^2}): = {g_1}({z^2}) + {\alpha _2} \cdot {h_1}({z^2})$$
to obtain ${f_2}({z^2})$.

(5) Use the received $root({f_2}), path({f_2}({z^2}))$ to verify ${f_2}({z^2})$:
$$root({f_2}) =  = \mathsf{Merkle}\left( {{f_2}({z^2}),path({f_2}({z^2}))} \right).$$
(6) Similarly verify ${f_2}(-{z^2})$. Accept if both checks pass, otherwise reject.

------------------------------------

**Prover: In step 3,**

(1) According to the polynomial folding formula, the degree $d/2$ polynomial ${f_2}(x)$ can be expressed as:
$${f_2}(x) = {g_2}({x^2}) + x \cdot {h_2}({x^2})$$
Let this be Formula 2.

(2) Hash $z$ and $root({f_2})$ to obtain a random number ${\alpha_3}$:
$${\alpha _3}: = \mathsf{hash}(z,root({f_2}))$$
(3) Construct a linear combination polynomial:
$${f_3}(x) = {g_2}(x) + {\alpha _3} \cdot {h_2}(x)$$
(4) Commit to ${f_3}(x)$ by computing its Merkle root $root({f_3})$.
Here ${f_3}(x)$ has degree $d/{2^2}$.

(5) Computing polynomial values ${{f}_{3}}(-{{z}^{4}})$.

**Send:** $\{root({f_3}),{f_3}( - {z^4}),path({f_3}({z^4})),path({f_3}( - {z^4}))\}$.

Note that there is no need to send ${f_3}({z^4})$ since it can be directly computed.

**Verifier:**

(1) Using the verified value ${f_2}({z^2})$ from Step 1, ${z^2}$, and the folding formula (Formula 2), obtain:
$$\begin{array}{l}
{f_2}({z^2}) = {g_2}({z^4}) + {z^2} \cdot {h_2}({z^4})\\
{f_2}( - {z^2}) = {g_2}( - {z^4}) - {z^2} \cdot {h_2}( - {z^4})
\end{array}$$
This allows solving equations to obtain ${g_2}({z^4}), {h_2}({z^4})$.
(2) Hash $z$ and $root({f_2})$ to obtain the random number ${\alpha_3}$:
$${\alpha _3}: = \mathsf{hash}(z,root({f_2})).$$
(3) Using ${g_2}({z^4}), {h_2}({z^4}), {\alpha_3},$ and the linear combination formula, compute:
$${f_3}({z^4}): = {g_2}({z^4}) + {\alpha _3} \cdot {h_2}({z^4})$$
to obtain${f_3}({z^4})$.

(4) Use $root({f_3}), path({f_3}({z^4}))$ to verify ${f_3}({z^4})$:
$$root({f_3}) =  = \mathsf{Merkle}\left( {{f_3}({z^4}),path({f_3}({z^4}))} \right).$$
(5) Similarly verify ${f_3}(-{z^4})$. Accept if both checks pass, otherwise reject.

------------------------------------

**Prover: In step $\log(d)$,**

**Send:** $\{root({f_{\log (d)}}),{f_{\log (d)}}( - {z^n}),path({f_{\log (d)}}({z^n})),path({f_{\log (d)}}( - {z^n}))\}$

**Verifier:**

(1)	Compute the polynomial value ${f_{\log(d)}}({z^n})$.

(2) Based on the polynomial folding and linear combination formulas, obtain a polynomial:
$${f_{\log (d)}}(x) = {g_{\log (d)}}(x) + {\alpha _{\log (d)}} \cdot {h_{\log (d)}}(x)$$
This polynomial has degree $d/{2^{\log(d)}} = 1$, so it is a constant polynomial.

(3) The verifier uses direct testing to test the degree of the constant polynomial.

------------------------------------

Note that:

(1) For the value range in the above protocol, it is necessary that for each value $z$ in the range $L$, $-z$ is also in the range $L$.

(2) The commitment to the polynomial ${f_1}(x)$ is not over the range $L$, but rather over the range ${L^2} = \{x^2 : x \in L\}$.

## Probability Analysis
For the polynomial values ${f_0}(z), {f_0}(-z)$, assume the probability that ${f_0}(z) = {f_0}(-z) = 0$ is $\varepsilon$, where $0 < \varepsilon < 1$. Then the probability of other cases is $1-\varepsilon$, where $0 < 1-\varepsilon < 1$.
$$f(x) = g({x^2}) + x \cdot h({x^2})$$
If the $1-\varepsilon$ probability case occurs, i.e. ${f_0}(z) = {f_0}(-z) \neq 0$, then there exists a unique ${{\alpha }_{1}}$ that makes the linear combination zero:
$${f_1}({z^2}) = {g_0}({z^2}) + {\alpha _1} \cdot {h_0}({z^2}) = 0$$
However, ${\alpha_1}$ is a random number computed via Fiat-Shamir, so the probability of manipulating ${\alpha_1}$ to a desired value is equal to the difficulty of POW. Therefore, the probability that ${f_1}({z^2}) \neq 0$ approaches 1. If the prover cheats on ${f_1}({z^2})$, the Merkle consistency check will fail. Thus, if the $1-\varepsilon$ probability case occurs, the verifier will reject it.

Conversely, the probability the prover successfully cheats in a round is $\varepsilon$. Over $\log(d)$ rounds, the probability the prover succeeds in every round is ${\varepsilon}^{\log(d)}$, which decays exponentially. Therefore, the probability the prover can successfully cheat is negligible.
In summary, soundness holds except with negligible probability $\varepsilon$.

## Batch FRI

In the Batched FRI Protocol, the prover aims to demonstrate the closeness of a set of functions $f_0,f_1,...,f_N:H \leftarrow F $ to low-degree polynomials all at once. It is possible to run individual FRI protocols for each function $f_i$ in parallel. Specifically, the prover directly applies the FRI protocol to a random linear combination of each function $f_i$. After committing to the functions and receiving a uniformly sampled value $\varepsilon $ from the verifier, the prover calculates a function 
$$
f(X): = {f_0}(X) + \sum\limits_{i = 1}^N {{\varepsilon ^i}{f_i}(X)},
$$
and applies the FRI protocol to it.

The function $f$ is computed as ${f_0}(X) + \sum\limits_{i = 1}^N {{\varepsilon ^i}{f_i}(X)}$, where a distinct random value $\varepsilon _i \in K $ is used for each function $f_i$ rather than relying on powers of a single value $\varepsilon $. Although this alternative is secure, the soundness bound increases linearly with the number of functions $N$. Therefore, it's reasonable to assume that $N$ is sublinear in $K$ to maintain protocol security.

In the batched version, the verifier needs to confirm the correct relationship between functions $f_0,f_1,...,f_N$ and the initial FRI polynomial $p_0=f$. The verifier uses evaluations of $p_0$ received from the prover during each FRI query phase. To facilitate the verification
$$\begin{array}{l}
{p_0}(r): = {f_0}(r) + \sum\limits_{i = 1}^N {{\varepsilon ^i}{f_i}(r)} \\
{p_0}( - r): = {f_0}( - r) + \sum\limits_{i = 1}^N {{\varepsilon ^i}{f_i}( - r)} ,
\end{array}$$
the prover sends evaluations of functions $f_0,f_1,...,f_N$ at both $r$ and $-r$, allowing the verifier to perform a local consistency check between $f_0,f_1,...,f_N$ and $p_0$. These evaluations are accompanied by their respective Merkle tree paths.


# Fibonacci Sequence Stark
## zero knowledge proof
For an NP problem $F$, demonstrate publicly the input value $X$ and the output value $Z$ without revealing the secret input $Y$. Prove that you know an input value $Y$ that satisfies the computational relationship 
$$F(X,Y)=Z$$
such that the verifier accepts this fact.

## Fibonacci's sequence
A prover needs to prove that the 1000th Fibonacci number $Z$ starts from a public value $X$ and a secret value $Y$, such that $F(X,Y)=Z$. This process is equivalent to proving
$$ {{F}_{0}}:=X,~{{F}_{1}}:=Y $$
$$ {{F}_{i}}:={{F}_{i-2}}+{{F}_{i-1}} $$
$$ Z:={{F}_{1000}}.$$
The computation requires $n$ steps and $w$ registers. The trace $T$ is a $n\times w$ table, where $n=1000, w=2$. For example, if $X=3,Y=4$, the Table 1 can be constructed as follows:

| $n$    |  $T_{n,0}$   |   $T_{n_1}$  |
| --- | --- | --- |
|  0   |   3  |   4  |
|  1   |   4  |   7  |
|  2   |   7  |    11 |
|  3   |   11  |  18   |
|  4   |   18  |  29   |
|  ...   |  ...   |   ...  |
|  999   |  $F_{999}$   |  $F_{1000}$   |


The above algorithm can be encoded as transition constraints and boundary constraints as follows:
$${{T}_{i+1,0}}={{T}_{i,1}}$$
$${{T}_{i+1,1}}={{T}_{i,0}}+{{T}_{i,1}}.$$
$${{T}_{0,0}}=X,$$
$${{T}_{999,1}}=Z. $$
Therefore, the following inference can be made:

*The prover proving that he knows the secret value $Y$ satisfying the relation $F(X,Y)=Z$ is equivalent to the prover proving that it knows the trace $T$ satisfying the transition constraints $transition\_constraints$ and the boundary constraints $boundary\_constraints$.*


## Trace Polynomial
Let $n=0,...,999$ be the x-coordinates of a polynomial, and let the traces stored in register ${{T}_{n,0}}$ and register ${{T}_{n,1}}$ be the polynomial values, then the value expression of the trace polynomial can be constructed as follows:
$$ {{P}_{0}}(i)={{T}_{i,0}},i=0,...,999. $$
$$ {{P}_{1}}(i)={{T}_{i,1}},i=0,...,999. $$
Therefore, coefficient polynomials ${{P}_{0}}(x),{{P}_{1}}(x)$ of degree 999 can be constructed to express the traces.

The value expression of the trace polynomial can be equivalently transformed into the coefficient expression of the trace polynomial, so there is an equivalent transformation:

------------------------------------

**Fibonacci sequence ADD triple: $a_n=a_{n-1}+a_{n-2}$**

Trace value expression: ${{T}_{i+1,1}}={{T}_{i,0}}+{{T}_{i,1}},i=0,...,999$

Polynomial coefficient expression: ${{P}_{1}}(i+1)={{P}_{0}}(i)+{{P}_{1}}(i),i=0,...,999$

Polynomial coefficient expression: ${{P}_{1}}(i+1)-({{P}_{0}}(i)+{{P}_{1}}(i))=0,i=0,...,999$

Polynomial coefficient expression: $Q(x):={{P}_{1}}(x+1)-({{P}_{0}}(x)+{{P}_{1}}(x))=0,x=0,...,999$

------------------------------------

Note that the degree of $Q(x)$ is 1000.
We construct a public target polynomial: 
$$R(x)=(x-0)(x-1)(x-2)...(x-999)$$
If $x=0,...,999$, then the target polynomial $R(x)=0$.
There are other solutions $x'$ to the equation $Q(x)=0$.
Thus, we can compute a quotient polynomial 
$$C(x)=\frac{Q(x)}{R(x)}.$$
Note that the degree of the quotient polynomial is 1.

Similarly, we can construct a multiplication tuple.

------------------------------------

**Fibonacci's sequence MUL triple: $a_n=a_{n-1}*a_{n-2}$**

Trace value expression: ${{T}_{i+1,1}}={{T}_{i,0}}\cdot {{T}_{i,1}},i=0,...,999$

Polynomial coefficient expression: ${{P}_{1}}(i+1)={{P}_{0}}(i)\cdot {{P}_{1}}(i),i=0,...,999$

Polynomial coefficient expression: ${{P}_{1}}(i+1)-({{P}_{0}}(i)\cdot {{P}_{1}}(i))=0,i=0,...,999$

Polynomial coefficient expression: $Q(x):={{P}_{1}}(x+1)-({{P}_{0}}(x)\cdot {{P}_{1}}(x))=0,x=0,...,999$

------------------------------------

Note that the degree of $Q(x)$ is 2000.
The public target polynomial is still:
$$R(x)=(x-0)(x-1)(x-2)...(x-999)$$
If $x=0,...,999$, then the target polynomial $R(x)=0$.
There are other solutions $x'$ to the equation $Q(x)=0$.
Thus, we can compute a quotient polynomial 
$$C(x)=\frac{Q(x)}{R(x)}.$$
Note that the degree of the quotient polynomial is 1000.

Similarly, we can construct a multiplication quadruple.

------------------------------------

**Fibonacci's sequence MUL quadruple: $a_n=a_{n-1}*a_{n-2}*a_{n-3}$**

Trace value expression: ${{T}_{i+1,1}}={{T}_{i,0}}\cdot {{T}_{i,1}}\cdot {{T}_{i,2}},i=0,...,999$

Polynomial coefficient expression: ${{P}_{1}}(i+1)={{P}_{0}}(i)\cdot {{P}_{1}}(i)\cdot {{P}_{2}}(i),i=0,...,999$

Polynomial coefficient expression: ${{P}_{1}}(i+1)-({{P}_{0}}(i)\cdot {{P}_{1}}(i)\cdot {{P}_{2}}(i))=0,i=0,...,999$

Polynomial coefficient expression: $Q(x):={{P}_{1}}(x+1)-({{P}_{0}}(x)\cdot {{P}_{1}}(x)\cdot {{P}_{2}}(x))=0,x=0,...,999$

------------------------------------

Note that the degree of $Q(x)$ is 3000.
The public target polynomial is still:
$$R(x)=(x-0)(x-1)(x-2)...(x-999)$$
If $x=0,...,999$, then the target polynomial $R(x)=0$.
There are other solutions $x'$ to the equation $Q(x)=0$.
Thus, we can compute a quotient polynomial 
$$C(x)=\frac{Q(x)}{R(x)}.$$
Note that the degree of the quotient polynomial is 2000.

Therefore, the following inference can be made:

*Algorithms often involve multiple multiplications, so the degree of the quotient polynomial $C(x)$ is usually higher than the degree of the trace polynomial $T(x)$.*


Now we back to **Fibonacci's sequence ADD triple**, the transition constraints $transition\_constraints$ can be equivalently transformed into the following equations
$$ {{T}_{i+1,1}}={{T}_{i,0}}+{{T}_{i,1}}\Leftrightarrow {{C}_{0}}=\frac{{{P}_{1}}(x+1)-({{P}_{0}}(x)+{{P}_{1}}(x))}{\prod\nolimits_{[0,...,998]}^{i}{(x-i)}} $$
$$ {{T}_{i+1,0}}={{T}_{i,1}}\Leftrightarrow {{C}_{1}}=\frac{{{P}_{0}}(x+1)-{{P}_{1}}(x)}{\prod\nolimits_{[0,...,998]}^{i}{(x-i)}} $$
And the boundary constraints $boundary\_constraints$ can be equivalently transformed into the following 
$${{T}_{0,0}}=X\Leftrightarrow {{C}_{2}}(x)=\frac{{{P}_{0}}(x)-X}{x-0} $$
$$ {{T}_{999,1}}=Z\Leftrightarrow {{C}_{3}}(x)=\frac{{{P}_{1}}(x)-Z}{x-999} $$
Therefore, the following inference can be made:

*The prover proving that he knows the trace $T$ satisfying the transition constraints $transition\_constraints$ and the boundary constraints $boundary\_constraints$ is equivalent to the prover proving that he knows the polynomials ${{P}_{0}}(x),{{P}_{1}}(x)$ such that ${{C}_{0}}(x),{{C}_{1}}(x),{{C}_{2}}(x),{{C}_{3}}(x)$ are degree $D$ polynomials.*

On the contrary, if the verifier accepts that ${{C}_{0}}(x),{{C}_{1}}(x),{{C}_{2}}(x),{{C}_{3}}(x)$ are degree $D$ polynomials, then the transition constraints and boundary constraints hold. Therefore, the verifier accepts the prover's proof that he knows the secret value $Y$ satisfying the relation $F(X,Y)=Z$.

## Stark Workflow
Using the Fiat-Shamir transformation, calculate the random numbers ${{\alpha }_{0}},{{\alpha }_{1}},{{\alpha }_{2}},{{\alpha }_{3}}$. Transform the linear combination constraint polynomials ${{C}_{0}}(x),{{C}_{1}}(x)$ and boundary constraint polynomials ${{C}_{2}}(x),{{C}_{3}}(x)$
$$C(x) = {\alpha _0}{C_0}(x) + {\alpha _1}{C_1}(x) + {\alpha _2}{C_2}(x) + {\alpha _3}{C_3}(x)$$
Using the polynomial halving lemma,

1.	The prover provides the Merkle root $Root$ of the coefficients of the polynomial $C(x)$ and proves that its degree is $2^n$;
2.	Equivalently, the prover uses the random number $\beta _0$ from the Fiat-Shamir transformation to prove the Merkle root $Root_0$ of the coefficients of the polynomial $C^0(x)$ and proves that its degree is $2^{n-1}$;
3.	Equivalently, the prover uses the random number $\beta _1$ from the Fiat-Shamir transformation to prove the Merkle root $Root_1$ of the coefficients of the polynomial $C^1(x)$ and proves that its degree is $2^{n-2}$;
4.	And so on, ...
5.	Equivalently, the prover uses the random number $\beta _n$ from the Fiat-Shamir transformation to prove the Merkle root $Root_n$ of the coefficients of the polynomial $C^n(x)$ and proves that its degree is $2^0$;
6.	Finally, the verifier verifies the above halving process, verifies the Merkle root $Root_n$ of the coefficients of the polynomial $C^n(x)$, and verifies that the degree of the polynomial $C^n(x)$ is 1. This is equivalent to verifying the Merkle root $Root$ of the coefficients of the polynomial $C(x)$ and proving that its degree is 1024. This, in turn, is equivalent to verifying that the trace $T$ satisfies the transition constraints and boundary constraints, which is equivalent to verifying $F(X,Y)=Z$ without knowing the secret $Y$.




## Try it 

Check out the examples in [README](https://github.com/0xEigenLabs/eigen-zkvm).