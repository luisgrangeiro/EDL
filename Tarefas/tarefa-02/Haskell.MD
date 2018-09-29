# A linguagem de programação Haskell

Haskell é uma linguagem de programação funcional, de tipagem estática e implícita.
## Origem
 No fim dos anos 80, durante a conferência de Linguagens de Programação Funcionais e Arquitetura de Computadores, foi discutido a questão da existência de uma grande quantidade de linguagens de programação funcional, mas poucas possuiam um bom projeto. Naquela época somente a linguagem Miranda era comercial e madura o suficiente para ser usada em produção.
Decidiu-se, então durante a conferência, que uma comissão seria formada para projetar uma nova linguagem que unificasse as melhores práticas de projeto de linguagem e implementasse as técnicas funcionais que eram discutidas na época. Para isso, em vez de começar uma linguagem do zero, elegeram Miranda como base para o projeto. 
A versão 1.0 dessa nova linguagem foi liberada em 1990 e foi batizada de Haskell.

## Classificação
Haskell é uma linguagem de programação puramente funcional. Diferentemente da programação imperativa, o paradigma funcional trata a computação com aplicação de funções e imutabilidade de dados. A imutabilidade de dados, significa que não existe alteração de estado, por exemplo uma função sempre irá retornar o mesmo valor X para uma mesma entrada Y, não existe a possibilidade de a função receber o parâmetro Y e retornar o valor Z.


### Lazy Evaluation
Uma das principais características de Haskell é a possibilidade de usar uma forma de avaliação chamada de avaliação preguiçosa (ou atrasada). Isso significa que expressões são avaliadas apenas se e quando seus valores forem necessários. Ou seja, se uma função tem dois parâmetros, mas em uma execução em particular o primeiro não é usado, ele não será avaliado. Além disso, se apenas uma parte de um parâmetro deve ser avaliado, a parte restante é deixada sem avaliação.
Com isso, a avaliação preguiçosa permite a definição de estruturas de dados infinitas. Por exemplo:

```haskell
Positives = [0..]
```
Essa expressão define uma lista infinita e, mesmo que um computador não possa representar todos os números dessa lista, a avaliação preguiçosa garante que essa expressão não será avaliada até que seja necessário e, assim, não necessitando dos recursos do computador para representar cada número dessa lista.
Agora digamos que desejamos verificar se o número 100 está contido nessa lista. Então fazemos o seguinte:
```haskell
100 `elem`positives
```
Com isso, temos o valor **True** retornado, significando que o núemro inteiro 100 está contido na lista positives, sendo que a lista só é avaliada até o número 100 ser encontrado.


## Bibliografia
---
* (SEBESTA, Robert W.) - Conceitos de linguagens de programação
* Haskell (Linguagem de Programação) - Wikipédia, a enciclopédia livre: https://pt.wikipedia.org/wiki/Haskell_(linguagem_de_programa%C3%A7%C3%A3o)
* Haskell Básico - A História: https://marceloparrela.wordpress.com/2013/11/01/haskell-a-historia/
* Haskell em 10 minutos - HaskellWiki: https://wiki.haskell.org/Haskell_em_10_minutos
