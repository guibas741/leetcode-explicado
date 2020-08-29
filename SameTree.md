# Same Tree
**Nível**:
- [X] Fácil ✅
- [ ] Médio ⚠️ 
- [ ] Difícil 🛑

**Link**: [Link para o problema](https://leetcode.com/problems/same-tree/)

## Problema
Dado duas árvores binárias, escreva uma função para verificar se elas são as mesmas ou não.

Duas árvores binárias são consideradas as mesmas se são estruturalmente iguais e seus nodes tem o mesmo valor.

**Exemplo 1:**
```
Entrada:   1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Saída: true
```

**Exemplo 2:**
```
Entrada:   1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Saída: false
```

**Exemplo 3:**
```
Entrada:   1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Saída: false
```
## Explicações

A explicação é sempre dividia em duas partes. A minha resolução sozinho ~~(que nem sempre é a melhor rs)~~. E por fim uma resolução feita com base em outros conteúdos, respostas dos usuários do leetcode, vídeos e etc.

### *Resolução 01*

**Usuário:** [Terrible Whiteboard](https://www.patreon.com/terriblewhiteboard)

**Fonte:** [vídeo](https://www.youtube.com/watch?v=G9wwY-cmuiE&feature=youtu.be)

**Linguagem:** `Javascript`

**Tempo de execução:** `48 ms`

**Uso de memória:** `33.8 MB`

#### Solução

Para esse problema foi utilizado [Recursividade](https://pt.wikipedia.org/wiki/Recursividade_(ci%C3%AAncia_da_computa%C3%A7%C3%A3o)) em sua solução, a idéia é simples: 

1. Verificar se um dos dois valores recebidos é null, que significa que o node não existe. 
2. Caso seja null, retorne a comparação entre o valor do primeiro com o segundo. A ideia aqui é que se algum valor for diferente a função retorna _false_ e para. Caso seja _true_ também retorna e para a função.
3. Caso nenhum dos dois valores seja null, vamos verificar se os valores são diferentes.
4. Se forem diferentes retorna _false_ e para a função.
5. Se já passamos por toda a verificação de null e valores diferentes, podemos seguir agora pra nossa recursividade. Vamos sempre iniciar verificando o node da direita, então chamamos a função _isSameTree_ passando os valores do node _right_. Ele vai começar acessar os valores da direita da árvore e executar a mesma verificação, até encontrar um valor diferente ou chegar ao fim da parte direita da arvore.
6. Após verificar a parte direita vamos fazer o mesmo processo para a esquerda da árvore passando os valores de _left_. A idéia é a função ir se repetindo verificando os valores, mesmo quando um node da esquerda tiver valores na direita e esquerda, a função _isSameTree_ vai buscar as comparações.

```javascript
var isSameTree = function(p, q) {
    if(p === null || q === null) { // 1
        return p === q; // 2
    }
    
    if(p.val !== q.val) { // 3
        return false; // 4
    }
    
    return isSameTree(p.right, q.right) // 5
    && isSameTree(p.left, q.left); // 6
};
```

**Código final:**
```javascript
var isSameTree = function(p, q) {
    if(p === null || q === null) { 
        return p === q;
    }
    
    if(p.val !== q.val) {
        return false;
    }
    
    return isSameTree(p.right, q.right) && isSameTree(p.left, q.left);
};
```

### Explicação passo a passo

Nossa entrada será:
```
       1        1
      / \      / \
     2   1    2   1
    / \      / \
   4   5    4   7
```
1. Recebemos nossas duas árvores e agora vamos iniciar nossa comparação.
```
       1 <-     1 <-
      / \      / \
     2   1    2   1
    / \      / \
   4   5    4   7
```
2. Primeiro vamos ver se o valor inicial é null, caso seja vamos verificar se o valor da segunda árvore também é null. 
```javascript
if(p === null || q === null) { 
  return p === q;
}
```
O primeiro valor é diferente de null em ambas as árvores então não podemos entrar nessa condição.
3. Então vamos verificar se os valores são diferentes.
```javascript
if(p.val !== q.val) {
    return false;
}
```
O valor do node que estamos comparando na primeira árvore é 1 e da segunda também é 1 então podemos prosseguir.
4. Agora vamos começar a recursividade, lembrando que primeiro comparamos os valores da DIREITA da árvore.
```
       1        1 
      / \      / \
     2   1<-  2   1<-
    / \      / \
   4   5    4   7
```
```javascript
return isSameTree(p.right, q.right) && isSameTree(p.left, q.left);
```
A ideia é que executemos a função _isSameTree_ quantas vezes forem necessárias até encontrarmos um valor diferente ou passarmos pela árvore inteira.
5. O próximo valor na direita em ambas as árvores é diferente de null, então podemos pular essa comparação.
```javascript
if(p === null || q === null) { 
  return p === q;
}
```
6. Vamos verificar se os valores são diferentes. Como o valor do node que estamos das duas árvores é 1 podemos pular essa condição também.
```javascript
if(p.val !== q.val) {
    return false;
}
```
7. Voltamos para a recursividade. E de novo damos prioridade para o valor da direita.
```javascript
return isSameTree(p.right, q.right) && isSameTree(p.left, q.left);
```
8. O valor da direita em ambas as árvores agora é null, então já caímos na primeira condição
```
        1                    1   
      /   \                /   \
     2     1              2     1
    / \    / \           / \    / \
   4   5 null null<-    4   7  null null<-
```
```javascript
if(p === null || q === null) { 
  return p === q;
}
```
Como os dois valores são null, vamos retornar _true_.
9. Agora vamos chegar os nodes da esquerda _&& isSameTree(p.left, q.left)_.
10.  O valor da esquerda em ambas as árvores agora é null, então já caímos na primeira condição
```
        1                     1   
      /   \                /     \
     2      1              2       1
    / \    /  \           / \    /   \
   4   5 null<- null    4   7  null<- null
```
```javascript
if(p === null || q === null) { 
  return p === q;
}
```
Como os dois valores são null, vamos retornar _true_.
11. Retornamos agora lá para o primeiro node
```
       1 <-       1 <-
      / \        / \
     2   1      2   1
    / \        / \
   4   5      4   7
```
12. Agora vamos ver o valor da esquerda neles
```
       1            1 
      /  \         /  \
     2<-  1       2<-  1 
    / \          / \
   4   5        4   7
```
13. Repetimos todo o processo, verificamos que os dois valores não são nulos e que são iguais nas duas árvores, 2 e 2.
14. Vamos para o próximo node com a recursividade, priorizando os valores da DIREITA
```
       1            1 
      / \          / \ 
     2   1        2   1
    / \          / \
   4   5 <-     4   7 <-
```
15. Verificamos que o valor não é nulo em ambas as árvores.
```javascript
if(p === null || q === null) { 
  return p === q;
}
```
16. Verificamos que os valores são DIFERENTES. Então retornamos _false_. Como eles são diferentes não verificamos os nodes a direita e esquerda do valor 5 e 7.
17. Voltamos para o node de cima. 
```
       1            1 
      /  \         /  \
     2<-  1       2<-  1 
    / \          / \
   4   5        4   7
```
18.E fazemos a comparação do node da esquerda, por mais que já não importe pois uma vez que o valor for _false_ constatamos que as árvores são diferentes. 
```
       1          1 
      / \        / \
     2   1      2   1
    / \        / \
   4<- 5      4<- 7
```
19. No final nossa saída será _false_.







