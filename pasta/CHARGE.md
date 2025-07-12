
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
\Nabla \equiv \frac{\partial E_x}{\partial x} + \frac{\partial E_y}{\partial y}
$$
$$
\rho(x,y) = \frac{dq}{dA}
$$
$$
\Nabla \bullet \vec{E} = \frac{\rho}{\epsilon_o}
$$
