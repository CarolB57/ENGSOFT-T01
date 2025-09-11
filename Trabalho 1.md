
# **Como LLM pode promover o aprendizado e o desenvolvimento de aplicações Ruby?**


**Aluna:** Caroline Bohadana Rodrigues Viana

**Matrícula:** 232050975

**Disciplina:** Engenharia de Software 2025/2


## **Exercício 1**

**a)** A resolução inicialmente proposta para esse exercício é:

```ruby
def palindrome?(string)

    # 1. Pré-processamento da string de entrada:
    #    - gsub(/[^a-zA-Z]/, ''): Remove todos os caracteres que não são letras.
    #      A expressão regular /[^a-zA-Z]/ significa: "qualquer caractere que não seja (^) uma letra de a-z, A-Z.".
    #    - .downcase: Converte toda a string para letras minúsculas para garantir que a comparação não diferencie maiúsculas de minúsculas.
    letras = string.gsub(/[^a-zA-Z]/, '').downcase

    # Inicializa uma variável booleana como 'true'. Assume-se que a palavra é um palíndromo até que se prove o contrário.
    palindromo = true
    tamanho = letras.length

    # 3. Loop para verificar se a palavra é um palíndromo.
    #    O loop vai de 0 até a metade do tamanho da palavra. Usar 'tamanho / 2' é eficiente, pois precisa-se comparar a primeira metade com a segunda.
    (0...tamanho / 2).each do |i|
        # Pega a letra da esquerda (começando do índice 0).
        letra_esquerda = letras[i]
        # Pega a letra correspondente da direita. O índice negativo '-(i + 1)' começa a contar do final do array.
        letra_direita = letras[-(i + 1)]
        # Compara as duas letras.
        if letra_esquerda != letra_direita
            # Se em qualquer ponto as letras não forem iguais, frase/palavra não é um palíndromo.
            palindromo = false
            break
        end
    end

    if palindromo == false
        puts "false"
        return
    end
    puts "true"
end

# A primeira palavra "a" já é um palíndromo. O código imprimirá "true" e vai parar.
palindrome?("A man, a plan, a canal -- Panama")

# A primeira palavra "madam" é um palíndromo. O código imprimirá "true" e vai parar.
palindrome?("Madam, I'm Adam!")

# A primeira palavra "abracadabra" não é um palíndromo. O código imprimirá "false".
palindrome?("Abracadabra")
```

Como implementação alternativa, pode-se usar:

```ruby
def palindrome_phrase?(string)
    # 1. Preparação da String:
    #    - Converte para minúsculas.
    #    - Usa gsub para remover tudo o que não for letra ou número.
    #      A expressão regular /[^a-z0-9]/ significa "qualquer caractere que não seja (^) uma letra de a-z ou um número de 0-9".
    processed_string = string.downcase.gsub(/[^a-z0-9]/, '')

    # 2. A Verificação:
    #    - Compara a string processada com ela mesma invertida (.reverse).
    #    - Esta linha retorna 'true' se forem iguais e 'false' caso contrário.
    processed_string == processed_string.reverse

end

# Retorna: true
puts palindrome_phrase?("A man, a plan, a canal -- Panama")

# Retorna: true
puts palindrome_phrase?("Madam, I'm Adam!")

# Retorna: false
puts palindrome_phrase?("Abracadabra")

# Retorna: true
puts palindrome_phrase?("Socorram-me, subi no onibus em Marrocos")
```

Tal implementação favorece a legibilidade, uma vez que o código é muito claro e idiomático em Ruby. Sua performance é excelente, pois o código é muito rápido para a maioria dos casos. Além disso, é uma solução simples e direta. Porém, necessita alocar uma nova string invertida, o que pode desfavorecer a performance com entradas muito grandes.

Dessa forma, o código acima favorece melhor entendimento do papel que o código exerce e é a melhor opção a ser utilizada.

**b)** A resolução inicialmente proposta para esse exercício é:

```ruby
def count_words(string)
  # 1. Pré-processamento da string de entrada:
  #    - gsub(/[^a-zA-Z\s]/, ''): Remove todos os caracteres que NÃO são letras ou espaços.
  #    - .downcase: Converte a string para letras minúsculas para que palavras como "A" e "a" sejam contadas como a mesma.
  #    - .split: Divide a string em um array de palavras, usando espaços como delimitadores.
  palavras = string.gsub(/[^a-zA-Z\s]/, '').downcase.split

  # 2. Criação do contador:
  #    - Hash.new(0): Cria um novo Hash (um dicionário de chave-valor).
  #    - O argumento '0' define um valor padrão. Isso significa que, se você tentar acessar uma chave
  #      que ainda não existe no hash, ele retornará 0 em vez de 'nil' (nulo).
  #    - Isso é extremamente útil para contadores, pois simplifica a lógica de incremento.
  contagem_de_palavras = Hash.new(0)

  # 3. Contagem das palavras:
  #    - .each_with_index itera sobre cada item do array 'palavras', fornecendo a palavra e seu índice.
  palavras.each do |palavra|
    # Para cada 'palavra', ela é usada como chave no hash 'contagem_de_palavras'.
    # - Se a chave 'palavra' ainda não existe, o valor padrão (0) é usado, e a operação se torna: contagem_de_palavras[palavra] = 0 + 1.
    # - Se a chave já existe, seu valor atual é pego e incrementado em 1.
    contagem_de_palavras[palavra] += 1
  end

  # 4. Exibição dos resultados:
  #    - Itera sobre o hash 'contagem_de_palavras', obtendo cada par de [chave, valor]
  #      e atribuindo-os às variáveis 'palavra' e 'contagem'.
  contagem_de_palavras.each do |palavra, contagem|
    # Imprime a palavra e sua respectiva contagem no console de forma formatada.
    puts "'#{palavra}' => #{contagem}"
  end
end

count_words("A man, a plan, a canal -- Panama")
puts
count_words("Doo bee doo bee doo")
```

Como implementação alternativa, propõe-se:

