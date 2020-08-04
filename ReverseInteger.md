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

### *Resolução 02*

**Usuário:** [Terrible Whiteboard](https://www.patreon.com/terriblewhiteboard)

**Fonte:** [vídeo](https://www.youtube.com/watch?v=XpvNcex-rc0&feature=youtu.be)

**Linguagem:** `Javascript`

**Tempo de execução:** `72 ms`

**Uso de memória:** `35.7 MB`

#### Solução

Terrible Whiteboard é um youtuber que cria conteúdo resolvendo problemas do leetcode. Para essa solução ele utilizou a seguinte abordagem:
 
1. Verifica se o valor é negativo e guarda isso em uma variável.
2. Inicializa o valor do invertido em 0.
3. Se for negativo, multiplica o valor original por `-1` para transforma-lo em positivo.
4. Cria um loop `while` enquanto o valor de x não for 0, vai continuar executando o código.
5. Utiliza o operator [módulo %](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#M%C3%B3dulo) para pegar o resto da divisão de x por 10. E soma isso ao valor de reversed * 10.
6. Atribui a x o valor arredondado para baixo, usando [Math.floor()](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) de x dividido por 10.
7. Verifica se o valor revertido é maior que o valor de 32 bits. Caso seja retorna 0. 
8. Quando x for menor igual a 0, vai sair do loop e retornar o valor de reversed. Se `negative` for true multiplica por -1 para transformar o valor em negativo.

```javascript
let reverse = function(x) {    
  let negative = x < 0; // 1
  let reversed = 0; // 2
  
  if (negative) { // 3
    x *= -1; 
  }
  
  while (x > 0) { // 4
    reversed = (reversed * 10) + (x % 10); // 5 
    x = Math.floor(x / 10); // 6
  }
  
  if (reversed > (2 ** 31 - 1)) { // 7
    return 0; 
  }
  
  return negative ? (reversed * -1) : reversed; // 8
};
```

**Código final:**

```javascript
let reverse = function(x) {    
  let negative = x < 0; 
  let reversed = 0; 

  if (negative) { 
    x *= -1; 
  }
  
  while (x > 0) { 
    reversed = (reversed * 10) + (x % 10); 
    x = Math.floor(x / 10); 
  }
  
  if (reversed > (2 ** 31 - 1)) { 
    return 0; 
  }
  
  return negative ? (reversed * -1) : reversed;
};
```

### Explicação passo a passo (inversão do número)

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






