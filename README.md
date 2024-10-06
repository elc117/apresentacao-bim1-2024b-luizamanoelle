### Introdução

Em Haskell, a **List Comprehension** é uma forma de gerar uma nova lista a partir de uma lista existente, usando notação que lembra bastante a matemática. Ela é inspirada na [notação de construção de conjuntos](https://en.wikipedia.org/wiki/Set-builder_notation), permitindo que você crie listas aplicando transformações ou filtrando valores.

### Sintaxe

```
[<expressão> | <geradores>, <filtros>]
```

### Exemplo:

Em matemática temo:

$$
 { 2x | x ∈ {1, … , 5}}
$$

```haskell
[n * 2 | n <- [1..5]]
```

Como lemos isso?

<aside>
💡

“pegue cada `n` da lista `[1..5]`, multiplique por 2 e coloque o resultado em uma nova lista”
** a seta indica os valores que vamos gerar para n**

</aside>

Resultado:

```haskell
[2, 4, 6, 8, 10]
```

## Relembrando map…

### sintaxe

```haskell
map função lista
map (*2) [1..5]

-- Resultado: [2, 4, 6, 8, 10]
```

## Comparando **List Comprehension** com **Map**

 Ambos transformam listas de acordo com uma regra:

```haskell
>>> [2*x | x <- [1..10]]
[2,4,6,8,10,12,14,16,18,20]
>>> map (2*) [1..10]
[2,4,6,8,10,12,14,16,18,20]
```

**List Comprehension** é útil quando você tem múltiplos geradores e filtros. Ela é mais flexível para manipulações mais complexas. **Map**, por outro lado, é mais simples e direto quando o objetivo é apenas aplicar uma função a cada elemento da lista.

### Exemplo

```haskell
[n * 2 | n <- [1..10], even n]
-- Resultado: [4, 8, 12, 16, 20]
```

Tradução:

- n * 2 = expressão
- n <- [1..10] = gerador mais filtro
- even n = outro filtro, separado por “ , “. *A função `even n` retorna `True` se `n` for par, ou seja, somente números pares serão considerados.*

"Pegue os números `n` da lista de 1 a 10, mantenha apenas os números pares, e multiplique cada um deles por 2 para construir uma nova lista."

Para fazer isso com **map**, precisaríamos usar também a função **filter**:

```haskell
map (*2) (filter even [1..10])
-- Resultado: [4, 8, 12, 16, 20]
```

### Resumindo:

Lista por compressão não é nada mais do que uma forma de “amizade” entre map e filter, não precisando chamar as funções separadamente só aplicando requisitos.

```haskell
[f(x) | x <- list]
```

map a lista f 

```haskell
[ x | x <- list, P(x) ]
```

aplique filter na lista P

### Conclusão

- **List Comprehension** é mais expressiva e próxima da matemática, permitindo múltiplos geradores e filtros em uma sintaxe compacta.
- **map** é mais simples e direto para aplicar uma função a uma lista, mas para comportamentos mais complexos, `filter` e `map` precisam ser usados juntos.

Ambas têm seu lugar dependendo do contexto, mas para operações mais simples e diretas, `map` é geralmente preferido, enquanto **List Comprehension** brilha em casos que exigem mais controle e filtragem de dados.

### Referências:

http://www2.math.ou.edu/~dmccullough/teaching/f06-6833/haskell/map_filter.pdf

https://www.educba.com/haskell-list-comprehension/

https://web.cs.dal.ca/~nzeh/Teaching/3137/haskell/standard_containers/list_comprehensions/map/

[https://pt.stackoverflow.com/questions/513808/o-que-é-compreensão-de-lista-estrutura-de-controle-loop](https://pt.stackoverflow.com/questions/513808/o-que-%C3%A9-compreens%C3%A3o-de-lista-estrutura-de-controle-loop)

https://www.youtube.com/watch?v=oq7-RPLp3sI
