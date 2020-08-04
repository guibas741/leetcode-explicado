# Palindrome Number
**Nível**:
- [X] Fácil ✅
- [ ] Médio ⚠️ 
- [ ] Difícil 🛑

**Link**: [Palindrome Number](https://leetcode.com/problems/palindrome-number/)

## Problema
Determinar quando um integer é um palíndromo. Um integer é um palíndromo quando ele se lê igual de trás para frente. 

**Exemplo 1:**
```
Input: 121
Output: true
```

**Exemplo 2:**
```
Input: -121
Output: false
Explanation: Da esquerda para a direita, se lê -121. Da direita para a esquerda, ele se torna 121-. Ou seja, não é um palíndromo.
```

**Exemplo 3:**
```
Input: 10
Output: false
Explanation: Da direita para a esquerda se lê 01. Ou seja, não é um palíndromo.
```


## Explicações

A explicação é sempre dividia em duas partes. A minha resolução sozinho ~~(que nem sempre é a melhor rs)~~. E por fim uma resolução feita com base em outros conteúdos, respostas dos usuários do leetcode, vídeos e etc.

### *Resolução 01*

**Usuário:** [guibas741](https://github.com/guibas741)

**Linguagem:** `Javascript`

**Tempo de execução:** `236 ms`

**Uso de memória:** `47 MB`

#### Solução

A minha ideia foi utilizar do método [reverse()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) do JavaScript para solucionar esse problema. Como esse é um método específico para arrays, minha solução foi a seguinte: 
 
1. Utilizar o `String(x)` para garantir que a variável x que estou recebendo vai ser transformada em uma string, ou seja, se eu recebi um valor `-121` agora ele é `'-121'`.
2. Dar um [split()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/String/split) na string, transformando-a assim em um array. Então agora o valor `'121'` acabou virando `['-', '1', '2', '1']`.
3. Usar o [reverse()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) neste array, minha variável agora é `['1', '2', '1', '-']`
4. Após ter a variável numberArray, eu criei uma variável numberString para poder comparar com o valor de x. Para isso utilizei o [join()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/join) um método do JavaScript para unificar arrays.
5. Após transformar o meu numberArray `['1', '2', '1', '-']` na minha variável numberString `'121-'`, tento transforma-lá em um Number, nesse caso específico o output será [NaN (Not-a-Number)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/NaN), ou seja, *Não é um número*.
6. Por fim retorno uma comparação entre o valor de x e o valor de number. `True` se forem iguais, `false` se forem diferentes.


```javascript
var isPalindrome = function(x) {
  const numberArray = String(x) // 1,
    .split("") // 2
    .reverse(); // 3

  const numberString = numberArray.join("") // 4
  const number = Number(numberString) // 5

  return x === number; // 6
};
```

**Código final:**
```javascript
var isPalindrome = function(x) {
  const numberArray = String(x).split("").reverse();
  const number = Number(numberArray.join(""));
  
  return x === number;
};
```

### *Resolução 02*

**Usuário:** [Terrible Whiteboard](https://www.patreon.com/terriblewhiteboard)

**Fonte:** [vídeo](https://www.youtube.com/watch?v=gnwFjlUXN1o&feature=emb_logo)

**Linguagem:** `Javascript`

**Tempo de execução:** `164 ms`

**Uso de memória:** `44.8 MB`

#### Solução

Terrible Whiteboard é um youtuber que cria conteúdo resolvendo problemas do leetcode. Para essa solução ele utilizou a seguinte abordagem:

1. Primeiro ele checa se o valor é negativo, já que todo número negativo não é um palíndromo.
2. Ele cria o retorno comparando x com o valor retornado da função `reversedInteger()`;
3. É criada uma variável `reversed` e inicializada com 0.
4. Cria um loop `while` enquanto o valor de x não for 0, vai continuar executando o código.
5. Utiliza o operator [módulo %](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#M%C3%B3dulo) para pegar o resto da divisão de x por 10. E soma isso ao valor de reversed * 10.
6. Atribui a x o valor arredondado para baixo, usando [Math.floor()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) de x dividido por 10.
7. Quando x for menor igual a 0, vai sair do loop e retornar o valor de reversed;

```javascript
var isPalindrome = function(x) {
  if (x < 0) {// 1
    return false;
  }

  return x === reversedInteger(x); // 2
}

var reversedInteger = function(x) {
  let reversed = 0; // 3

  while (x > 0) { // 4
    reversed = (reversed * 10) + (x % 10); // 5
    x = Math.floor(x / 10); // 6
  }

  return reversed; // 7
}
```

**Código final:**
```javascript
var isPalindrome = function(x) {
  if (x < 0) {// 1
    return false;
  }

  return x === reversedInteger(x);
}

var reversedInteger = function(x) {
  let reversed = 0; 

  while (x > 0) { 
    reversed = (reversed * 10) + (x % 10); 
    x = Math.floor(x / 10); 
  }

  return reversed; 
}
```

### Explicação passo a passo

1. Reverter 49 para que seja 94.
2. Cria uma coluna Invertido que sempre inicia com 0.
3. Cria um coluna atual que mantém o estado do valor original.

| Invertido | Atual |
|-----------|-------|
| 0         | 49    |

4. Analisamos que o último número original precisa ser o primeiro invertido, ou seja. 9 vai ser o primeiro numero do Invertido.
5. Para fazer isso, dividir o valor atual (49) por 10 e pegar o resto. `49 % 10 = 9`.
6. Para ter certeza que o primeiro número é 9 é preciso pegar o valor do Invertido, multiplicar por 10 e somar com o valor resto da divisão. Então `Invertido = (0 * 10) + 9;`.

| Invertido | Atual |
|-----------|-------|
| 0         | 49    |
| 9         | 49    |

7. Agora é necessário remover o número 9 do atual. Para isso dividir o valor de atual por 10 e arredondar para baixo. `49 / 10 = 4.9` e 4.9 arredondado para baixo é 4. Ou seja, 4 é o valor atual agora.

| Invertido | Atual |
|-----------|-------|
| 0         | 49    |
| 9         | 49    |
| 9         | 4     |

8. A partir disso é só repetir o processo (passos 4, 5, 6, 7) até que o valor atual seja 0.
9. Pegar o valor atual que agora é 4 dividir por 10 e pegar o resto. `4 % 10 = 4`.
10. Pegar o valor invertido, que agora é 9 multiplicar por 10 e somar ao resto da divisão. `invertido = (9 * 10) + 4;`.

| Invertido | Atual |
|-----------|-------|
| 0         | 49    |
| 9         | 49    |
| 9         | 4     | 
| 94        | 4     | 

11. Remover o número 4 do atual. Dividimos o valor por 10 e arredondamos para baixo. `4 / 10 = 0.4` e 0.4 arredondado para baixo é 0. O valor de atual é 0 e olhando no passo 8 lembramos que quando o valor atual é 8 ele retorna o invertido.

| Invertido | Atual |
|-----------|-------|
| 0         | 49    |
| 9         | 49    |
| 9         | 4     | 
| 94        | 4     | 
| 94        | 0     |

12. Valor invertido = 94.