```ruby
def count_words(string)
    # A etapa de limpeza da string continua a mesma.
    palavras = string.downcase.gsub(/[^a-z0-9\s]/, '').split
    
    # O método .tally faz a contagem de todos os elementos do array
    # e retorna um hash com o resultado. É tudo feito em uma única chamada.
    contagem_de_palavras = palavras.tally
    
    contagem_de_palavras.each do |palavra, contagem|
        puts "'#{palavra}' => #{contagem}"
	end
end

count_words("A man, a plan, a canal -- Panama")
puts
count_words("Doo bee doo bee doo")
```

O código acima é mais conciso, uma vez que substitui um bloco de iteração inteiro por uma única chamada de método (`.tally`); é mais legível, pois o nome do método, `tally` (contagem), expressa claramente a intenção do código, além de ser performático, pois por ser um método nativo implementado em C, geralmente é mais rápido do que um loop implementado em Ruby puro. 

Dessa forma, o código acima favorece iniciantes em Ruby e é a melhor opção a ser utilizada.

## **Exercício 2**

**a)** A resolução inicialmente proposta para esse exercício é:

```ruby
# Define uma classe de erro personalizada para quando o número de jogadores for incorreto.
class WrongNumberOfPlayersError < StandardError ; end
# Define uma segunda classe de erro para quando uma estratégia (jogada) for inválida.

class NoSuchStrategyError < StandardError ; end
# REGRAS é uma constante (indicada pelo nome em maiúsculas) que armazena a lógica do jogo.

# É um Hash onde a chave representa o vencedor e o valor representa o perdedor.
# 'R' (Pedra) ganha de 'S' (Tesoura)
# 'S' (Tesoura) ganha de 'P' (Papel)
# 'P' (Papel) ganha de 'R' (Pedra)

REGRAS = { 'R' => 'S', 'S' => 'P', 'P' => 'R' }

# Lista dos símbolos válidos NO JOGO
JOGADAS_VALIDAS = ['R', 'P', 'S']

def rps_game_winner(game)
    # 1. Validação de entrada (Guard Clause)
    #    Verifica se o array 'game' tem exatamente 2 elementos (jogadores).
    #    Se não tiver, ele lança (raise) a exceção WrongNumberOfPlayersError, interrompendo a execução.
    raise WrongNumberOfPlayersError unless game.length == 2

    # 2. Itera sobre as combinações de jogadores.
    #    O método .combination(2) em um array de 2 elementos gera apenas uma combinação: o par de jogadores.
    #    Portanto, este loop 'each' executará apenas uma vez.
    game.combination(2).each do |jogador1, jogador2|
        # 3. Desestruturação dos dados dos jogadores.
        #    Pega o array de cada jogador e atribui seus elementos a variáveis separadas.
        nome1, simbolo1 = jogador1 # nome1="Kristen", simbolo1="P"
        raise NoSuchStrategyError unless JOGADAS_VALIDAS.include?(simbolo1) # Verifica se o símbolo é válido
        nome2, simbolo2 = jogador2 # nome2="Pam",    simbolo2="S"
        raise NoSuchStrategyError unless JOGADAS_VALIDAS.include?(simbolo2) # Verifica se o símbolo é válido

        # Inicializa as variáveis de resultado como nulas.
        vencedor = nil
        perdedor = nil

        # 4. Lógica para determinar o vencedor
        #    Verifica se o símbolo do jogador 1 ganha do símbolo do jogador 2.
        if REGRAS[simbolo1] == simbolo2
            vencedor = jogador1
            perdedor = jogador2
        # Senão, verifica se o símbolo do jogador 2 ganha do símbolo do jogador 1.
        elsif REGRAS[simbolo2] == simbolo1
            vencedor = jogador2
            perdedor = jogador1
        end
        # Se nenhuma das condições acima for atendida, significa que houve um empate 
        # Nesse caso, a variável 'vencedor' continuará como 'nil'.
        if vencedor
            # ...imprime o array do jogador vencedor no formato "[Nome, Símbolo]".
            puts "[#{vencedor[0]}, #{vencedor[1]}]"
        else
            # Senão (em caso de empate), imprime a lista original com os dois jogadores.
            puts "[[#{nome1}, #{simbolo1}], [#{nome2}, #{simbolo2}]]"
        end
    end
end

rps_game_winner([ [ "Kristen", "P" ], [ "Pam", "S" ] ])
# => returns the list ["Pam", "S"] wins since S>P
```

Uma abordagem alternativa é:

```ruby
class WrongNumberOfPlayersError < StandardError; end
class NoSuchStrategyError < StandardError; end

REGRAS = { 'R' => 'S', 'S' => 'P', 'P' => 'R' }
JOGADAS_VALIDAS = REGRAS.keys # Obtém as jogadas válidas diretamente do hash: ['R', 'S', 'P']

def rps_game_winner(game)
    # 1. Validação de Número de Jogadores
    raise WrongNumberOfPlayersError, "O jogo deve ter exatamente 2 jogadores" unless game.length == 2

    # 2. Atribuição Direta dos Jogadores
    #    Removemos o .combination(2).each, que era desnecessário.
    jogador1, jogador2 = game

    # Desestrutura os dados de cada jogador
    nome1, jogada1 = jogador1
    nome2, jogada2 = jogador2

    # 3. Validação das Jogadas (Mais robusto)
    #    Verifica se ambas as jogadas são válidas antes de continuar.
    raise NoSuchStrategyError, "Jogada '#{jogada1}' é inválida" unless JOGADAS_VALIDAS.include?(jogada1)
    raise NoSuchStrategyError, "Jogada '#{jogada2}' é inválida" unless JOGADAS_VALIDAS.include?(jogada2)

    # 4. Lógica de Decisão Simplificada
    #    Se as jogadas são iguais, o jogador 1 vence por padrão.
    return jogador1 if jogada1 == jogada2

    # Se a jogada do jogador1 ganha da jogada do jogador2, então o jogador1 é o vencedor.
    if REGRAS[jogada1] == jogada2
        return jogador1
    else
        # Se não foi empate e o jogador1 não ganhou, então o jogador2 deve ser o vencedor.
        return jogador2
    end
end

begin
    vencedor = rps_game_winner([["Kristen", "P"], ["Pam", "S"]])
    puts "#{vencedor.inspect}" # Saída: ["Pam", "S"]
    empate = rps_game_winner([["David", "R"], ["Richard", "R"]])
    puts "Em caso de empate, o vencedor é: #{empate.inspect}" # Saída: Em caso de empate, o vencedor é: ["David", "R"]
    
    # Teste de erro de jogada inválida
    rps_game_winner([["Michael", "X"], ["Dave", "P"]])

rescue WrongNumberOfPlayersError => e
  puts "Erro: #{e.message}"
rescue NoSuchStrategyError => e
  puts "Erro: #{e.message}" # Saída: Erro: Jogada 'X' é inválida
end
```

