---
layout: post
title: Python 101 - Practice what you know
categories: 
 - python
---

> You know nothing Jon Snow - Ygritte

Summary:

1. [First program in Python](#primeiro-programa)
1. [Variables](#variáveis)
1. [Tuples](#tuples)
1. [Nesting](#nesting)
1. [Slicing](#slicing)
1. [List](#list)

Atualmente estou aprendendo Python para utilizar em minhas aplicações porque acabei gostando da linguagem e da facilidade de conseguir fazer muita coisa com pouco código. Algo que me atraiu muito é a quantidade de bibliotecas para Data Science, a quantidade de documentação e a quantidade de biblioteca open source. Pode ser que algo que eu fale nessa série de artigos esteja incorreto ou falte algum complemento, então sinta-se livre para comentar abaixo e dar uma ajuda.

Como iremos praticar o que sabemos sobre Python se sabemos nada? Irei abordar os primeiros dois tópicos do [Backend Developer Roadmap](https://roadmap.sh/backend). Primeiro precisamos saber o básico. O que é o básico? Recomendo fazer o [30 days of code do Hacker Rank](https://www.hackerrank.com/domains/tutorials/30-days-of-code) porque ele aborda conteúdos básicos em Java como: Variáveis, Tipos, Métodos, Funções, Objetos, Interfaces, Listas, Arrays, Recursão, Pilhas, Filas, Árvores e Grafos, ou seja, ele aborda tudo que tu precisa saber que existe em qualquer linguagem de programação e já te ensina um pouco de lógica de programação. Eles aproveitam e ensinam também como manipular dados, o que é orientação a objetos e estrutura de dados, entre outras coisas. Agora você deve estar se perguntando: "Por que está dizendo para fazer um curso em Java se está escrevendo sobre Python?". Na programação importa muito aprender os conceitos que irá aprender no 30 days of code. Esses conceitos são usados para todas as linguagens de programação e a lógica que irá aprender a usar também é utilizada em qualquer linguagem. Então sim, vale a pena fazer o 30 days of code.

Aqui irei abordar alguns conceitos básicos de Python, também irei trabalhar alguns algoritmos e farei um projeto comentando o desenvolvimento dele. O projeto será um jogo da cobra no console.

Só vamos.

## Pré requisitos

- Python 3.6+
- Editor de texto (eu estou utilizando o Visual Studio Code, mas pode ser qualquer um)

## Primeiro programa

Normalmente quando estamos aprendendo uma linguagem de programação sempre fazemos um Hello World de começo.

Crie um arquivo com .py na extensão e digite:

```python
    print("Hello World")
    print("The WOOORLD")
    print("WRYYYY")
```

agora para executar? Para executar o programa é muito simples. Basta executar:

```bash
    python .\nomedoarquivo.py
```

e tu vai ver que no terminal ele irá imprimir as frases.

O comando print imprime no console o que está dentro dele em formato de texto.

No python tu não tem um padrão básico de inicialização de programa que nem no Java ou no C# que tu precisa começar pelo método main. No Python tu orienta pelo escopo que é definido pela indentação do arquivo, mais tarde iremos ver sobre isso.

Agora tu já sabe executar o seu primeiro programa em Python.

## Variáveis

Pelo que eu entendi Python não é uma linguagem fortemente tipada em certos casos. Por exemplo, quando temos uma variável int podemos atribuir um valor de string nela e ela terá seu tipo alterado para string, ou seja, sempre que atribuirmos um novo valor a variável irá receber seu tipo e seu valor.

Contudo, sempre temos que cuidar quando formos fazer alguma alteração nessas variáveis porque pode ser que o tipo não possibilite a operação.

Exemplo de variável:

```python
    a = 1
    a = "Rafael"
    print(type(a))
    a = 1
    print(type(a))
    a = (1, 2, 3)
    print(type(a))
    a = 2
    print(type(a))
```

Linguagens tipadas como C#, tu precisa dizer qual vai ser o tipo daquela variável e o tipo só poderá ser trocado ao fazer um cast atribuindo ela a uma variável do tipo desejado (não sei ao certo se dá para fazer de outra maneira. Se houver, manda para mim que eu gostaria de aprender). Exemplo:

```csharp
    string s = "123";
    int a = (int)s;
```

[Documentação do Python sobre tipos](https://docs.python.org/3/library/stdtypes.html)

[Basic Data Types in Python](https://realpython.com/python-data-types/)

### Tuples

Tuples são valores ordenados e **imutáveis**. 

Podem conter qualquer tipo de dado dentro de uma tupla, ou seja, tu pode ter tanto valores inteiros, floats quanto strings.

Como instanciar uma Tuple:

```python
    tuple = (1, 2, 3, 4, 5)
    tuple1 = tuple + ("Rafael", "William")
    tuple1
    #Retorno: (1, 2, 3, 4, 5, "Rafael", "William")
```

acessando o valor de uma tuple:

```python
    tuple[0]
```

Para adicionar um valor a uma tupla, tu vai ter que criar uma nova e concatenar seus valores porque elas são imutáveis.

### Nesting

É agregar outros tipos de dados complexos dentro de um, ou seja, adicionar uma tuple dentro de uma tuple.

```python
    tuple1 = (1, 2, ("Rafael", "William"), ("Zelda", 23.5))
```

Agora como acessamos seus valores?

Os indexes dos normais continuam iguais, mas o das nested são como se tu fosse acessar os valores de uma tuple dentro de uma tuple. Exemplo:

```python
    tuple1 = (1, 2, ("Rafael", "William"), ("Zelda", 23.5))
    #indexes: 0, 1,           2,                   3
    
    tuple1[0]
    #Retorno: 1
    
    tuple1[2]
    #Retorno: ("Rafael", "William")
    #indexes:     0,         1
    
    tuple1[2][0]
    #Retorno: "Rafael"
```

### Slicing

Slicing funciona com qualquer valor, tu consegue manipular seus dados pelos indexes e suas posições, sempre retorna uma nova instância com os dados que tu quer. Exemplo:

```python
    tuple1[0:3]
    #Retorno: (1, 2, ("Rafael", "William"))
    
    word = "banana"
    word[::-1]
    #Retorno: "ananab"
```

### List

Listas são **mutáveis**

São sequências ordenadas. Instanciadas com [ ]

```python
    list = ["Naruto", "Sasuke", "Sakura"]
    list
    #Retorno: ["Naruto", "Sasuke", "Sakura"]
```

Podemos utilizar Nesting e Slicing  que nem nas tuples.

Modo de acessar é igual ao da tuple.

Diferença é que como são mutáveis, tu pode adicionar e remover os elementos da mesma lista sem ter que criar uma nova instância sem aquele elemento.

[What is the difference between Python's list methods append and extend?](https://stackoverflow.com/questions/252703/what-is-the-difference-between-pythons-list-methods-append-and-extend)

Adicionando um elemento na lista:

```python
    list.extend(["Kakashi", "Jiraya"])
    list
    #Retorno: ["Naruto", "Sasuke", "Sakura", "Kakashi", "Jiraya"]
```