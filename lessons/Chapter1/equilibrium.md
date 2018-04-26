# Equilibrium

## Profiles

We consider the following profile for $q$

$$
  q(r) = q_0 \left[ 1+ \left( \frac{r}{r_0} \right)^{2 \lambda} \right]^{\frac{1}{\lambda}}
$$

---
**todo** add bumps

---

Let us denote

$$
  r_0 = a \left[ \left( \frac{q_a}{q_0} \right)^{\lambda} -1 \right]^{-\frac{1}{2 \lambda}}
$$

Then the current is given as

$$
  J(r) = \frac{B_0}{\mu_0 R_0} \times \frac{2}{q_0 \left[1+ \left( \frac{r}{r_0} \right)^{2 \lambda} \right]^{\frac{1}{\lambda} +1}}
$$

However, we have the following approximation for $r$:

$$
  r \approx a \sqrt{1-\frac{\psi}{\psi_0}}
$$
  
where $\psi_0 = \psi(r=0)$.

Thus we obtain the follwing expression for $J$:

$$
  J(\psi) = \frac{B_0}{\mu_0 R_0} \times \frac{2}{q_0 \left[1+ \left( \frac{a^2}{r_0^2} \left( 1-\frac{\psi}{\psi_0} \right) \right)^{\lambda} \right]^{\frac{1}{\lambda} +1}}
$$

## Grad-Shafranov equation

We recall that at the equilibrium, $\psi$ is the solution of the Grad-Shafranov equation

$$
  \Delta^{\star} \psi = - \mu_0 \frac{R}{R_0} J(\psi)
$$

where, the Grad-Shafranov operator $\Delta^{\star}$ is defined as

$$
  \Delta^{\star} \psi & \, \hat{=} \, R^2 \nab \cdot \left( \frac{1}{R^2} \nab \psi \right) 
  \\
                             &  = R \partial_R \left( \frac{1}{R} \partial_R \psi \right) + \partial_{Z}^2 \psi
$$

### Normalisation

We now normalise the Grad-Shafranov equation, using:

$$    
  \Delta^{\star} \rightarrow \frac{1}{a^2} \tilde{\Delta}^{\star}, \quad
  R \rightarrow a \tilde{R}, \quad
  r_0 \rightarrow a \tilde{r_0}, \quad
  \psi \rightarrow \epsilon a B_0 \tilde{\psi}, \quad
  J \rightarrow \frac{B_0}{\mu_0 R_0} \tilde{J}
$$
  
We then get the following equation:

$$
  \tilde{\Delta}^{\star} \tilde{\psi} = - \epsilon \tilde{R} \tilde{J}(\tilde{\psi})
$$
  
with

$$
  J(\tilde{\psi}) = \frac{2}{q_0 \left[1+ \left( \frac{1}{\tilde{r_0}^2} \left( 1-\frac{\psi}{\psi_0} \right) \right)^{\lambda} \right]^{\frac{1}{\lambda} +1}}
$$

where $\epsilon=\frac{a}{R_0}$, inverse aspect ratio.

From now on, every physical quantity is dimensionless.

### Numerical solution

We use a Picard algorithm to treat the non-linearity

* $\psi^0$ is given,

* knowing $\psi^n$, we solve : 

$$
  \Delta^{\star} \psi^{n+1} = -\epsilon R J(\psi^n)
$$

---
**note**  

- $\mathcal{V}_h$ will denote a subspace of $H^1(\Omega)$ of finite dimension.
- Currently, we use Homogeneous Dirichlet boundary conditions.
---

#### Weak formulation

Let us introduce the following bilinear form, operating on $\mathcal{V}_h \times \mathcal{V}_h$:

$$
  a(v, \psi) = \int_{\Omega} \partial_R v \partial_R \psi + \partial_Z v \partial_Z \psi + \frac{1}{R} \partial_R \psi ~v ~d\Omega 
$$

and the linear form on $\mathcal{V}_h$

$$
  l(v; \psi) = \epsilon \int_{\Omega} R J(\psi) v ~d\Omega 
$$

The weak formulation of the Picard method writes

$$
  a(v, \psi^{n+1}) = l(v; \psi^n), \quad \forall v \in \mathcal{V}_h
$$

---
**note**: In practice, we take $\psi^0 = 0$.

---

---
**note**: the *fortran* weak formulation kernels are available in **fema/fortran/src/gallery/gallery_mhd_equilibrium.F90**.

---

---
**todo**: add link to source code after merging the devel-minorswing branch.

---


**TODO add plot**

   Numerical solution of the Grad-Shafranov equilibrium. 
