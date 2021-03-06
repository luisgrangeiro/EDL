# A linguagem de programação Haskell

Haskell é uma linguagem de programação funcional, de tipagem estática e implícita.
## Origem
 No fim dos anos 80, durante a conferência de Linguagens de Programação Funcionais e Arquitetura de Computadores, foi discutido a questão da existência de uma grande quantidade de linguagens de programação funcional, mas poucas possuiam um bom projeto. Naquela época somente a linguagem Miranda era comercial e madura o suficiente para ser usada em produção.
Decidiu-se, então durante a conferência, que uma comissão seria formada para projetar uma nova linguagem que unificasse as melhores práticas de projeto de linguagem e implementasse as técnicas funcionais que eram discutidas na época. Para isso, em vez de começar uma linguagem do zero, elegeram Miranda como base para o projeto. 
A versão 1.0 dessa nova linguagem foi liberada em 1990 e foi batizada de Haskell.


Na linha do tempo abaixo podemos ver a origem de Haskell vinda de Miranda, que por sua vez teve influências de ML e Lisp.
![Haskell](/Tarefas/tarefa-02/img/lps.jpg)

## Classificação
Haskell é uma linguagem de programação puramente funcional. Diferentemente da programação imperativa, o paradigma funcional trata a computação com aplicação de funções e imutabilidade de dados. A imutabilidade de dados, significa que não existe alteração de estado. Por exemplo, uma função sempre irá retornar o mesmo valor X para uma mesma entrada Y, não existe a possibilidade de a função receber o parâmetro Y e retornar o valor Z.

O Haskell possui um sistema de tipagem estática. Sendo assim, o tipo de cada expressão é conhecido na hora da compilação e isso tem como benefício um código mais seguro, já que se tentarmos dividir um tipo booleano por um número inteiro, o código nem irá compilar.
Haskell possui também inferência de tipo. Assim, se digitarmos um valor, True, por exemplo, ele conseguirá identificar que é um tipo booleano. Existe um comando em Haskell que ao ser executado e passando um valor, irá retornar o tipo da expressão digitada. Esse comando é o :t.

```haskell
ghci> :t True
True :: Bool
```

## Writability
Para tratar do conceito de Writability vamos comparar os dois códigos a seguir:

Haskell
```haskell
let shoppingList = ["Eggs", "Milk"]
```
Java
```java
ArrayList<String> shoppingList = new ArrayList<>();
shoppingList.add("Eggs");
shoppingList.add("Milk");
```
Nos dois casos definimos uma lista de string com dois elementos. No código em java, vemos que é necessário declarar que shoppingList é um ArrayList duas vezes e depois a atribuição dos elementos da lista é feita isoladamente.
Em Haskell, é possível perceber que na própria declaração da variável já é feita a atribuição da lista de string. 
Sendo assim, o código em Haskell sem declarações desnecessárias consegue definir uma lista de string.

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

### Lazy Evaluation
Uma das principais características de Haskell que mostra um pouco do seu poder de expressividade, é a possibilidade de usar uma forma de avaliação chamada de avaliação preguiçosa (ou atrasada). Isso significa que expressões são avaliadas apenas se e quando seus valores forem necessários. Ou seja, se uma função tem dois parâmetros, mas em uma execução em particular o primeiro não é usado, ele não será avaliado. Além disso, se apenas uma parte de um parâmetro deve ser avaliado, a parte restante é deixada sem avaliação.
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

### Pattern matching
O patttern matching é uma característica de linguagens funcionais que nada mais é que uma construção sintática que procura padrões em dados e, em caso de sucesso, faz algo com ele.

Quando definimos uma função, podemos definir um código específico para alguns padões esperados nos dados recebidos.

```haskell
numDaSorte :: (Integral a) => a -> String
numDaSorte 13 = "Você está com sorte !!"
numDaSorte x = "Opa, parece que você está com azar..."
```
No código acima, definimos uma função que recebe um valor a, que deve ser um número, e retorna uma string.
Na segunda linha definimos o primeiro padrão. Se o número recebido for 13, retornamos uma mensagem.
Na terceira linha definimos um padrão geral, ou seja, qualquer número que não seja 13, retornará aquela mensagem.

Em linguagens não funcionais, esse código poderia ser construído com a utilização do if/else como podemos observar em java.

```java
public string NumeroDaSorte(int a){
	if(a == 7){
		return "Você está com sorte !!"
	} else {
		return "Opa, parece que você está com azar..."
	}
}
```

Usando o pattern matching para o cálculo do número fatorial:

```haskell
factorial :: (Integral a) => a -> a  
factorial 0 = 1  
factorial n = n * factorial (n - 1) 
```


Na linguagem C ficaria assim:
```c 
#include<stdio.h>

int fat, n;

int main()
{
  scanf("%d", &n) ;
  for(fat = 1; n > 1; n = n - 1)
  {
      fat = fat * n;
  }
  printf("\n%d", fat);
  return 0;
}
```

##### Concluindo
Se tratando de expressividade, vemos que a maior diferença se trata na criação de listas infinitas, que não é possível expressar em C ou Java. Em outras construções é possível expressar tanto em haskell quanto nas outras linguagens, mas fica claro que em haskell o código fica menor, muito mais simples e legível.


## Bibliografia
---
* (SEBESTA, Robert W.) - Conceitos de linguagens de programação
* Haskell (Linguagem de Programação) - Wikipédia, a enciclopédia livre: https://pt.wikipedia.org/wiki/Haskell_(linguagem_de_programa%C3%A7%C3%A3o)
* Haskell Básico - A História: https://marceloparrela.wordpress.com/2013/11/01/haskell-a-historia/
* Haskell em 10 minutos - HaskellWiki: https://wiki.haskell.org/Haskell_em_10_minutos
* Haskell Tailor Fontela: http://haskell.tailorfontela.com.br
