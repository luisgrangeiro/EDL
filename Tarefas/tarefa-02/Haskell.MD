# A linguagem de programação Haskell

Haskell é uma linguagem de programação funcional, de tipagem estática e implícita.
## Origem
 No fim dos anos 80, durante a conferência de Linguagens de Programação Funcionais e Arquitetura de Computadores, foi discutido a questão da existência de uma grande quantidade de linguagens de programação funcional, mas poucas possuiam um bom projeto. Naquela época somente a linguagem Miranda era comercial e madura o suficiente para ser usada em produção.
Decidiu-se, então durante a conferência, que uma comissão seria formada para projetar uma nova linguagem que unificasse as melhores práticas de projeto de linguagem e implementasse as técnicas funcionais que eram discutidas na época. Para isso, em vez de começar uma linguagem do zero, elegeram Miranda como base para o projeto. 
A versão 1.0 dessa nova linguagem foi liberada em 1990 e foi batizada de Haskell.

## Classificação
Haskell é uma linguagem de programação puramente funcional. Diferentemente da programação imperativa, o paradigma funcional trata a computação com aplicação de funções e imutabilidade de dados. A imutabilidade de dados, significa que não existe alteração de estado. Por exemplo, uma função sempre irá retornar o mesmo valor X para uma mesma entrada Y, não existe a possibilidade de a função receber o parâmetro Y e retornar o valor Z.

O Haskell possui um sistema de tipagem estática. Sendo assim, o tipo de cada expressão é conhecido na hora da compilação e isso tem como benefício um código mais seguro, já que se tentarmos dividir um tipo booleano por um número inteiro, o código nem irá compilar.
Haskell possui também inferência de tipo. Assim, se digitarmos um valor, True, por exemplo, ele conseguirá identificar que é um tipo booleano. Existe um comando em Haskell que ao ser executado e passando um valor, irá retornar o tipo da expressão digitada. Esse comando é o :t.

```haskell
ghci> :t True
True :: Boll
```

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

## Expressividade
Boa parte do poder de expressividade de Haskell pode ser conferido através do conceito de compreensão de listas.
Compreensão de lista é uma construção sintática para criação de uma lista baseada em listas existentes. 

Por exemplo, uma compreensão de conjunto S= { 2.x | x  Є N, x ≤ 10 }
Que define o conjunto que contém o dobro de cada um dos números naturais de 1 a 10
Pode ser expressa em Haskell da seguinte forma:
```haskell
[x * 2 | x <- [1..10]]
```

Se quisermos criar uma função que retorna o dobro de cada elemento de uma lista pode ser feito da seguinte forma:
```haskell
doublesList xs = [x*2 | x <- xs]

doublesList [1..10]
```
Ess código define a função doublesList que recebe xs como parâmetro e para cada x em xs, será retornado o dobro de x.
Executando a função passando a lista [1..20] irá retornar a seguinte lista:
[2,4,6,8,10,12,14,16,18,20]

Comparando com C#, podemos ver que seria necessário criar métodos e declarar tipos de retorno, como é visto no código a seguir:
```cs
public List<int> DoublesList(List<int> list) {
        var list2 = new List<int>();
            
        list.ForEach(x => { list2.Add(x * 2); });

        return list2;
}
```
Assim definimos um método que recebe uma lista como entrada, faz um loop dobrando cada elemento e adiciona na lista que será retornada.
Para criar a lista de entrada e chamar o método fica da seguinte forma:
```cs
var list = new List<int>();
list.AddRange(new int[]{ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10});
var result = DoublesList(list);
```
Vemos que é necessário digitar cada elemento da lista.

## Bibliografia
---
* (SEBESTA, Robert W.) - Conceitos de linguagens de programação
* Haskell (Linguagem de Programação) - Wikipédia, a enciclopédia livre: https://pt.wikipedia.org/wiki/Haskell_(linguagem_de_programa%C3%A7%C3%A3o)
* Haskell Básico - A História: https://marceloparrela.wordpress.com/2013/11/01/haskell-a-historia/
* Haskell em 10 minutos - HaskellWiki: https://wiki.haskell.org/Haskell_em_10_minutos
* Haskell Tailor Fontela: http://haskell.tailorfontela.com.br
