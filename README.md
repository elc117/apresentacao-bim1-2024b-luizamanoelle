# Introdução à List Comprehension em Haskell

Em Haskell, a **List Comprehension** é uma forma de gerar uma nova lista a partir de uma lista existente, usando notação que lembra bastante a matemática. Ela é inspirada na [notação de construção de conjuntos](https://en.wikipedia.org/wiki/Set-builder_notation), permitindo que você crie listas aplicando transformações ou filtrando valores.

## Sintaxe Básica
A estrutura de uma List Comprehension segue a seguinte forma:
```
[<expressão> | <geradores>, <filtros>]
```
 - Expressão: a transformação que será aplicada aos elementos.
 - Geradores: de onde os valores serão retirados.
 - Filtros: condições que os elementos precisam satisfazer.
<aside>
💡 Isso significa: "Construa uma nova lista onde cada elemento é o resultado da expressão, usando valores gerados e filtrados."
 </aside>
 
### Exemplo: Comparação com Matemática
Podemos ilustrar isso com um exemplo simples da matemática:
$$
 { 2x | x ∈ {1, … , 5}}
$$

Em Haskell, a mesma ideia seria escrita assim:
```haskell
[n * 2 | n <- [1..5]]
-- Resultado: [2, 4, 6, 8, 10]
```
### Leitura da expressão
Como lemos essa expressão?
<aside>
💡 “Pegue cada `n` da lista `[1..5]`, multiplique por 2 e coloque o resultado em uma nova lista”
</aside>
- *O operador <- pode ser lido como "pertence a", indicando que n assume valores da lista [1..5]*

## Map: Um Breve Lembrete
A função map em Haskell é utilizada para aplicar uma transformação a cada elemento de uma lista. Sua sintaxe é:
```haskell
map função lista
map (*2) [1..5]

-- Resultado: [2, 4, 6, 8, 10]
```

## Comparando **List Comprehension** com **Map**
Tanto List Comprehension quanto map transformam listas com base em uma regra, mas há diferenças sutis entre as duas abordagens.

```haskell
>>> [2*x | x <- [1..10]]
[2,4,6,8,10,12,14,16,18,20]
>>> map (2*) [1..10]
[2,4,6,8,10,12,14,16,18,20]
```

**List Comprehension** é útil quando você tem múltiplos geradores e filtros. Ela é mais flexível para manipulações mais complexas. **Map**, por outro lado, é mais simples e direto quando o objetivo é apenas aplicar uma função a cada elemento da lista.

### Exemplo com filtro
Um dos grandes diferenciais da List Comprehension é a possibilidade de incluir filtros diretamente na expressão.
```haskell
[n * 2 | n <- [1..10], even n]
-- Resultado: [4, 8, 12, 16, 20]
```
Aqui estamos filtrando os números pares antes de aplicar a transformação. Podemos ler essa expressão assim:
<aside>
💡  "Pegue os números n da lista de 1 a 10, mantenha apenas os números pares (even n), e multiplique cada um deles por 2."
 - _ Os diferentes filtros são separador por virgula (",") _
</aside>
Para fazer isso com **map**, precisaríamos usar também a função **filter**:

```haskell
map (*2) (filter even [1..10])
-- Resultado: [4, 8, 12, 16, 20]
```

## Resumindo a Compreensão de Listas

List Comprehension não é nada mais do que uma forma de “amizade” entre map e filter, não precisando chamar as funções separadamente só aplicando requisitos.

```haskell
[f(x) | x <- list]
```
map a lista f 

```haskell
[ x | x <- list, P(x) ]
```
aplique filter na lista P

## Conclusão

- **List Comprehension** é mais expressiva e próxima da matemática, permitindo múltiplos geradores e filtros em uma sintaxe compacta.
- **map** é mais simples e direto para aplicar uma função a uma lista, mas para comportamentos mais complexos, `filter` e `map` precisam ser usados juntos.

Ambas têm seu lugar dependendo do contexto, mas para operações mais simples e diretas, `map` é geralmente preferido, enquanto **List Comprehension** brilha em casos que exigem mais controle e filtragem de dados.

### Referências:

- [McCullough's Teaching Notes on Haskell](http://www2.math.ou.edu/~dmccullough/teaching/f06-6833/haskell/map_filter.pdf)  
- [Haskell List Comprehension - EDUCBA](https://www.educba.com/haskell-list-comprehension/)  
- [List Comprehension e Map - Dalhousie University](https://web.cs.dal.ca/~nzeh/Teaching/3137/haskell/standard_containers/list_comprehensions/map/)  
- [Compreensão de Lista no StackOverflow](https://pt.stackoverflow.com/questions/513808/o-que-%C3%A9-compreens%C3%A3o-de-lista-estrutura-de-controle-loop)  
- [Vídeo sobre List Comprehension em Haskell](https://www.youtube.com/watch?v=oq7-RPLp3sI)
