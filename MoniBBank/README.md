# Validação dos campos de um formulário com JavaScript

#### Tecnologias utilizadas no projeto
* JavaScript
* HTML
* CSS

## Validação CPF

Para verificar os dados de um documento de cpf existem diversas validações que podem ser feitas com JS.
Neste formulário primeiro pegamos os campos dos imputs no arquivo script.js com document.querySelectorAll('[required]')
Depois utilizamos o médoto replace para substituir os caracteres const cpf = campo.value.replace(/\.|-/g, "") por um espaço vazio.
Agora percorremos uma lista com o objetivo de verificar se tem numeros repetidos usando a função validaNumerosRepetidos;
Na função validaPrimeiroDigito vamos validar o primeiro dígito:

        Tutorial para calcular os dígitos verificadores:
        https://www.campuscode.com.br/conteudos/o-calculo-do-digito-verificador-do-cpf-e-do-cnpj 


### Resumo da aula:
Quando estamos construindo um sistema que requer a criação de contas como o MoniBank, devemos validar os dados em que há essa possibilidade. Usando JavaScript nativamente, sem o uso de bibliotecas, iremos precisar fazer algumas validações manualmente, como a validação do CPF.

Vamos atuar em cima de um CPF base que será: 451.055.040-54. A fórmula do cálculo dos últimos dígitos verificadores de um CPF é dividida em:

Primeiro dígito
Para descobrir o primeiro dígito você precisará recolher os 9 primeiros dígitos do CPF e multiplicar por números de 10 a 2, sequencialmente.

Valor do CPF	4	5	1	0	5	5	0	4	0
Sequência	10	9	8	7	6	5	4	3	2
Resultado	40	45	8	0	30	25	0	12	0
Depois, precisamos somar todos os valores gerados nas multiplicações entre eles. Nesse caso, a soma resultou em 160. Em seguida, será necessário multiplicar essa soma por 10, que gerou o número 1600. Por fim, devemos considerar o módulo da divisão desse número com 11: 5.

Antes de decidirmos que esse é o primeiro dígito verificador, precisamos testar uma condição: Se o resultado for 10 ou 11, precisaremos zera-lo. Como não é o caso, podemos confirmar que 5 realmente é o primeiro dígito verificador do CPF base.

Segundo dígito
Para descobrir o segundo dígito você precisará recolher os 10 primeiros dígitos do CPF e multiplicar por números de 11 a 2, sequencialmente.

Valor do CPF	4	5	1	0	5	5	0	4	0	5
Sequência	11	10	9	8	7	6	5	4	3	2
Resultado	44	50	9	0	35	30	0	16	0	10
Em seguida, será necessário somar todos os valores resultados pela multiplicação novamente, e essa soma resultou em 194. Depois, multiplicamos essa soma por 10, para encontrar o valor 1940. Ao final, chegamos na etapa de encontrar o módulo da divisão por 11: o número 4.

Novamente, precisamos verificar para caso o resultado for 10 ou 11, será necessário zera-lo. Como novamente não foi o caso, o número 4 realmente é o segundo dígito verificador do CPF base.

## Validações de Idade

Criamos o arquivo valida-idade.js dentro da pasta js, neste arquivo vamos fazer o export default e criar a função ehMaiorDeIdade(campo).
Criamos a const dataNascimento = new Date(campo.value) que pega as informações de data de transforma em uma data que o JavaScript entende.
E importamos esse arquivo em script.js além de adicionar o if de aniversário na função verificaCampo.
Por fim, fazemos as comparações  na função validaIdade, colocaos um console.log(validaIdade(dataNascimento)) em ehMaiorDeIdade e verificamos a data retorna true ou false no console do navegador.

## Validity State

No arquivo script.js na função verificaCampo colocamos um console.log(campo.validity) 

Clicamos no campo "Data de nascimento" e depois fora dele. Neste momento o Console retorna uma lista chamada ValidityState que exibe possíveis erros de validação que ocorrem automaticamente quando interagimos com esse formulário. Neste caso todos os elementos estão retornando false, menos o valueMissing, já que deixamos o campo sem nenhum valor preenchido.
Em script.js dentro do camposDoFormulario.forEach vamos adicionar um event listener para invalid

Em script.js vamos criar uma variável const para guardar um array com os tipos de erros
E outra const com uma lista de objetos, para guardar as mensagens de erros.