A abordagem acima possui diversas melhorias em termos de legibilidade e eficiência, como:

- A estrutura `if jogada1 == jogada2`, `if REGRAS[jogada1] == jogada2`, `else` é  mais direta e cobre as três possibilidades (empate, vitória do jogador 1, vitória do jogador 2) de forma explícita e sem a necessidade de variáveis intermediárias como `vencedor` e `perdedor`.

- A adição da verificação de jogadas inválidas (`NoSuchStrategyError`) torna a função mais segura e previne comportamentos inesperados se a entrada contiver dados incorretos.

- A remoção da chamada ao método `.combination(2).each`, e a atribuição direta `jogador1, jogador2 = game` é uma mudança que deixa o código mais rápido e mais simples de ler.

- A definição de `JOGADAS_VALIDAS = REGRAS.keys` evita que duas listas de jogadas separadas tenham que ser mantidas. Se houver uma adição de uma nova regra ao hash, a lista de jogadas válidas é atualizada automaticamente.

Dessa maneira, o código acima é uma implementação boa e prática.

**b)** O código inicialmente proposto para esse exercício é:

```ruby
class NoSuchStrategyError < StandardError ; end

# REGRAS é um Hash que define a lógica de vitória: a CHAVE ganha do VALOR.
REGRAS = { 'R' => 'S', 'S' => 'P', 'P' => 'R' }

# JOGADAS_VALIDAS é um Array criado a partir das chaves do hash REGRAS.
# Isso garante que a lista de jogadas válidas esteja sempre sincronizada com as regras.
# O resultado será: ['R', 'S', 'P']
JOGADAS_VALIDAS = REGRAS.keys

# FUNÇÃO 1: Decide o vencedor de UMA ÚNICA PARTIDA
# Recebe dois jogadores como argumento, onde cada jogador é um array [nome, jogada].
def rps_game_winner(jogador1, jogador2)
    # Extrai apenas a jogada (o segundo elemento, índice 1) de cada jogador.
    simbolo1 = jogador1[1]
    simbolo2 = jogador2[1]

    # Valida se a jogada de cada jogador está na lista de JOGADAS_VALIDAS.
    # Se uma jogada for inválida, emite a exceção NoSuchStrategyError, interrompendo a execução.
    raise NoSuchStrategyError, "Jogada '#{simbolo1}' é inválida" unless JOGADAS_VALIDAS.include?(simbolo1)
    raise NoSuchStrategyError, "Jogada '#{simbolo2}' é inválida" unless JOGADAS_VALIDAS.include?(simbolo2)

    # Lógica para determinar o vencedor:
    # 1. Verifica se a jogada do jogador1 ganha da jogada do jogador2, consultando o hash REGRAS.
    if REGRAS[simbolo1] == simbolo2
        return jogador1 # Se sim, retorna o array completo do jogador1.
    # 2. Senão, verifica se a jogada do jogador2 ganha da jogada do jogador1.
    elsif REGRAS[simbolo2] == simbolo1
        return jogador2 # Se sim, retorna o array completo do jogador2.
    # 3. Se nenhuma das condições acima for verdadeira, significa que as jogadas são iguais (empate).
    else
        return nil # Retorna 'nil' para indicar um empate.
    end
end

# FUNÇÃO 2: Simula um TORNEIO INTEIRO
# Recebe um 'game', que é uma estrutura de arrays aninhados representando as chaves do torneio.
def rps_tournament_winner(game)
    # Prepara a primeira rodada:
    # .flatten(2) "achata" os arrays internos em 2 níveis, criando uma lista única
    # com todos os jogadores em ordem para a primeira rodada.
    rodada_atual = game.flatten(2)
    # Loop principal do torneio: continua enquanto houver mais de um jogador na rodada.
    while rodada_atual.length > 1
        # Array para armazenar os vencedores da rodada que está prestes a acontecer.
        vencedores_da_rodada = []
        # .each_slice(2) agrupa os jogadores da rodada em pares (partidas de 2).
        rodada_atual.each_slice(2) do |partida|
            # Desestrutura a partida nos dois jogadores.
            jogador1, jogador2 = partida
            # Tratamento para número ímpar de jogadores na rodada:
            # Se 'jogador2' for 'nil', significa que 'jogador1' não teve um par.
            if jogador2.nil?
                vencedor = jogador1 # Avança automaticamente
            else
                # Se houver um par, chama a função rps_game_winner para decidir o vencedor da partida.
                vencedor = rps_game_winner(jogador1, jogador2)
            end
        # Adiciona o vencedor da partida na lista de vencedores da rodada.
            vencedores_da_rodada << vencedor
        end
        # Ao final da rodada, a lista de jogadores da "próxima rodada" se torna a lista de vencedores da rodada atual.
        rodada_atual = vencedores_da_rodada
    end

    # Quando o loop 'while' termina, 'rodada_atual' contém apenas um elemento: o grande campeão.
    vencedor = rodada_atual[0]
    return vencedor # Retorna o array do vencedor final.

end

vencedor_do_torneio = rps_tournament_winner(
[ # Chave principal
  [ # Semi-final 1
    [ ["Kristen", "P"], ["Dave", "S"] ],    # Partida 1 -> Vencedor: Dave
    [ ["Richard", "R"], ["Michael", "S"] ],  # Partida 2 -> Vencedor: Richard (R > S)
  ],
  [ # Semi-final 2
    [ ["Allen", "S"], ["Omer", "P"] ],      # Partida 3 -> Vencedor: Allen
    [ ["David E.", "R"], ["Richard X.", "P"] ] # Partida 4 -> Vencedor: Richard X.
  ]
]) # Final: Richard vs Richard X. -> Richard X vence (P > R) | Dave vs Allen -> Allen vence (S > P) -> Final: Richard X vs Allen

# Desestrutura o resultado final para exibição.
nome, simbolo = vencedor_do_torneio
# Imprime o vencedor do torneio.
puts "[#{nome}, #{simbolo}]"
```

