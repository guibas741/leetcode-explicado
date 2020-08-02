# Palindrome Number
*Nível*: fácil ✅

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
3. Usar o [reverse()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) neste array, minha variável agora é `['1', '2', '1', '-']`.
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


 







