# Two Sums
**Nível**:
- [X] Fácil ✅
- [ ] Médio ⚠️ 
- [ ] Difícil 🛑

**Link**: [Two Sums](https://leetcode.com/problems/two-sum/)

## Problema
Dado um array de números inteiro, retorne o índice de dois números que somados resultam no valor target passado.

Você pode assumir que cada input terá exatamente uma solução, and não serão utilizados o mesmo elemento duas vezes.

**Exemplo:**
```
Dado nums = [2, 7, 11, 15], target = 9,

Já que nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
## Explicações

A explicação é sempre dividia em duas partes. A minha resolução sozinho ~~(que nem sempre é a melhor rs)~~. E por fim uma resolução feita com base em outros conteúdos, respostas dos usuários do leetcode, vídeos e etc.

### *Resolução 01*

**Usuário:** [guibas741](https://github.com/guibas741)

**Linguagem:** Javascript

**Tempo de execução:** 132 ms

**Uso de memória:** 37.1 MB

#### Solução

Para essa solução eu utilizei um loop dentro do outro, passando por todos os valores e comparando se o valor da soma era igual o valor target passado.

1. Criar um loop que passe por todos os valores do array, então se tiver um array de `[1, 4, 5, 8]` ele vai passar por cada número uma vez.
2. Criar um loop pra percorrer novamente o array.
3. Comparar se o valor somado do numero atual no primeiro loop com o número atual no segundo loop é igual ao valor target.
4. Se for igual comparar também se os números no primeiro e no segundo loop são diferentes.
5. Retornar o índice do primeiro loop e do segundo.

```javascript
var twoSum = function(nums, target) {
  for(let i = 0; i < nums.length; i++) { // 1
      for(let j = 0; j < nums.length; j++) { // 2
          if(nums[i] + nums[j] === target && // 3
            i !== j) { // 4
              return [i,j]; // 5
          }
      }
  }
};
```

**Código final:**
```javascript
var twoSum = function(nums, target) {
  for(let i = 0; i < nums.length; i++) {
    for(let j = 0; j < nums.length; j++) {
      if(nums[i] + nums[j] === target && i !== j) {
        return [i,j];
      }
    }
  }
};
```

### Explicação passo a passo

Digamos que recebemos o array `[2, 4, 5]` e o valor target é `9`.

1. Primeiro vamos percorrer todo o array para ter o primeiro número na soma.
2. Depois vamos percorrer novamente o array para termos o segundo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |

3. Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `2 + 2 = 4` e o valor que queremos é `9` então vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |

4. Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `2 + 4 = 6` e o valor que queremos é `9` então vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |
| 2       | 5       |

5. Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `2 + 5 = 7` e o valor que queremos é `9` então vamos para o próximo número. Nesse caso o segundo loop chegou ao final do array, então voltamos o 2 valor para o inicio no primeiro loop e vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |
| 2       | 5       |
| 4       | 2       |

6. Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `4 + 2 = 6` e o valor que queremos é `9` então vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |
| 2       | 5       |
| 4       | 2       |
| 4       | 5       |

7. Comparamos se o valor da soma deles é igual ao target `4 + 5 = 9` e o valor que queremos é `9` então comparamos se os valores não representam o mesmo índice no array, O valor 4 é o índice 1 e o valor 5 é o índice 2 então podemos retornar [1, 2].

### *Resolução 02*

**Usuário:** [Terrible Whiteboard](https://www.patreon.com/terriblewhiteboard)

**Fonte:** [vídeo](https://www.youtube.com/watch?v=U8B984M1VcU&feature=emb_logo)

**Linguagem:** `Javascript`

**Tempo de execução:** `60 ms`

**Uso de memória:** `35.1 MB`

#### Solução

Terrible Whiteboard é um youtuber que cria conteúdo resolvendo problemas do leetcode. Para essa solução ele utilizou [Map](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/map) para mapear o elemento que você está e seu índice. Com o elemento que você está compara se a diferença entre ele e o valor target existe no `Map`. Se existe você encontrou a solução.

1. Primeiro é criado um `Map`.
2. Cria um result como um array vazio. Caso não tenha resposta o retorno será essa variável result.
3. Cria um loop com for para percorrer o array por completo.
4. Salva o valor atual em uma variável num que recebe o elemento atual, ou seja, nums[i];
5. Salva a diferença entre o valor atual e o valor target na variável complement;
6. Checar se o `Map` tem o valor da diferença já salvo.
7. Se tiver o valor dentro do `Map`, o primeiro valor do resultado será o índice da diferença(variável complement).
8. E o segundo valor do resultado será o índice do elemento atual, ou seja, `i`.
9. Retorna o resultado.
10. Caso não tenha encontrar o valor. Adiciona o elemento atual `num` e o seu índice `i` ao `Map`.

```javascript
var twoSums = function(nums, target) {
  let numberIndex = new Map() // 1

  let result = []; // 2

  for(let i = 0; i < nums.length; i++) { // 3
    let num = nums[i]; // 4
    let complement = target - num; // 5

    if(numberIndex.has(complement)) { // 6
      result[0] = numberIndex.get(complement); // 7
      result[1] = i; // 8

      return result; // 9
    }

    numberIndex.set(num, i); // 10
  }

  return result;
};
```

**Código final:**
```javascript
var twoSums = function(nums, target) {
  let numberIndex = new Map();
  let result = [];

  for(let i = 0; i < nums.length; i++) { 
    let num = nums[i];
    let complement = target - num; 

    if(numberIndex.has(complement)) { 
      result[0] = numberIndex.get(complement); 
      result[1] = i;
      return result; 
    }
    numberIndex.set(num, i); 
  }
  return result;
};
```

### Explicação passo a passo

Digamos que o array tem valor `[2, 5, 7, 4]` e o valor target é `9`.

1. Pegamos o primeiro elemento do array que é o 2 e vemos a diferença entre o valor target 9. `9 - 2 = 7`.

| Elemento | MAP     |
|----------|---------|
| 2        |         |

2. 7 se encontra em nosso map? Não, então adicionamos o `2` e o seu índice que é `0` ao `Map`.

| Elemento | MAP     |
|----------|---------|
| 2        | 2:0     |

3. Vamos ao próximo elemento.

| Elemento | MAP     |
|----------|---------|
| 2        | 2:0     |
| 5        |         |

4. Vemos a diferença entre o valor do target e o elemento. `9 - 5 = 4`. Temos 4 em nosso `Map`? Não, então adicionamos o `5` e seu índice que é `1` ao `Map`. 

| Elemento | MAP     |
|----------|---------|
| 2        | 2:0     |
| 5        | 5:1     |

5. Vamos ao próximo elemento.

| Elemento | MAP     |
|----------|---------|
| 2        | 2:0     |
| 5        | 5:1     |
| 7        |         |

6. Vemos a diferença entre o valor do target e o elemento. `9 - 7 = 2`. Temos `2` em nosso `Map`? Sim! Então pegamos o índice do valor `2` que está salvo em nosso `Map` e o índice do valor do elemento que estamos 7 e retornamos como resposta. 
7. Reposta [0, 2].

 







