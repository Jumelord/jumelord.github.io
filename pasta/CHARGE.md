---
title: "Physics Simulators"
layout: default
---

<style>
.site-header {
  display: none;
}
</style>


<head>
<style>
a {
  color: #59b390;
  text-decoration: none;
}
a:hover {
  color: #006400;
  text-decoration: underline;
}
</style>
</head>

<!-- Enables MathJax -->
<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

# 2D Electromagnetism

O eletromagnetismo em duas dimensões é reescrito de maneira análoga ao modelo tridimensional, mas as leis e equações são ainda diferentes. Desa forma, o conteúdo aqui presente conta com uma modelagem numérica das equações de Maxwell para simular o movimento de cargas pontuais, o campo elétrico e magnético no espaço. Assim, todo o modelo teórico das equações de Maxwell reescritas para um mundo bidimensional foram baseado no artigo "On Maxwell’s electrodynamics in two spatial dimensions", enquanto o modelo computacional é próprio. Enquanto que a teoria por de trás equações pode ser um pouco complicada, a aplicação nessa simulação exige apenas o conhecimento básico de equações diferencias, e a dificuldade na implementação é progressiva.

## Cargas Pontuais e o campo eletrico

### Lei de Gauss

Em duas dimensões a lei de gauss toma uma forma semelhante, mas tanto a densidade de carga quanto o divergente devem ser feitos também em duas dimensões.

$$
\vec{E} = (E_x, E_y)
$$

$$
\nabla \equiv \frac{\partial E_x}{\partial x} + \frac{\partial E_y}{\partial y}
$$

$$
\rho(x,y) = \frac{dq}{dA}
$$

A lei de Gauss se torna:

$$
\nabla \cdot \vec{E} = \frac{\rho}{\epsilon_o}
$$

A densidade de carga de uma carga pontual pode ser modelada como uma função generalizada, chamda de delta de dirac, que depende apenas da posição, e retorna um valor nulo em qualquer ponto do espaço, exceto na origem, aonde retorna infinito.

$$
\delta(\vec{r}) = 
\begin{cases}
\inf & \text{if } r \neq 0 \\
0             & \text{if } r = 0
\end{cases}
$$

$$
\rho(\vec{r}) = q\delta(\vec{r})
$$

A partir disso podemos deduzir como será o campo elétrico de uma carga pontual. Integrando os dois lados em uma área circular centrada em nossa carga potual, e utilizando o teorema de Gauss em duas dimensões para transformar a integral de area em uma integral de caminho ao longo da circunfência, obtemos uma expressão fechada para o campo de nossa carga.

$$
\int \int_C \nabla \cdot \vec{E} dA = \frac{\int \int_C \rho dA}{\epsilon_o} 
$$

$$
\oint_\partial C \vec{E} \cdot \hat{n} dr  = \frac{\int \int_C q\delta(\vec{r}) dA}{\epsilon_o} 
$$

$$
E \oint_\partial C dr  = \frac{q}{\epsilon_o} 
$$

$$
E (2 \pi |r|)  = \frac{q}{\epsilon_o} 
$$

$$
E = \frac{q}{2 \pi \epsilon_o |r|} 
$$
