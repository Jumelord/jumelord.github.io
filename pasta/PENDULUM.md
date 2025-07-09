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

The system consists of a rigid, massless rod of length \( L \), fixed at one end, with a point mass \( m \) attached to the other. The pendulum forms an angle ( $ \theta $ ) with the vertical and is subject to gravity acting downward.

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

Using the arc length relation \( \mathrm{d}\vec{r} = L\, \mathrm{d}\vec{\theta} \), we get:

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

## Taylor Expansion and the Euler Method

To solve the system numerically, we use a Taylor expansion of a function \( f(t) \) around a point \( t \):

$$
f(t + \Delta t) = f(t) + \Delta t\, f'(t) + \frac{(\Delta t)^2}{2!}\, f''(t) + \cdots
$$

For small time steps \( \Delta t \), higher-order terms can be neglected. Keeping only the first derivative leads to the **Euler method**:

$$
f(t + \Delta t) \approx f(t) + \Delta t\, f'(t)
$$

This is a **first-order numerical integration method**, with an error of order \( \mathcal{O}(\Delta t^2) \).

---

## Applying Euler’s Method to the Pendulum

To apply Euler's method, the equation must be written as a system of **first-order differential equations**. Starting with:

$$
\ddot{\theta} = -\frac{g}{L} \sin(\theta)
$$

we define:

$$
u = \dot{\theta}
$$

This gives the system:

$$
\dot{u} = -\frac{g}{L} \sin(\theta)
$$

$$
\dot{\theta} = u
$$

Euler's method then proceeds in two steps:

1. Update the velocity:

   $$
   u(t + \Delta t) = u(t) - \frac{g}{L} \sin(\theta(t))\, \Delta t
   $$

2. Update the angle:

   $$
   \theta(t + \Delta t) = \theta(t) + u(t + \Delta t)\, \Delta t
   $$
