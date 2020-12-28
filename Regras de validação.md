# Regras de validação

#### Manter caixa checkbox marcada

`IF(`

`AND(nome_checkbox = True,`

​          `ISCHANGED(nome_checkbox)=True)`

`, False, True)`

 De acordo com a lógica de regras do SF:

1) IF - recebe a lógica booleana (que vai retornar verdadeiro ou falso), e ao final são inseridos os valores caso o retorno seja true e depois se for false (os dois últimos valores depois da vírgula são separados para inserir os valores nessa ordem, sejam booleanos, textos, números ou qualquer outro valor)

2)AND - corresponde ao && das linguagens de programação convencionais. Forma um compilado com todas as expressões booleanas, que são separadas por vírgula. A inserção delas devem ser feitas entre os parênteses.

3)ISCHANGED - verifica se o valor foi alterado, comparando com o que estava armazenado anteriormente. Se houve mudança, o valor booleano é verdadeiro.

4) Como o intuito é de manter a checkbox como está, o valor para caso o retorno do AND seja verdadeiro seria true, para que a plataforma não permita que hajam mudanças. Se for retornado false, o valor é igualado como false pois uma das condições não se aplica. 