Como solução alternativa, tem-se o seguinte código:

```ruby
class NoSuchStrategyError < StandardError ; end

REGRAS = { 'R' => 'S', 'S' => 'P', 'P' => 'R' }
JOGADAS_VALIDAS = REGRAS.keys

# A função de jogo único foi aprimorada para lidar com empates de forma explícita.
# Em caso de empate, o jogador 1 é considerado o vencedor por convenção.
def rps_game_winner(jogador1, jogador2)
    simbolo1 = jogador1[1]
    simbolo2 = jogador2[1]

    raise NoSuchStrategyError, "Jogada '#{simbolo1}' é inválida" unless JOGADAS_VALIDAS.include?(simbolo1)
    raise NoSuchStrategyError, "Jogada '#{simbolo2}' é inválida" unless JOGADAS_VALIDAS.include?(simbolo2)

    # Se a jogada do jogador 2 estiver no valor correspondente à chave do jogador 1, jogador 1 ganha.

    return jogador1 if REGRAS[simbolo1] == simbolo2
    # Caso contrário, por eliminação (e tratando o empate), o jogador 2 ganha.
    # Se for empate (ex: 'R' vs 'R'), a condição acima é falsa, então o jogador 2 é retornado.
    # Ajuste: A convenção clássica é que o jogador 1 vence no empate. Vamos ajustar.

    return jogador2 if REGRAS[simbolo2] == simbolo1

    # Se nenhuma das condições de vitória for atendida, é um empate. Retorna o primeiro jogador.
    return jogador1
end

def rps_tournament_winner(bracket) # Versão recursiva
    # 1. CASO BASE: Verificamos se 'bracket' é um jogador.
    #    Um jogador é um array onde o segundo elemento é uma String (a jogada 'R', 'P', ou 'S').
    #    Uma chave de torneio é um array onde os elementos são outros arrays.
    if bracket[0].is_a?(String) # Uma forma simples de checar se é um jogador
        return bracket
    end

    # 2. PASSO RECURSIVO: Se não for um jogador, é uma chave de torneio.
    #    A chave (bracket) contém duas sub-chaves: bracket[0] e bracket[1].
    # Encontra o vencedor da primeira metade do bracket chamando a função para essa metade.
    vencedor_chave1 = rps_tournament_winner(bracket[0])
    # Encontra o vencedor da segunda metade do bracket.
    vencedor_chave2 = rps_tournament_winner(bracket[1])
    # Agora que temos os dois vencedores, colocamos eles para jogar um contra o outro.
    return rps_game_winner(vencedor_chave1, vencedor_chave2)
end

torneio =
[[
  [ ["Kristen", "P"], ["Dave", "S"] ],
  [ ["Richard", "R"], ["Michael", "S"] ],
],
[
  [ ["Allen", "S"], ["Omer", "P"] ],
  [ ["David E.", "R"], ["Richard X.", "P"] ]
]]

vencedor = rps_tournament_winner(torneio)
puts "#{vencedor.inspect}"
```

Como vantagens dessa implementação, podem-se citar a versatilidade da versão, uma vez que não depende de um nível fixo de aninhamento. Ela funcionará para um torneio de 4, 8, 16, ou 32 jogadores sem precisar de nenhuma alteração. Além disso, o uso da recursão elimina essa complexidade e torna o fluxo de dados mais explícito. Uma grande vantagem de tal código é que é a facilidade de depurar e dar manutenção em um código que segue uma lógica direta. Se houver um problema, pode-se rastrear a árvore de chamadas da recursão de forma lógica.

Portanto, a implementação acima é mais simples, intuitiva e prática, facilitando o uso e futuras manutenções.

## **Exercício 3**

 A resolução inicialmente proposta para essa questão é:

```ruby
def combine_anagrams(words)

    # Cria um Hash (dicionário) vazio. Ele será usado para agrupar as palavras
    # que são anagramas umas das outras.
    anagram_groups = {}
    
    # Itera sobre cada palavra no array de entrada.
    words.each do |word|
        # 1. Cria uma "chave canônica" para a palavra.
        #    A chave será a mesma para todos os seus anagramas.
        sorted_word = word.downcase.chars.sort.join

        # 2. Garante que existe um array para esta chave no hash.
        #    O operador ||= (conhecido como "or-equals") é um atalho que diz:
        #    "Se anagram_groups[sorted_word] ainda não existir (for nil),
        #    então crie-o e atribua um array vazio [] a ele."
        #    Se a chave já existir, esta linha não faz nada.
        anagram_groups[sorted_word] ||= []

        # 3. Adiciona a palavra *original* ao array correspondente à sua chave.
        anagram_groups[sorted_word] << word
    end

    # 4. Retorna o resultado.
    #    Ao final, estamos interessados apenas nos grupos de palavras (os valores do hash),
    #    e não nas chaves ordenadas. O método .values retorna um array com todos os valores do hash.
    anagram_groups.values

end

words1 = ['cars', 'for', 'potatoes', 'racs', 'four','scar', 'creams', 'scream']
words2 = ["creams", "scream"]

# .inspect é usado para imprimir o array de uma forma legível.
puts combine_anagrams(words1).inspect
puts combine_anagrams(words2).inspect
```

Como uma solução distinta, tem-se o seguinte código:

```ruby
def combine_anagrams(words)
    # 1. words.group_by {...}: Itera sobre cada palavra.
    # 2. O bloco calcula a chave (a palavra ordenada), exatamente como antes.
    # 3. O group_by usa essa chave para agrupar todas as palavras que resultam na mesma chave.
    # 4. .values: Pega apenas os arrays de palavras agrupadas no final.
    words.group_by { |word| word.downcase.chars.sort.join }.values
end

words1 = ['cars', 'for', 'potatoes', 'racs', 'four','scar', 'creams', 'scream']
words2 = ["creams", "scream"]

puts combine_anagrams(words1).inspect
puts combine_anagrams(words2).inspect
```

