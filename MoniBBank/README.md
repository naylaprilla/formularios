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

## Validity State e Tratando erros

No arquivo script.js na função verificaCampo colocamos um console.log(campo.validity) 

Clicamos no campo "Data de nascimento" e depois fora dele. Neste momento o Console retorna uma lista chamada ValidityState que exibe possíveis erros de validação que ocorrem automaticamente quando interagimos com esse formulário. Neste caso todos os elementos estão retornando false, menos o valueMissing, já que deixamos o campo sem nenhum valor preenchido.
Em script.js dentro do camposDoFormulario.forEach vamos adicionar um event listener para invalid

Em script.js vamos criar uma variável const para guardar um array com os tipos de erros
E outra const com uma lista de objetos, para guardar as mensagens de erros.

tiposDeErro.forEach(erro => { //o forEach executa uma função para cada erro da lista
        if(campo.validity[erro]) { // nesta parte ele verifica dentro do validity para ver se algum campo está como true
            mensagem = mensagens[campo.name][erro]; // se algum campo estiver true então ele pega a lista de mensagens e verifica o nome do campo então atribui a mensagem específica para esse erro. 
            console.log(mensagem);
        }
    })

Mas por enquanto só estamos vendo esse erro no console. Agora vamos fazer aparecer na tela.

        const mensagemErro = campo.parentNode.querySelector(".mensagem-erro"); 

/* Aqui criamos um seletor que pega só a tag span que está no html na pasta pages abrir-conta-form.html dessa forma <span class="mensagem-erro"></span>*/
    const validadorDeInput = campo.checkValidity(); // Aqui estamos checando se o campo está válido ou não.

    if(!validadorDeInput){
        mensagemErro.textContent = mensagem; 
    }else {
        mensagemErro.textContent = "";
    }


Em valida-cpf trocamos o console.log por campo.setCustomValidity("Esse cpf não é valido.")

campo.setCustomValidity("") //Essa linha serve para resetar a mensagem de erro depois que a informação é corrigida.

PERGUNTA: Visando criar validações customizadas para o campo de CPF e de data de nascimento, tivemos que recorrer ao tipo de erro customError. Para conseguir imprimir a mensagem específica dessas validações que foram desenvolvidas manualmente foi necessário alterar o valor do customError dentro do Validity State.
Seguindo o padrão desse projeto, como poderíamos alterar o valor de customError em uma possível validação de CNPJ?
RESPOSTA: campoDoCNPJ.setCustomValidity('Esse CNPJ não é válido');
Com o método setCustomValidity é possível alterar o valor de customError. Com isso, a mensagem do erro específica de acordo com o valor da propriedade do erro dentro do validityState irá aparecer pois o valor de customError não será mais false.


## Recebendo os Dados do Formulário

const formulario = document.querySelector("[data-formulario]") // selecionamos o formulario através do data atributes

formulario.addEventListener('submit', (e) => { // Estamos escutando quando o evento de submit ou quando o formulário é enviado.
    e.preventDefault(); // esse e é de evento, ou event, aqui estamos tirando o padrão de reload da página
    const listaRespostas = {
        "nome": e.target.elements["nome"].value, // pega o alvo do evento, o elemento dele e o valor
        "email": e.target.elements["email"].value,
        "rg": e.target.elements["rg"].value,
        "cpf": e.target.elements["cpf"].value,
        "aniversario": e.target.elements["aniversario"].value,
    }

    localStorage.setItem("cadastro", JSON.stringify(listaRespostas)); 
    // aqui selecionamos o localStorage que é o armazenamento local, inserimos um item dentro desse armazenamento local, que tinha a chave cadastro que é o primeiro parâmetro e o segundo mandamos os itens da lista, onde usamos o JSON.stringify para converter esses objetos em json para salvar essas informações.

    window.location.href = "./abrir-conta-form-2.html"; // aqui criamos um direcionamento para a ultima parte do formulário.
})

Agora vamos testar se as informações estão mesmo chegando:
  Na pagina do formulário no navegador selecione inspecionar/  >> aplicattion/ Local Storage clique no endereço url
  Agora será possível ver a Key e Value, e se clicarmos em cima da value aparecem as informações.








