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
\dot{\vec{r}} = L \dot{\hat{\theta}}
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

## Numerical Methods

### Euler's Method

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

### Applying the Method to Our Problem

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
   
> **Note:** One could use \\( u(t) \\) instead of \\( u(t + \Delta t) \\) in the second update step, and this would still be consistent with Euler’s method. However, using the most recently updated value makes the method slightly more robust in practice.  
> Moreover, when \\( \Delta t \\) is small, we have \\( u(t + \Delta t) \approx u(t) \\), so the difference is not significant.

## Godot Setup

Para performar essa simulação no **Godot**,
* Criar uma cena 3D
* Adicionar uma câmera
* Adicionar um Nó 3D que será o pênduo
* Adicionar um mesh com forma de cilindro para a aste dentro do nó do Pendulo
* Mover a o cilindro verticalmente para baixo até a sua ponta de cima ficar no centro do Nó do Pendulo
* Adicionar um mesh com forma de esfera para a massa do Pendulo
* Adicionar um script à raiz da cena 3D
* (Opcional) Adicionar um ambiente
  
![Godot Pendulum Setup](../pics/pendulum_setup.png)

## Godot Scripting

### Variables

O código do godot é muito semelhante ao Python, mas possui algumas peculiaridades. Para definir uma variável escrevemos var nome_da_variavel = valor_da_variavel. QUando escrevemos dessa maneira, o tipo da variável já é definido como o tipo do valor que colocamos.

Agora abrimos o código e começamos a criar as variáveis que vamos utilizar. Nesse caso criamos uma variável para o \Delta t, \theta, \dot{\theta}, gravidade, e comprimento, nomeadas respectivamente como dt, theta, dtheta, g, e L. Essa variáveis não são parâmetros de qualquer objeto do Godot, mas vamos vincular elas as propriedades físicas depois.

extends Node3D

var dt = 0.01
var theta = 1.4
var dtheta = 0
var g = -9.8
var L = 1

O extends Node3D não é uma variável, mas ele é mandatório para executar o código pois determina o tipo do objeto do nó raiz.

### Euler Method

Nosso objetivo aqui não é resolver uma equação diferencial com o maximo de precisão, mas sim de maneira visualmente atraente e fisicamente compatível. Assim sendo, vamos fazer o Godot achar novos valores para \theta a cada frame. Para isso, vamos utilizar a função _physics_process(delta) que é executada a cada frame.

Aplicando as equações que obtemos anteriormente no código obtemos isso.

func _physics_process(delta: float) -> void:
  dtheta += g*sin(theta)/L*dt
  theta += dtheta*dt
  $Pendulum.rotation.z = theta

As linhas 2 e 3 são exatamente as equações que discutimos antes, enquanto que na linha 4 estamos atualizando a rotação do objeto pendulo no eixo z utilizando a variável theta.

Colocando o Godot para executar a simulação, já devemos observar que o pêndulo em movimento.

### Correção Temporal

Se você alterar o valor do time-step, você deve perceber que isso afeta a velocidade do pêndulo. Isso pode parecer estranho, pois o time-step não é um parâmetro físico. Contudo, devemos levar em conta que não existe uma relação tão clara entre o tempo da simulação, e o tempo que observamos (Qualquer semelhança com a relatividade é mera coincidencia.). Se o seu time-step é de 0.1, e a física do simulador é iterada 60 vezes por segundo, então a simulação vai ser 6 vezes mais rápido do que você veria na realidade.

Há duas formas de ajustar isso. A primeira consiste em utilizar o parâmetro delta que recebemos do _physics_process. Esse parâmetro retorna um valor 1/FPS, ou seja se definimos dt = delta, a cada segundo vamos ter dt * FPS = 1/FPS * FPS = 1 segundos de simulação por segundos reais, o que resolve nossos problemas com o preço da precisão ser limitada.

func _physics_process(delta):
  dt = delta
  dtheta += g*sin(theta)/L*dt
  theta += dtheta*dt
  $Pendulum.rotation.z = theta

A segunda maneira é tentar forçar o Godot a aumentar a velocidade de processamento. Isso permite você aumentar a precisão até o limite em que seu computador aguentar. Para isso utilizamos a função _ready() que é chamada assim que a simulação inicializa, e alteramos o número de iterações por segundo para 1/dt, assim 
temos que dt * FPS = dt * 1/dt = 1 segundos de simulação por segundos reais.

func _ready():
	Engine.physics_ticks_per_second = 1/dt

