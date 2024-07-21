Jest é um poderoso Framework de Testes em JS com foco na simplicidade.

## Matchers

Claro, aqui estão algumas das funções `expect` do Jest e suas explicações simplificadas:

- `.toBe(value)`
    
    - Verifica se o valor recebido é estritamente igual (`===`) ao valor esperado.
- `.toEqual(value)`
    
    - Verifica se o valor recebido é igual ao valor esperado. Isso é útil para verificar a igualdade de objetos ou arrays.
- `.toBeTruthy()`
    
    - Verifica se o valor recebido é verdadeiro. Qualquer valor que não seja `false`, `0`, `''`, `null`, `undefined` ou `NaN` é considerado verdadeiro.
- `.toBeFalsy()`
    
    - Verifica se o valor recebido é falso. `false`, `0`, `''`, `null`, `undefined` e `NaN` são considerados falsos.
- `.toBeUndefined()`
    
    - Verifica se o valor recebido é `undefined`.
- `.toBeDefined()`
    
    - Verifica se o valor recebido é definido, ou seja, não é `undefined`.
- `.toBeNull()`
    
    - Verifica se o valor recebido é `null`.
- `.toContain(item)`
    
    - Verifica se o valor recebido é um array que contém o item especificado.
- `.toBeGreaterThan(number)`
    
    - Verifica se o valor recebido é maior que o número especificado.
- `.toBeLessThan(number)`
    
    - Verifica se o valor recebido é menor que o número especificado.
- `.toBeCloseTo(number, precision?)`
    
    - Verifica se o valor recebido está próximo do número especificado, dentro do número de casas decimais fornecido.