A implementação acima é mais concisa do que a primeira. Isso se deve ao uso do método group_by, o qual agrupa palavras com a mesma ordenação de letras. Em termos de velocidade de execução, a diferença entre as duas versões é mínima ou inexistente. Ambas executam essencialmente as mesmas operações (calcular a chave para cada palavra e inseri-la em um hash). A complexidade do algoritmo continua a mesma. A eficiência em questão seria principalmente para o desenvolvedor, que pode escrever e entender o código mais rapidamente.

Dessa forma, ambas as abordagens são boas em diversos quesitos, como velocidade, performance. Cabe ao desenvolvedor escolher a que mais lhe agrada.

## **Exercício 4**

**a)** A resolução inicialmente proposta para esse exercício é:

```ruby
class Dessert

    # O método 'initialize' é o construtor da classe. Ele é chamado
    # sempre que um novo objeto é criado (ex: Dessert.new).
    def initialize(name, calories)
        # '@name' e '@calories' são variáveis de instância. Elas pertencem a cada
        # objeto específico e guardam suas informações (estado).
        @name = name
        @calories = calories
    end
    
	# Define um método de instância chamado 'healthy?'.
    def healthy?
    # Retorna 'true' se as calorias forem menores que 200, senão 'false'.
        if @calories < 200
            return true
        else
            return false
        end
    end

    # Define outro método de instância, 'delicious?'.
    def delicious?
        # Por padrão, toda sobremesa da classe 'Dessert' é considerada deliciosa.
        return true
    end
end

bolo = Dessert.new("Mané pelado", 350)

# Chama o método 'delicious?' do objeto 'bolo'. Usa a lógica da classe Dessert.
puts bolo.delicious?
# Chama o método 'healthy?' do objeto 'bolo'. 350 não é < 200.
puts bolo.healthy?
```

Outra versão do mesmo código é:

```ruby
class Dessert

    # 1. Usa attr_reader para criar automaticamente os métodos de leitura
    #    para os atributos @name e @calories. Agora pode-se acessá-los de fora.
    attr_reader :name, :calories
    def initialize(name, calories)

        @name = name
        @calories = calories
    end
    
    # 2. Simplificação do método booleano.
    #    A expressão '@calories < 200' já avalia para 'true' ou 'false'.
    #    Não é necessário um 'if/else' para retornar esses valores.
    #    O Ruby retorna implicitamente o resultado da última linha do método.

    def healthy?
        @calories < 200
    end

    def delicious?
        # Este método já era simples e eficiente.
        true
    end
end

bolo = Dessert.new("Mané pelado", 350)

puts bolo.delicious?
puts bolo.healthy?
```

A implementação acima reduz definições de alguns métodos. A expressão de comparação `@calories < 200` no método `healthy?` já resulta em `true` ou `false`. O Ruby automaticamente retorna o valor da última expressão avaliada em um método. Portanto, o bloco `if/else` completo é desnecessário e verboso. A versão de uma linha é mais curta, mais rápida de ler e faz exatamente a mesma coisa.

Na classe `Dessert` original, as variáveis `@name` e `@calories` eram "privadas" ao objeto; não havia como lê-las de fora. A versão com `attr_reader` é o jeito idiomático do Ruby para criar "métodos getter" (métodos de leitura). Ele gera automaticamente os métodos `def name; @name; end` e `def calories; @calories; end` por baixo dos panos. Isso torna a classe mais útil e o código mais limpo.

Com as mudanças aplicadas, o código se tornou de fácil manutenção, uma vez que ficou menos verboso, facilitando depuração.

Dessa maneira, o segundo código é melhor a ser utilizado, uma vez que é mais conciso e de fácil entendimento e manutenção.

**b)** A resolução inicialmente proposta para esse exercício é:

```ruby
class Dessert

    # O método 'initialize' é o construtor da classe. Ele é chamado
    # sempre que um novo objeto é criado (ex: Dessert.new).
    def initialize(name, calories)
        # '@name' e '@calories' são variáveis de instância. Elas pertencem a cada
        # objeto específico e guardam suas informações (estado).
        @name = name
        @calories = calories
    end
    
	# Define um método de instância chamado 'healthy?'.
    def healthy?
    # Retorna 'true' se as calorias forem menores que 200, senão 'false'.
        if @calories < 200
            return true
        else
            return false
        end
    end

    # Define outro método de instância, 'delicious?'.
    def delicious?
        # Por padrão, toda sobremesa da classe 'Dessert' é considerada deliciosa.
        return true
    end
end

# Define uma classe 'JellyBean' que HERDA da classe 'Dessert'.
# O sinal '<' indica herança. 'JellyBean' é um tipo de 'Dessert' e, portanto,
# recebe todos os seus métodos (initialize, healthy?, delicious?).
class JellyBean < Dessert
    # 'attr_accessor' é um atalho do Ruby que cria automaticamente
    # os métodos para ler e escrever a variável de instância '@flavor'.
    attr_accessor :flavor

    # Construtor específico para a classe JellyBean.
    def initialize(name, calories, flavor)
        # 'super(name, calories)' chama o método 'initialize' da classe pai (Dessert).
        # Isso evita reescrever a lógica de atribuir @name e @calories.
        super(name, calories)
        # Atribui a variável de instância específica da classe JellyBean.
        @flavor = flavor
    end

    # Sobrescrita de Método (Method Overriding)
    # A classe 'JellyBean' fornece sua própria versão do método 'delicious?'.
    def delicious?
        # Adiciona uma regra especial: se o sabor for 'black licorice', não é delicioso.
        return false if @flavor == 'black licorice'
        # Para todos os outros sabores, ele usa a lógica da classe pai.
        # 'super' aqui chama o método 'delicious?' da classe 'Dessert',
        # que por padrão retorna 'true'.
        super
    end
end

bolo = Dessert.new("Mané pelado", 350)
jelly = JellyBean.new("Jelly", 150, "orange licorice")
puts bolo.delicious?   # => true
puts bolo.healthy?
puts jelly.delicious?
puts jelly.healthy?
```

