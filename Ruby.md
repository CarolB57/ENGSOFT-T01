
#### 1) Laço de repetição for:

Em C:

```C
for(int i = 0; i < 5; i++) {
  // faz algo
}
```

vira

```ruby
5.times do
  # faz algo
end
```

Um loop não está sendo criado, e sim uma mensagem mensagem está sendo enviada a `.times` para o objeto `5`**. Guarde essa ideia. Funções não são chamadas, e sim "mensagens são enviadas para objetos".

#### 2) Sintaxe e Variáveis:

- Variáveis em Ruby são dinamicamente tipadas;
- Nomes de variáveis usam `snake_case` (ex: `minha_variavel`). Nomes de Classes usam `CamelCase` (ex: `MinhaClasse`).

```ruby
numero = 10 
mensagem = "Olá, mundo!"
```

#### 3) Objetos e Métodos:

Todo **valor** é um **objeto de uma classe**. E objetos respondem a "mensagens", que são os **métodos**.

```ruby
puts 10.class # => Integer (O número 10 é um objeto da classe Integer) 
puts "olá".class # => String (O texto "olá" é um objeto da classe String) 
puts 3.14.class # => Float 

# Enviando mensagens (chamando métodos) para esses objetos: 
puts "olá".upcase # => "OLÁ" (Enviando a mensagem .upcase para o objeto "olá") 
puts 120.even? # => true (Perguntando ao objeto 120 se ele é par)
```

Pense nos métodos como funções que já "vivem" dentro dos dados.

#### 4) Arrays e Hashes (Listas e Dicionários)

- **Array**: Uma lista ordenada de objetos. Muito parecido com as listas de Python.
- **Hash**: Um dicionário de pares `chave => valor`. Equivalente ao `dict` de Python.

```ruby
# Array
numeros = [10, 20, 30, 40]
puts numeros[0]       # => 10
numeros << 50         # Adiciona 50 ao final do array. O '<<' é um método!

# Hash
usuario = { "nome" => "Ana", "idade" => 25 }
puts usuario["nome"]  # => "Ana" | nome é uma string

# Em Ruby, é mais comum usar Símbolos (com :) como chaves de Hash por performance.
usuario_moderno = { nome: "Ana", idade: 25 }
puts usuario_moderno[:nome] # => "Ana" | nome é um símbolo
```

###### **Algumas observações:**

**1. Notação com "Hash Rocket" (`=>`)**

```ruby
usuario = { "nome" => "Ana", "idade" => 25 }
```

- **Tipo da Chave:** Neste caso, as chaves são **Strings**.
- **Como Acessar:** Você precisa usar a própria string para acessar o valor

```ruby
puts usuario["nome"] # => "Ana"
```

**2) Notação com Símbolos (estilo JSON)**

```ruby
usuario_moderno = { nome: "Ana", idade: 25 }
```

- **Tipo da Chave:** Esta é uma sintaxe mais moderna e é um atalho para criar chaves que são **Símbolos**.
- O código acima é 100% equivalente a isto:

```ruby
usuario_moderno = { :nome => "Ana", :idade => 25 }
```

- **Como Acessar:** É preciso saber o símbolo para acessar o valor.

```ruby
puts usuario_moderno[:nome] # => "Ana"
```

- **Strings (`"nome"`):** São usadas para representar dados de texto. Elas são "mutáveis", o que significa que podem ser alteradas.

- **Símbolos (`:nome`):** São usados como identificadores ou rótulos. Eles são "imutáveis" e únicos. O Ruby garante que existe apenas uma cópia de um símbolo específico em memória, o que os torna muito mais eficientes (rápidos e com menor uso de memória) para serem usados como chaves de Hashes.

#### 5) Loops

Esqueça o `for (int i = ...)` de C. Em Ruby, é pedido para as coleções (como Arrays) se percorrerem sozinhas usando **iteradores** e **blocos**.

- **Bloco:** É um pedaço de código anônimo que você passa para um método. Ele é definido entre `do...end` ou `{...}`.

O iterador mais importante é o `.each`:

```ruby
nomes = ["Ana", "Bruno", "Carla"] # Pedindo para o array 'nomes' percorrer cada um de seus itens 

nomes.each do |nome_individual| 
	puts "Olá, #{nome_individual}!" 
end
```

**Como ler isso:** "Array `nomes`, para CADA um de seus elementos (que são chamados de `nome_individual` por vez), execute este bloco de código.".

#### 6) Orientação a Objetos

**1) Classes e Objetos**

- Uma **Classe** é a planta de um objeto (ex: a planta de uma casa).
- Um **Objeto** é a construção real a partir da planta (ex: a casa em si).

```ruby
# Definindo a planta para um "Cachorro" 
class Cachorro 
	# O método initialize é o "construtor", chamado quando usamos .new 
	def initialize(nome, raca) # Variáveis com '@' pertencem ao objeto (são "variáveis de instância") 
		@nome = nome 
		@raca = raca 
	end
	
# Métodos são as "ações" que o objeto pode fazer 
	def latir 
		puts "#{@nome} diz: Au au!" 
	end 
end 

# Criando objetos (instâncias) a partir da classe 
rex = Cachorro.new("Rex", "Pastor Alemão")
bela = Cachorro.new("Bela", "Poodle")

# Enviando mensagens para nossos novos objetos 
rex.latir # => Rex diz: Au au! 
bela.latir # => Bela diz: Au au!
```

**2) Getters e Setters (`attr_accessor`)**

Para ler e escrever as variáveis `@nome` e `@raca` de fora do objeto, usamos `attr_accessor`. É um atalho que cria os métodos de leitura e escrita para você.

```ruby
class Cachorro
  attr_accessor :nome, :raca # Mágica! Cria os métodos nome, nome=, raca, raca=

  def initialize(nome, raca)
    @nome = nome
    @raca = raca
  end

  def latir
    puts "#{@nome} diz: Au au!"
  end
end

rex = Cachorro.new("Rex", "Pastor Alemão")
puts rex.nome  # Lendo o nome (getter)
rex.nome = "Rexy" # Alterando o nome (setter)
rex.latir     # => Rexy diz: Au au!
```

#### 7) Herança

Herança permite que uma classe (filha) herde os comportamentos de outra (mãe).

```ruby
class Animal
  def respirar
    puts "Inspirando e expirando..."
  end
end

# A classe Cachorro herda de Animal usando o sinal '<'
class Cachorro < Animal
  # ... todo o código da classe Cachorro ...
end

rex = Cachorro.new("Rex", "Pastor Alemão")
rex.latir     # Método da própria classe Cachorro
rex.respirar  # Método herdado da classe Animal!
```


Anotar sobre self, attr_accessor, initialize, etc
Anotar sobre funções como group_by, include?, .inspect etc

## Syntax

The Ruby group_by() method is available to any object that includes the Enumerable module, which includes collections such as arrays and hashes.

**The syntax for using Ruby group_by() is as follows:**

```ruby
enumerable.group_by { |element| criterion }
```

Here, enumerable represents the collection on which you want to apply the grouping, and criterion is a block of code that defines the criterion for grouping the elements. The block takes each element of the collection as an argument and returns the value based on which the elements will be grouped.

## Parameters

The Ruby group_by() method takes a single parameter, which is a block of code that defines the criterion for grouping the elements. The block is executed for each element in the collection, and its return value is used as the key in the resulting hash.

**The block has the following syntax:**

```ruby
{ |element| criterion }
```

Here, element represents an individual element from the collection, and criterion is the code that determines how the elements should be grouped. The criterion can be any expression or calculation that produces a value based on which the elements will be grouped.