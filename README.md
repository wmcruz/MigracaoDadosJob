# MigracaoDadosJob - Spring Batch
Projeto Java utilizando Spring Boot.

## Objetivo 
Ler 20 mil dados em arquivo.csv, sendo:
- 10 mil pessoas
- 10 mil dados bancários

*Esses dados são ficticios!*

Após a leitura o programa irá realizar o processamento e escrita. Podendo ser feito a escrita em um banco de dados em MySql ou novamente em um arquivo .csv de registros inválidos.

## Reader
### Pessoas
Realiza a leitura do arquivo */files/pessoas.csv*

### Dados Bancários
Realiza a leitura do arquivo */files/dados_bancarios.csv*

## Processor and Writer
### migrarPessoasStep
Através do __ClassifierCompositeItemWriter__ o nosso *stepConfig* direciona o programa para filtrar se uma pessoa é valida ou não. (Se nome, email ou data de nascimento não estão em branco ou inválidos).
Caso a pessoa seja válida, a gravação do dado processado será feita no Banco de Dados, caso contrário será criado um arquivo */files/pessoas_invalidas.csv* com os *IDs* das pessoas inválidas.

### migrarDadosBancariosStep
Nesse caso foi utilizado apenas o ItemWriter para realizar a escrita no BD.

### Importante
O job trabalha com os dois steps em paralelo.

## Utilização
Após realizar o 'fork/clone', execute o comando `docker compose up` para subir a instancia do mysql no docker.
Caso queira subir uma instancia do DB mysql diferente de um container, o script para criação dos bancos e tabelas estão na pasta __/mysql/init.sql__

Não esqueça de configurar usuário e senha do banco no arquivo de properties do projeto. <br />
Mas caso queira mudar a implementação da base, ou o tipo do BD, basta mudar os apontamentos:

- pom.xml
- application.properties
- DataSourceConfig.java