Outra implementação seria:

```ruby
class Dessert

    # 1. Usa attr_reader para criar automaticamente os métodos de leitura
    #    para os atributos @name e @calories. Agora podemos acessá-los de fora.
    attr_reader :name, :calories

    def initialize(name, calories)
        @name = name
        @calories = calories
    end

    # 2. Simplificação do método booleano.
    #    A expressão '@calories < 200' já avalia para 'true' ou 'false'.
    #    Não é necessário um 'if/else' para retornar esses valores.
    #    O Ruby retorna implicitamente o resultado da última linha do método.
    def healthy?
        @calories < 200
    end

    def delicious?
        # Este método já era simples e eficiente.
        true
    end
end

# Define uma classe 'JellyBean' que HERDA da classe 'Dessert'.
# O sinal '<' indica herança. 'JellyBean' é um tipo de 'Dessert' e, portanto,
# recebe todos os seus métodos (initialize, healthy?, delicious?).
class JellyBean < Dessert

    # attr_accessor para o atributo 'flavor' já estava perfeito.
    attr_accessor :flavor

    def initialize(name, calories, flavor)
        super(name, calories)
        @flavor = flavor
    end

    # 3. Esta implementação já era idiomática e eficiente.
    #    O uso de uma "guard clause" (o 'if' em uma linha) e o 'super'
    #    são considerados ótimas práticas em Ruby.
    def delicious?
        return false if @flavor == 'black licorice'
        super
    end
end

bolo = Dessert.new("Mané pelado", 350)
jelly = JellyBean.new("Jelly", 150, "orange licorice")
puts bolo.delicious?   # => true
puts bolo.healthy?
puts jelly.delicious?
puts jelly.healthy?
```

Essa implementação possui as mesmas vantagens referentes à segunda versão do código feito na **letra a**.

## **Exercício 5**

Inicialmente, o exercício foi resolvido por meio do seguinte código:

```ruby
class Class

    # Define um novo método de classe chamado 'attr_accessor_with_history'.
    # Ele funcionará de forma parecida com o 'attr_accessor' nativo, mas com uma modificação
    def attr_accessor_with_history(attr_name)
    
        # Garante que o nome do atributo seja uma string para facilitar a manipulação.
        attr_name = attr_name.to_s

        # 1. Cria dinamicamente o método de LEITURA (getter) para o atributo.
        attr_reader attr_name

        # 2. Cria dinamicamente o método de LEITURA para o HISTÓRICO do atributo.
        attr_reader attr_name + "_history"

        # 3. A MÁGICA PRINCIPAL: Gera o método de ESCRITA (setter) dinamicamente.
        #    'class_eval' executa o código dentro da string como se ele estivesse
        #    escrito diretamente dentro da classe que chamou o método (a classe 'Foo').
        #    %Q{...} é uma forma de criar uma string que permite interpolação (#{...}).
        class_eval %Q{
        # Abaixo está o CÓDIGO QUE SERÁ GERADO E INSERIDO NA CLASSE 'Foo'.
        # Para attr_name = "bar", a linha abaixo se torna "def bar=(value)".
        def #{attr_name}=(value)
            # Inicializa a variável de instância do histórico SE ela ainda não existir.
            # O '||=' garante que isso só aconteça na primeira vez que o método for chamado
            # para um objeto. Começa com [nil] para registrar o estado inicial "sem valor".
            @#{attr_name}_history ||= [nil]
            # Adiciona o novo 'value' ao final do array de histórico.
            @#{attr_name}_history << value
            # Finalmente, executa a ação normal de um setter: atribui o valor
            # à variável de instância principal.
            @#{attr_name} = value
        end
        }
    end
end

# Cria uma classe chamada Foo.
class Foo
    # Foo chama o método 'attr_accessor_with_history' que definimos em 'Class'.
    # Isso executa todo o código acima e cria dinamicamente os métodos
    # 'bar', 'bar_history' e 'bar=' dentro da classe Foo.
    attr_accessor_with_history :bar
end

# Cria um novo objeto (uma instância) da classe Foo.
f = Foo.new

# Chama o método setter 'bar=' que foi criado dinamicamente.
# - @bar_history é inicializado como [nil].
# - 1 é adicionado -> @bar_history se torna [nil, 1].
# - @bar é definido como 1.
f.bar = 1

# Chama o setter 'bar=' novamente.
# - @bar_history já existe, então o '||=' não faz nada.
# - 2 é adicionado -> @bar_history se torna [nil, 1, 2].
# - @bar é definido como 2.
f.bar = 2

# Chama o método getter 'bar_history' que foi criado dinamicamente.
# Ele retorna o array [nil, 1, 2].
f.bar_history

# Imprime o histórico para visualização.
puts "Histórico de f.bar: #{f.bar_history.inspect}"
```

A versão aprimorada desse código é:

```ruby
class Class

    def attr_accessor_with_history(attr_name)
        attr_name = attr_name.to_s
        
        # 1. Os getters são criados da mesma forma
        attr_reader attr_name
        attr_reader "#{attr_name}_history"

        # 2. Usa-se 'define_method' com um bloco.
        #    Isso define o método setter dinamicamente sem precisar analisar uma string de código.
        #    O nome do método a ser criado é o primeiro argumento.
        #    O bloco a seguir se torna o corpo do novo método.
        define_method("#{attr_name}=") do |value|
            # O nome da variável de instância para o histórico.
            history_iv_name = "@#{attr_name}_history"

            # Verifica se a variável de histórico já foi definida para este objeto.
            unless instance_variable_defined?(history_iv_name)
                # Se não, a inicializa com o valor [nil] inicial.
                instance_variable_set(history_iv_name, [nil])
            end

            # Adiciona o novo valor ao array de histórico.
            # 'instance_variable_get' lê o valor da variável de instância.
            instance_variable_get(history_iv_name) << value

            # Define o valor da variável de instância principal.
            # 'instance_variable_set' define o valor de uma variável de instância.
            instance_variable_set("@#{attr_name}", value)
        end
    end
end

class Foo
    attr_accessor_with_history :bar
end

f = Foo.new
f.bar = 1
f.bar = 2
f.bar = "hello"

puts "Atributo bar: #{f.bar.inspect}"
puts "Histórico de f.bar: #{f.bar_history.inspect}"
# Saída: Histórico de f.bar: [nil, 1, 2, "hello"]
```

