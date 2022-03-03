# Subset Predicate Encryption with Weakly Attribute Hiding

## Notations

#### Bilinear Maps

$G_1,\ G_2,\ G_T \in \text{cyclic groups}$
$g_1,\ g_2,\ g_T\text{ are the generator of }G_1,\ G_2,\ G_T$

$e: G_1 \times G_2 \rightarrow G_T$
$e(g_1,\ g_2) = g_t$

#### define $[a]_i$

$\text{for } i \in \{1, 2, T\} \text{ and } a \in \mathbb Z_p$
$\text{define }[a]_i = g_i^a \in G_i$

#### define $S_k, S_C$
$\text{there are 2 vector }S_k, S_C$
$\text{cyphertext can be decrypted iff } S_k \subseteq S_C$

---

## Setup
- $\text{Setup}(n)$
$\text{choose } g_1 \in G_1,\ g_2 \in G_2\text{, then obtain }G = (g_1, g_2, g_T)$
$\text{randomly choose }x_1, x_2, ...\ x_n \in \mathbb Z_p$
$\text{randomly choose }w, t \in \mathbb Z_p$
$\text{compute }X_i = [x_i]_1 \text{ for } i = 1 ,2,... ,n$
$\text{compute }\Omega = [w]_T,\ T = [t]_1$

<br>

- $\text{Output }param,\ msk$
$param = (G, X_1, X_2, ..., X_n, T, \Omega)$
$msk = (x_1, x_2, ..., x_n, t, w)$
---

## KeyGen

- $\text{KeyGen}(param,\ msk,\ S_k)$
$\text{input the vector }S_k \in \{0, 1\}^n$
$\text{randomly choose }u, v \in \mathbb Z_p$
$\text{compute }X_K = \sum_{i = 1}^n S_{k_i} \cdot x_i$
$\text{compute }\hat K_1 = [-(w + X_ku + tv)]_2,\ K_2 = [v]_2,\ K_3 = [u]_2$

<br>

- $\text{Output }SK(\hat K_1,\ \hat K_2,\ \hat K_3,\ S_k)$
---

## Encrypt

- $\text{Encrypt}(param, M, S_C)$
$\text{input the vector }S_C \in \{0, 1\}^n$
$\text{randomly choose }s \in \mathbb Z_p$
$\text{compute } C_0 = \Omega ^ s\cdot M,\ C_1 = [s]_1,\ C_2 = T^s$
$\text{For }i = 1, 2, ..., n$
$\qquad \text{if }S_C == 1$
$\qquad \qquad \bar C_i = X_i^s$
$\qquad \text{else}$
$\qquad \qquad \bar C_i \leftarrow G_1 \text{ randomly}$


<br>

- $\text{Output }CT(C_0, C_1, C_2, \bar C_1, \bar C_2, ..., \bar C_n)$
---

## Decrypt

- $\text{Decrypt}(param, CT, SK)$
$\text{compute }C_3 = \prod_{i = 1}^n S_{k_i} \cdot \bar C_i$
$\text{compute }M = C_0 \cdot \prod_{i = 1}^3 S_{k_i} \cdot e(C_i,\hat K_i)$