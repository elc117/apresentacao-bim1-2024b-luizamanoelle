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
💡  “Pegue cada `n` da lista `[1..5]`, multiplique por 2 e coloque o resultado em uma nova lista”
</aside>

  > **Obs:** O operador `<-` pode ser lido como "pertence a", indicando que `n` assume valores da lista `[1..5]`.

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
</aside>

  > **Obs:** Diferentes filtros em uma List Comprehension são separados por vírgulas (`,`), permitindo aplicar várias condições simultaneamente.

Para fazer isso com **map**, precisaríamos usar também a função **filter**:

```haskell
map (*2) (filter even [1..10])
-- Resultado: [4, 8, 12, 16, 20]
```
### Exemplo com Múltiplos Geradores
Com List Comprehension, você também pode trabalhar com mais de um gerador. Aqui está um exemplo onde criamos pares combinando dois conjuntos de valores:

```haskell
[(x, y) | x <- [1, 2], y <- [3, 4]]
-- Resultado: [(1, 3), (1, 4), (2, 3), (2, 4)]
```
<aside>
💡 "Pegue cada x da lista [1, 2], e para cada x, pegue cada y da lista [3, 4] para formar todos os pares possíveis."
</aside>

*Isso nos dá uma lista com todas as combinações de x e y daquelas listas. Usando múltiplos geradores, você pode criar combinações de valores de diferentes fontes.*

Para obter o mesmo resultado usando map, você pode combinar a função concatMap com uma função lambda. A função concatMap aplica uma função que retorna uma lista e, em seguida, concatena todas essas listas em uma única lista.
```haskell
concatMap (\x -> map (\y -> (x, y)) [3, 4]) [1, 2]
-- Resultado: [(1, 3), (1, 4), (2, 3), (2, 4)]
```
_Explicação do Código_
 * concatMap: Itera sobre cada elemento da lista [1, 2].
 * map (\y -> (x, y)) [3, 4]: Para cada x, ele mapeia os elementos de [3, 4] criando tuplas (x, y).
O resultado será a concatenação de todas as listas de tuplas geradas, resultando em [(1, 3), (1, 4), (2, 3), (2, 4)].

## Possíveis Erros em List Comprehension

Ao trabalhar com **List Comprehension** em Haskell, alguns erros comuns podem surgir, principalmente relacionados à sintaxe e à lógica dos geradores, expressões e filtros. Aqui estão alguns erros possíveis e como evitá-los:

 1. Erro de Sintaxe
A **List Comprehension** tem uma sintaxe muito específica, e qualquer erro na formatação pode resultar em falhas de compilação. Um exemplo comum é esquecer os colchetes `[]` ao redor da expressão.

**Exemplo de erro**:
```haskell
x | x <- [1..5]  -- Sem colchetes

[x | x <- [1..5]]  -- Correto
```
 2. Tipos Incompatíveis
Haskell é uma linguagem fortemente tipada, então é importante garantir que os tipos da expressão, geradores e filtros sejam compatíveis. 
**Exemplo de erro**:
```haskell
[ x + "a" | x <- [1..5] ]  -- Tenta somar número com string
```
 3. Filtros Malformados
Se o filtro usado não for uma expressão booleana válida, Haskell não saberá como lidar com ele.
```haskell
[ x | x <- [1..5], x + 1 ]  -- Filtro inválido (não é uma condição booleana)
[ x | x <- [1..5], x > 2 ]  -- Correto
```
 4. Geradores Vazios
Se a lista gerada por um dos geradores for vazia, o resultado final da List Comprehension será uma lista vazia. Esse comportamento pode ser inesperado quando há múltiplos geradores.

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