O código em questão tornou-se mais claro e levemente eficiente, pois o `define_method` é geralmente mais rápido que `class_eval` com uma string. Isso ocorre porque o Ruby não precisa "interromper e analisar" a string para transformá-la em código executável toda vez que o método é definido. O bloco já é uma estrutura de código nativa.

Além disso, o código acima é mais seguro, uma vez que escrever código dentro de strings é propenso a erros de digitação, problemas com aspas e falhas de syntax highlighting no editor. O código dentro de um bloco é apenas código Ruby normal, mais limpo e seguro. Se houver um erro dentro do bloco `define_method`, o backtrace (pilha de erros) geralmente aponta para o local correto no seu arquivo, facilitando a depuração. Erros dentro de uma string de `class_eval` podem ser mais difíceis de rastrear.

Uma outra melhoria é que o bloco passado para `define_method` é um _closure_. Isso significa que ele "lembra" das variáveis que existiam ao seu redor quando foi definido, como a variável `attr_name`. Essa é uma importante característica do Ruby, que torna a passagem de informações para o método recém-criado mais elegante.

Dessa maneira, conclui-se que o código modificado é melhor do que a primeira opção apresentada.

## **Exercício 6**

**a)** Inicialmente, o exercício foi resolvido por meio do seguinte código:

```ruby
class Numeric

    # @@currencies é uma variável de classe. Ela é compartilhada por todos os
    # objetos da classe Numeric e armazena as taxas de conversão.
    # A base da conversão é o dólar (valor 1.0).
    @@currencies = {'dollar' => 1.0, 'yen' => 0.013, 'euro' => 1.292, 'rupee' => 0.019}

    # 'method_missing' chama AUTOMATICAMENTE quando tenta-se invocar um método que não existe em um objeto.
    def method_missing(method_id)
    
        # 'method_id' é o nome do método que foi chamado, como um símbolo (:dollars).
        # .to_s.gsub(/s$/, '') converte para string e remove o 's' do final se houver.
        # Isso permite que tanto 'dollar' quanto 'dollars' funcionem.
        singular_currency = method_id.to_s.gsub( /s$/, '')

        # Verifica se a moeda (já no singular) existe como chave no hash.
        if @@currencies.has_key?(singular_currency)
	        # Se existir, multiplica o número ('self') pela taxa de conversão.
	        # 'self' aqui é o próprio número em que o método foi chamado.
	        # O resultado é o valor convertido para a moeda base (dólares).
	        self * @@currencies[singular_currency]
        else
            # Se o método chamado não for uma moeda, é importante chamar 'super', pois
            # passa a chamada para o 'method_missing' da classe pai,
            # permitindo que o Ruby lance o erro padrão "NoMethodError".
            super
        end

    end
    
    # Este método é projetado para ser chamado no resultado da primeira conversão (o valor já em dólares).
    def in(target_currency)
        # Remove o 's' do final da moeda de destino.
        singular_currency = target_currency.to_s.gsub(/s$/, '')
        # Pega o valor atual ('self', que já está em dólares) e divide pela
        # taxa de conversão da moeda de destino para obter o valor final.
        self / @@currencies[singular_currency]
    end
end

valor_em_euros = 5.dollars.in(:euros)
puts "5 dólares equivalem a #{valor_em_euros.round(2)} euros."
```

Uma outra resolução seria:

```ruby
class Numeric

    # 1. Usa-se uma constante em vez de uma variável de classe (@@).
    #    Para dados fixos como taxas de conversão, constantes são mais seguras e uma prática melhor.
    CONVERSION_RATES = {'dollar' => 1.0, 'yen' => 0.013, 'euro' => 1.292, 'rupee' => 0.019}

    # O método 'in' permanece quase o mesmo, apenas usa a nova constante.
    def in(target_currency)
        singular_currency = target_currency.to_s.gsub(/s$/, '')
        self / CONVERSION_RATES[singular_currency]
    end

    # 2. Definem-se os métodos na hora em que a classe é carregada.
    #    Itera-se sobre cada moeda definida na nossa constante.
    CONVERSION_RATES.each_key do |currency|
        # Para cada moeda, usa-se 'define_method' para criar dinamicamente
        # tanto a versão singular quanto a plural do método.

        # Define o método no singular.
        define_method(currency) do
            # O corpo do método é a mesma lógica de antes:
            # converte o número para a moeda base (dólares).
            self * CONVERSION_RATES[currency]
        end

        # Define o método plural.
        define_method("#{currency}s") do
            self * CONVERSION_RATES[currency]
        end
    end
end

valor_em_reais = 100.euros.in(:rupees)
puts "100 euros equivalem a #{valor_em_reais.round(2)} rúpias."
valor_em_euros = 5.dollars.in(:euros)
puts "5 dólares equivalem a #{valor_em_euros.round(2)} euros."
```

As melhorias no código acima em relação ao primeiro código são notáveis. Uma delas é a melhoria de velocidade, pois em vez de realizar uma busca lenta e uma chamada de emergência para `method_missing` toda vez, agora há uma chamada de método direta e otimizada. Os métodos (`.dollars`, `.euros`, etc.) existem de verdade na classe `Numeric` após o código inicial ser executado.
    
Além disso, em se tratatando de clareza e manutenibilidade, pode-se afirmar que o código é mais explícito. Os métodos são criados de uma vez só, tornando o comportamento da classe `Numeric` mais previsível. Ferramentas de desenvolvimento e outros programadores conseguem inspecionar a classe e ver que esses métodos realmente existem.
    
Portanto, o código acima deve é recomendado por questões de melhorias na clareza, manutenibilidade e velocidade.

**b)** Inicialmente, a resolução proposta é:

