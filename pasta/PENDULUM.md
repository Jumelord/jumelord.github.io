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

# Métodos Numéricos

## Método de Euler

A expansão em taylor nos permite escrever a maioria das funções como uma soma de potências. Se x é um ponto no domínio da função e a é um ponto conhecido, podemos escrever f(x) como:

$$f(x) = f(a) + f^'(a)(x-a) + f^{''}(a)(x-a)²/2! ...$$

Para um problema de valor inicial, sabemos $$f(t)$$ e queremos calcular $$f$$ um periodo de tempo adiante, em $$t + \Delta t$$. Dessa forma, tomamos $$x = t + \Delta t$$, e a = t.

$$f(t + \Delta t) = f(t) + f^' (t)\Delta t + f^{''}(t)\Delta t^2/2! ...$$





