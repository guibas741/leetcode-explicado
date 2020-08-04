# Reverse Integer
**Nível**:
- [X] Fácil ✅
- [ ] Médio ⚠️ 
- [ ] Difícil 🛑

**Link**: [Reverse Integer](https://leetcode.com/problems/reverse-integer/)

## Problema

Dado um número inteiro 32 bits, reverta os digitos do número.

**Exemplo 1:**
```
Input: 123
Output: 321
```

**Exemplo 2:**
```
Input: -123
Output: -321
```

**Exemplo 3:**
```
Input: 120
Output: 21
```

Nota:
Assuma que estamos lidando com um ambiente que só pode armazenar números dentro do intervalo inteiro assinado de 32 bits: [−231, 231 - 1]. Para o propósito do problema, assuma que sua função retorne 0 caso o valor invertido ultrapasse o intervalo.

## Explicações

A explicação é sempre dividia em duas partes. A minha resolução sozinho ~~(que nem sempre é a melhor rs)~~. E por fim uma resolução feita com base em outros conteúdos, respostas dos usuários do leetcode, vídeos e etc.

### *Resolução 01*

**Usuário:** [guibas741](https://github.com/guibas741)

**Linguagem:** `Javascript`

**Tempo de execução:** `92 ms`

**Uso de memória:** `38.7 MB`

#### Solução

A minha ideia foi utilizar do método [reverse()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) do JavaScript para solucionar esse problema. Como esse é um método específico para arrays, minha solução foi a seguinte: 

1. Transformar a variável x em uma string e logo após dar um split nela para transforma-la em um array.
2. Checar se o valor de x é negativo e guardar essa resposta em uma variável `negative`.
3. Caso seja negativo, remover o simbolo `-` utilizando o método [splice()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) que é o primeiro elemento do array.
4. Criar uma variável e armazenar o array invertido.
5. Percorrer o array invertido,
6. Adicionar cada elemento do array em uma string `result`.
7. Transformar a string `result` em um número.
8. Checar se o valor inteiro do resultado é maior que o valor de `32 bits`. Se for retornar 0.
9. Checar se o valor negativo era `true` caso seja, multiplicar por -1 o resultado final, se negative for `false` retornar o resultado.

```javascript
var reverse = function(x) {
    const list = (""+x).split(""); // 1
    const negative = x < 0; // 2
    if (negative) {
      list.splice(0, 1); // 3
    }
    
    const invertedList = list.reverse(); // 4
    
    let result = '';
    invertedList.forEach((num) => { // 5
        result +=  num; // 6
    });
    
    const resultNumber = Number(result); // 7
    if(resultNumber > 0x7FFFFFFF) { // 8
        return 0;
    }
    
    return negative ? resultNumber * -1 : resultNumber; // 9
};
```

**Código final:**

```javascript
var reverse = function(x) {
  const list = (""+x).split("");
  const negative = x < 0;
  if(negative) {
    list.splice(0, 1);
  }
  
  const invertedList = list.reverse();
  
  let result = '';
  invertedList.forEach((num) => {
    result +=  num;
  });
  
  const resultNumber = Number(result);
  if(resultNumber > 0x7FFFFFFF) {
    return 0;
  }
  
  return negative ? resultNumber * -1 : resultNumber;
};

```


 