```ruby
class String

    # Define um novo método de instância chamado 'palindrome?'.
    # A interrogação no final é uma convenção em Ruby para métodos
    # que retornam um valor booleano (true ou false).
    def palindrome?

        # 1. Prepara a string para a verificação.
        #    - self: Refere-se à própria string na qual o método foi chamado (ex: 'foo').
        #    - .downcase: Converte toda a string para minúsculas, para que a
        #                 comparação não diferencie maiúsculas de minúsculas
        #    - .gsub(/\W+/, ''): Remove todos os caracteres que não são de "palavra".
        #      A expressão regular /\W+/ encontra um ou mais caracteres que NÃO são
        #      letras, números ou underscore.
        processed_string = self.downcase.gsub(/\W+/, '')

        # 2. A verificação do palíndromo.
        #    Compara a string processada com a sua versão invertida (.reverse).
        #    Esta expressão retorna 'true' se forem iguais e 'false' caso contrário.
        #    Como é a última linha do método, seu resultado é retornado implicitamente.
        processed_string == processed_string.reverse
    end
end

puts "#{'foo'.palindrome?}"
frase = "A man, a plan, a canal -- Panama"
# 1. frase.downcase.gsub(/\W+/, '') -> "amanaplanacanalpanama"
# 2. "amanaplanacanalpanama" == "amanaplanacanalpanama".reverse -> true
puts "#{frase.palindrome?}"
```

Uma outra solução é:

```ruby
class String

    def palindrome?
        processed_string = self.downcase.gsub(/\W+/, '')
        len = processed_string.length

        # Itera apenas até a metade da string.
        (0...len / 2).each do |i|
            # Compara o caractere da esquerda (índice 'i') com o seu
            # correspondente da direita (índice '-(i + 1)').
            if processed_string[i] != processed_string[-(i + 1)]

                # Se em qualquer ponto os caracteres forem diferentes,
                # então não é um palíndromo.
                return false
            end
        end

        # Se o loop terminar sem encontrar nenhuma diferença,
        # significa que a string é um palíndromo.
        true
    end
end

frase = "A man, a plan, a canal -- Panama"
puts "#{frase.palindrome?}"

puts

palavra = "hello"
puts "#{palavra.palindrome?}"
```

Ambas as soluções propostas possuem complexidade O(n). Em questão de memória, a implementação anterior não cria novas strings, algo que economiza memória. Além disso, a implementação acima é recomendada ao trabalhar com strings muito grandes ou quando se trabalha com gargalos de performance comprovados.

Portanto, a implementação modificada é levemente mais eficiente que a primeira solução proposta. Porém, esta é a solução preferível na maioria dos casos.

**c)** Inicialmente, a resolução proposta é:

```ruby
module Enumerable

    # Define o método palindrome? para coleções em geral.
    def palindrome?

        # 1. Converte o enumerável para um array.
        #    O método .to_a é fornecido pelo próprio módulo Enumerable. Ele transforma
        #    qualquer coleção (seja um Range, um Hash, etc.) em um array simples de seus elementos.
        elementos = self.to_a
        
        # 2. Compara o array de elementos com sua versão invertida.
        #    A lógica é a mesma da string, mas agora funciona para qualquer
        #    sequência de elementos, não apenas caracteres.
        elementos == elementos.reverse
    end
end

puts "#{[1, 2, 3, 2, 1].palindrome?}" # => true
puts "#{['a', 'b', 'a'].palindrome?}" # => true
puts "#{[1, 2, 3].palindrome?}" # => false
puts "#{(1..5).palindrome?}" # => false
```

Uma solução alternativa seria:

```ruby
module Enumerable

    def palindrome?

        # A conversão para array ainda é necessária, pois Enumerable não garante
        # acesso a elementos por índice (ex: um 'Range' ou um enumerador 'lazy').
        # A otimização aqui é que evitamos criar o SEGUNDO array (o invertido).

        arr = self.to_a
        len = arr.length

        # Itera apenas até a metade do array.
        (0...len / 2).each do |i|
            # Compara o elemento da esquerda (arr[i]) com o da direita (arr[-(i + 1)]).
            if arr[i] != arr[-(i + 1)]
                return false # Se encontrar uma diferença, já sabemos que não é um palíndromo.
            end
        end

        # Se o loop terminar sem encontrar diferenças, a coleção é um palíndromo.
        true
    end
end

class String
    # Sobrescreve-se o método de Enumerable com uma versão para strings.
    def palindrome?
        # A etapa de limpeza continua sendo a mais importante.
        processed_string = self.downcase.gsub(/\W+/, '')
        len = processed_string.length

        # Aplica-se a mesma lógica de "dois ponteiros" diretamente na string processada.

        (0...len / 2).each do |i|
            if processed_string[i] != processed_string[-(i + 1)]
                return false
            end
        end
        true
    end
end

puts "#{[1, 2, 1].palindrome?}"
# => true
puts "#{'A man, a plan, a canal -- Panama'.palindrome?}"
# => true
puts "#{'hello'.palindrome?}"
# => false
```

A solução anterior faz uso de menos memória, uma vez que não cria uma coleção extra invertida. Porém, possui a desvantagem de ser mais verboso e com lógica mais complexa.

Dessa forma, para facilidade de leitura e simplicidade de implementação, o primeiro código é a melhor escolha. A fim de salvar recursos de memória, a segunda implementação é a mais indicada.

---

## **Conclusão**

Diante de todos os códigos implementados pela presente autora desse trabalho e pela IA do Google (Gemini), é possível afirmar que o Gemini conseguiu propor respostas excelentes, desde o aspecto da clareza do código até aspectos como velocidade e memória. Além disso, por mais que seja muito mais fácil e prático utilizar métodos já contidos na linguagem Ruby (como .reverse, .sort etc), o seu uso pode não ser a melhor alternativa em todos os casos. Isso se deve ao fato de que há uma tendência a alocar grandes espaços na memória (principalmente), o que desfavorece a implementação em si.

Portanto, cabe ao desenvolvedor escolher a melhor implementação para o seu projeto. Nesse caso, o uso alguma IA como um guia pode ser uma excelente escolha, uma vez que esta pode auxiliar na construção de um projeto eficiente e que atenda aos requisitos esperados dos stakeholders.


