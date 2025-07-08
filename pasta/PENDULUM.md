<!-- Adiciona MathJax -->
<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

O pêndulo é um dos sistemas mecânicos mais simples. Contudo, o termo não linear na sua equação do movimento dificulta os cálculos, e sua resolução exata não pode ser encontrada analíticamente. Uma maneira de estudar o comportamento desse sistema é por meio do cálculo numérico.
Aqui vou utilizar o método de Euler, talvez o mais simples algorítmo de resolução de equações diferenciais, para resolver pêndulo utilizando o programa Godot.


---
# Formulação do Problema

O problema consiste de uma barra de massa desprezível e comprimento *L*, com uma das pontas presa a um eixo, e outra ponta presa a uma massa *m*, formando um ângulo $$\theta$$ com a vertical. Além disso, a massa é forçada pela força da gravidade que aponta para baixo.

O fato da massa estar vinculada a barra faz com que a força resultante da massa na direção que aponta para a barra é zero, e portanto devemos tratar apenas da componente angular da força.

Essa componente é dada pela seguinte equação:

$$ F_{\theta} = -sin(\theta)mg $$

A partira da segunda lei de Newton obtemos a equação do movimento.

$$F = m \ddot{r} = -sin(\theta)mg$$

$$\ddot{r} = -sin(\theta)g$$

Podemos utilizar a geometria do sistema para expressar r em termos de $\theta$.

$$r = L \theta$$

Portanto:

$$L\ddot{\theta} = -sin(\theta)g$$
$$\ddot{\theta} = -sin(\theta)g/L$$


