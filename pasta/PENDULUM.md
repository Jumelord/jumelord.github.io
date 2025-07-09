---
title: "Damped Pendulum"
layout: default
---

<!-- Enables MathJax -->
<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

# Damped Pendulum

The pendulum is one of the simplest mechanical systems. However, the presence of a nonlinear term in its equation of motion complicates the analysis, and in general, an exact analytical solution is not available. One way to study the behavior of this system is through **numerical methods**.

In this case, the **Euler method** — one of the simplest algorithms for solving differential equations — is used to simulate the motion of a damped pendulum. The simulation was implemented using the **Godot** engine.

Furthermore, mouse interaction has been implemented, allowing the pendulum to be moved directly by the user. System parameters such as the pendulum's length and air viscosity can also be freely adjusted.

---

## Physical Model

The system consists of a rigid, massless rod of length \\( L \\), fixed at one end, with a point mass \\( m \\) attached to the other. The pendulum forms an angle \\( \theta \\) with the vertical and is subject to gravity acting downward.

Due to the constraint imposed by the rod, the motion occurs only in the angular direction. The angular component of the gravitational force is:

$$
\vec{F}_\theta = -mg \sin(\theta)\hat{\theta}
$$

Applying Newton's second law:

$$
\vec{F} = m \ddot{\vec{r}} = -mg \sin(\theta)\hat{\theta}
$$

$$
\ddot{\vec{r}} = -g \sin(\theta)\hat{\theta}
$$

Using the arc length relation \\( \mathrm{d} \vec{r} = L\, \mathrm{d} \hat{\theta} \\), we get:

$$
\dot{\vec{r}} = L \dot{\vec{\theta}}
$$

Taking another derivative and projecting onto the angular coordinate:

$$
L \ddot{\theta} = -g \sin(\theta)
$$

So:

$$
\ddot{\theta} = -\frac{g}{L} \sin(\theta)
$$

This is a **nonlinear second-order differential equation**, for which a general analytical solution does not exist.

---

# Numerical Methods

## Euler's Method

Taylor expansion allows us to write most functions as a power series. If \\( x \\) is a point in the domain of the function and \\( a \\) is a known point, we can write \\( f(x) \\) as:

$$
f(x) = f(a) + f'(a)(x - a) + \frac{f''(a)}{2!}(x - a)^2 + \cdots
$$

For an initial value problem, we know \\( f(t) \\) and want to calculate \\( f \\) a short time ahead, at \\( t + \Delta t \\). Thus, we take \\( x = t + \Delta t \\) and \\( a = t \\).

$$
f(t + \Delta t) = f(t) + f'(t)\Delta t + \frac{f''(t)}{2!}(\Delta t)^2 + \cdots
$$

If \\( \Delta t \\) is sufficiently small, then \\( (\Delta t)^2 \\) and higher powers of \\( \Delta t \\) will be even smaller. So we can discard the remaining powers of \\( \Delta t \\), with an error on the order of \\( \Delta t^2 \\).

$$
f(t + \Delta t) \approx f(t) + f'(t)\Delta t
$$

Therefore, if we know \\( f(t) \\) and \\( f'(t) \\), we can approximate \\( f(t + \Delta t) \\).

## Applying the Method to Our Problem

Unfortunately, Euler's method can only be directly applied to equations where we know the derivative as a function of the independent variables and the function itself — and in our equation we only have the relationship of \\( \ddot{\theta} \\) with \\( \theta \\).

To solve this, we use a simple trick: define a new variable \\( u \\).

$$
u = \dot{\theta}
$$

Therefore:

$$
\dot{u} = \ddot{\theta}
$$

The equation we had before becomes:

$$
\dot{u} = -\frac{g}{L} \sin(\theta)
$$

$$
\dot{\theta} = u
$$

We first use Euler’s method to find \\( u \\) with the first equation, and then use the newly calculated \\( u \\) to find \\( \theta \\) with the second equation.

Euler's method then proceeds in two steps:

1. Update the velocity:

   $$
   u(t + \Delta t) = u(t) - \frac{g}{L} \sin(\theta(t))\, \Delta t
   $$

2. Update the angle:

   $$
   \theta(t + \Delta t) = \theta(t) + u(t + \Delta t)\, \Delta t
   $$
