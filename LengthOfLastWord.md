# Nome do problema
**Nível**:
- [x] Fácil ✅
- [ ] Médio ⚠️ 
- [ ] Difícil 🛑

**Link**: [Length of last word](https://leetcode.com/problems/length-of-last-word/)

## Problema
Dada uma string s que consiste de palavras em maiúsculo e minusculo e espaços em branco, retorne o tamanho da última palavra(lendo a linha da esquerda para a direita) que aparece na string.

Se a última palavra não existe, retorne 0.

**Exemplo:**
```javascript
Input: "Hello World"
Output: 5
```

## Explicações

A explicação é sempre dividia em duas partes. A minha resolução sozinho ~~(que nem sempre é a melhor rs)~~. E por fim uma resolução feita com base em outros conteúdos, respostas dos usuários do leetcode, vídeos e etc.

### *Resolução 01*

**Usuário:** [guibas741](https://github.com/guibas741)

**Linguagem:** Javascript

**Tempo de execução:** 80 ms

**Uso de memória:** 38 MB

#### Solução
A minha abordagem pra essa resolução foi encontrar onde se localizava a última palavra e contar seus caractéres com o método `length`.

1. Primeiro verificamos se existem palavras na string, utilizamos o método `trim()` para remover os espaços em branco e analisamos se o tamanho da string é menor que 1, se for retornamos 0.
2. Depois separamos as palavras da string com o método `split` passando o espaço em branco como argumento para dividir a string em elementos de um array.
3. Depois vamos buscar o último valor desse array e guarda-lo em uma variável.
4. Se o tamanho da última palavra for menor que 1, ou seja, um valor em branco. Vamos buscar então do penúltimo.
5. Agora vamos entrar em um loop. Primeiro criamos uma variável que vai controlar os indices pelos quais vamos passar em nosso array de palavras e inicializa-lo com o valor de 1. Iniciamos ele com o valor de 1 pois já eliminamos um valor do nosso array.
6. Agora criamos o loop `while`. Vamos navegar pelo nosso array de trás pra frente buscando sempre a última palavra existente para encontrar seu tamanho. Usamos o `while` pois já verificamos que existe uma string com valor dentro de nosso array, mas não sabemos onde ela está localizada.
7. Aumentamos o nosso valor de i para subtrairmos do tamanho inteiro do array de palavras e vamos atribuindo nossa variável ao valor do array no índice [`tamanho do array` - `numero de voltas no while`].
8. No final retornamos o tamanho da string.

```javascript
if(s.trim().length < 1) { // 1
    return 0;
  }
  
  const words = s.split(" "); // 2

  let lastWord = words[words.length-1] // 3
  if(lastWord.length < 1) { // 4
    let i = 1; // 5
    while(lastWord.length < 1) { // 6
      i = i + 1;
      lastWord = words[words.length-i]; // 7
    }
  }
  
  return lastWord.length; // 8
};
```

**Código final:**
```javascript
if(s.trim().length < 1) {
    return 0;
  }
  
  const words = s.split(" ");

  let lastWord = words[words.length-1]
  if(lastWord.length < 1) {
    let i = 1;
    while(lastWord.length < 1) {
      i = i + 1;
      lastWord = words[words.length-i];
    }
  }
  
  return lastWord.length;
};
```

### *Resolução 02*

**Usuário:** [Terrible Whiteboard](https://www.patreon.com/terriblewhiteboard)

**Fonte:** [vídeo](https://www.youtube.com/watch?v=8XW9av_8Yqc&feature=youtu.be)

**Linguagem:** `Javascript`

**Tempo de execução:** `52 ms`

**Uso de memória:** `33.9 MB`
 

#### Solução
Para essa solução a abordagem do Terrible Whiteboard foi ler a string carácter por carácter da direita para a esquerda, e encontrar onde aparecia o primeiro carácter diferente de vazio e depois onde voltava a aparecer vazio após o inicio dos caracteres não vazios.

1. Cria uma variável para contar o numero de caracteres.
2. Cria uma para ver se já apareceu algum carácter não vazio.
3. Checa se a string é vazia. Se for retorna 0;
4. Cria um loop com `for` que percorre a string de trás pra frente. 
5. Verifica se o carácter na posição atual do loop é diferente de vazio. 
6. Se for diferente de vazio, adiciona 1 a variável de conta o tamanho da palavra.
7. Transforma em `true` a variável de verifica se apareceu algum carácter diferente de vazio.
8. Caso o carácter seja vazio, verifica se já foi encontrado algum diferente de vazio. Pois isso significa que a palavra ja foi encontrada.
9. Retorna a variável que conta o número de caracteres.
```javascript
let lengthOfLastWord = function(s) {
  let lastWordLength = 0; // 1
  let beforeFirstNonEmptyChar = true; // 2

  if (s.length === 0) { // 3
    return lastWordLength;
  }

  for (let i = s.length - 1; i >= 0; i--) { // 4
    if (s.charAt(i) !== ' ') { // 5
      lastWordLength++; // 6
      beforeFirstNonEmptyChar = false; // 7
    } else if (!beforeFirstNonEmptyChar) { // 8
      break;   
    }
  }

  return lastWordLength; // 9
};
```

**Código final:**
```javascript
let lengthOfLastWord = function(s) {
  let lastWordLength = 0;
  let beforeFirstNonEmptyChar = true;

  if (s.length === 0) {
    return lastWordLength;
  }

  for (let i = s.length - 1; i >= 0; i--) {
    if (s.charAt(i) !== ' ') {
      lastWordLength++;
      beforeFirstNonEmptyChar = false;
    } else if (!beforeFirstNonEmptyChar) {
      break;   
    }
  }

  return lastWordLength;
};
```



