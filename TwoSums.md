# Nome do problema
**Nível**:
- [X] Fácil ✅
- [ ] Médio ⚠️ 
- [ ] Difícil 🛑
**Link**: [Two Sums](https://leetcode.com/problems/two-sum/)

## Problema
Dado um array de números inteiro, retorne o índice de dois números que sumados resultam no valor target passado.

Você pode assumir que cada input terá exatamente uma solução, and não serão utilizados o mesmo elemento duas vezes.

**Exemplo:**
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
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

1 - Criar um loop que passe por todos os valores do array, então se tiver um array de `[1, 4, 5, 8]` ele vai passar por cada número uma vez.
2 - Criar um loop pra percorrer novamente o array.
3 - Comparar se o valor somado do numero atual no primeiro loop com o número atual no segundo loop é igual ao valor target.
4 - Se for igual comparar também se os números no primeiro e no segundo loop são diferentes.
5 - Retornar o índice do primeiro loop e do segundo.

```javascript
var twoSum = function(nums, target) {
  for(let i = 0; i < nums.length; i++) { //1
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

1 - Primeiro vamos percorrer todo o array para ter o primeiro número na soma.

2 - Depois vamos percorrer novamente o array para termos o segundo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |

3 - Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `2 + 2 = 4` e o valor que queremos é `9` então vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |

4 - Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `2 + 4 = 6` e o valor que queremos é `9` então vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |
| 2       | 5       |

5 - Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `2 + 5 = 7` e o valor que queremos é `9` então vamos para o próximo número. Nesse caso o segundo loop chegou ao final do array, então voltamos o 2 valor para o inicio no primeiro loop e vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |
| 2       | 5       |
| 4       | 2       |

6 - Comparamos se o valor da soma deles é igual ao target, se nao for o 2 valor vai para o próximo número no array. `4 + 2 = 6` e o valor que queremos é `9` então vamos para o próximo número.

| 1 valor | 2 valor |
|---------|---------|
| 2       | 2       |
| 2       | 4       |
| 2       | 5       |
| 4       | 2       |
| 4       | 5       |

7 - Comparamos se o valor da soma deles é igual ao target `4 + 5 = 9` e o valor que queremos é `9` então comparamos se os valores não representam o mesmo índice no array, O valor 4 é o índice 1 e o valor 5 é o íncide 2 então podemos retornar [1, 2].




 







