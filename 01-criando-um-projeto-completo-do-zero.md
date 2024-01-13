# Criando um projeto completo do zero

Este tópico aborda desde a instalação dos softwares até rodar na máquina o projeto do frontend batendo no backend e apresentando os dados consultados no banco de dados.

*Obs.¹: Algumas definições podem ser encontradas no final da página.*

*Obs.²: Como instalar os softwares também está incluso nesta documentação.*

## O projeto será composto por:

- Frontend - React
- Backend - API em C#
- Banco de dados - SQL Server

## Fluxo:

[TODO]

## Softwares necessários:

- Visual Studio 22 - Versão Community + SQL Server Express 2019 LocalDB

## - Frontend - React

[TODO]

## - Backend:- API em C#

[TODO]

## - Banco de dados - SQL Server

Esta parte será dividida nas seguintes partes:

- Criar o banco de dados
- Criar as tabelas no banco de dados
- Inserir dados no banco de dados

Primeiro vamos criar a base de dados, para isto vamos no Visual Studio instalado e clicar no menu em "View" > "SQL Server Object Explorer", ao clicar em "SQL Server" haverá um servidor de banco de dados correspondente ao LocalDB Express (algo como "(localdb)(...))") e, se expandir a pasta "Databases" não haverá nenhum banco de dados lá, vamos criar o primeiro. Para isto vamos clicar com o botão direito sobre esta pasta "Databases" e depois em "Add New Database":

![SQL Server Object Explorer - Add New Database](https://github.com/jmrqs/get-started/blob/main/img/sql-server-object-exporer-add-new-database.jpg)

Em "Database Name" que irá aparecer informe "db-customers" (vamos padronizar este nome por enquanto para usarmos como referência em todo projeto) e clique em "OK".

Como segundo passo, agora vamos criar a tabela do banco de dados. Para isto clique com o botão direito no banco de dados criado "db-customers", depois em "New Query" e copie essa query (nome dado ao texto utilizado para fazer operações no banco de dados):

~~~sql
CREATE TABLE Customers (
	CustomerId INT IDENTITY(1,1) PRIMARY KEY,
	Document VARCHAR(18) NOT NULL ,
	CustomerName VARCHAR(100) NOT NULL,
	Mail VARCHAR(20) NOT NULL
);
~~~

Que ficaria basicamente após ser populado (último passo abaixo):

Servidor: db-customers
Banco de dados: Customers

|CustomerId|Document        |CustomerName       |Mail                |
|----------|----------------|-------------------|--------------------|
| 1        | 111.111.111-11 | Nome do cliente 1 | cliente1@gmail.com |
| 2        | 222.222.222-22 | Nome do cliente 2 | cliente2@gmail.com |

Basicamente essa query é composta por:

- Na primeira linha inicia a sintaxe para criar uma tabela chamada Customers e dentro dela (o que está entre abre e fecha parênteses acima) possui os nomes das colunas;
- Na segunda linha é criado um Id (identificador) para cada cliente que for inserido posteriormente, ao criar um cliente não precisa informar qual id ele será, como está IDENTITY(1,1) ele vai fazer o acréscimo automaticamente de 1 a 1. Não é possível passar o id via código quando ele já é incrementado automático;
- Ainda na segunda linha, ele está como PRIMARY KEY, ou seja, é um identificador único (não repete) e toda tabela possui uma e somente uma chave primária. Elas não podem ser nulas;
- E continuando mais uma vez na segunda linha, o CustomerId é do tipo INT, que é um tipo número sem vírgula ou pontos (inteiro) que está entre	-2.147.483.648 to 2.147.483.647, se for necessário um número maior, por exemplo, ou é uma base que insere muitos dados e esse número for pequeno pode-se utilizar BIGINT que possui um tamanho bem maior, consulte [aqui](https://learn.microsoft.com/en-us/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql?view=sql-server-ver16) os tipos de dados possíveis;
- Na terceira linha é tipo é VARCHAR de no máximo 18 caracteres, ou seja, recebe um texto e como possui NOT NULL na frente este campo não pode ser inserido vazio;
- Na quarta linha o limite é de um texto de 20 caracteres, no máximo.

E por último vamos inserir um cliente:

~~~sql
INSERT INTO Customers (Document, CustomerName, Mail) VALUES ('111.111.111-11', 'Nome do cliente 1', 'cliente1@gmail.com');
INSERT INTO Customers (Document, CustomerName, Mail) VALUES ('222.222.222-22', 'Nome do cliente 2', 'cliente2@gmail.com');
~~~

A composição desta parte é feita por:

- INSERT INTO é referência a inserir na tabela, no caso tabela Customer, em seguida entre parênteses é informado quais campos vão ser inseridos, após em VALUES quais valores vão ser inseridos nestes campos;
- Os campos textos precisam ser colocados entre aspas simples '' para delimitar o contexto;

Como foi dito anteriormente, o CustomerId não é passado pois ele é incrementado automaticamente.

Extra:

para consultar se os dados foram inseridos corretamente execute com asterísco para selecionar todas colunas:

~~~sql
SELECT * Customers
~~~

|CustomerId|Document        |CustomerName       |Mail                |
|----------|----------------|-------------------|--------------------|
| 1        | 111.111.111-11 | Nome do cliente 1 | cliente1@gmail.com |
| 2        | 222.222.222-22 | Nome do cliente 2 | cliente2@gmail.com |

Ou especifique as colunas que queira retornar:

~~~sql
SELECT Document, CustomerName, Mail FROM Customers
~~~

|Document        |CustomerName       |Mail                |
|----------------|-------------------|--------------------|
| 111.111.111-11 | Nome do cliente 1 | cliente1@gmail.com |
| 222.222.222-22 | Nome do cliente 2 | cliente2@gmail.com |

### Forma 1


## Como instalar os softwares

Visual Studio 22 - Versão Community + SQL Server Express 2019 LocalDB

Acesse [o link](https://visualstudio.microsoft.com/downloads/) e baixe a versão Community clicando no botão “Free Download”;

![Visual Studio Communitty - Download button](https://github.com/jmrqs/get-started/blob/main/img/visual-studio-community-download-button.jpg)

Abra o instalador (Visual Studio Installer) e clique em “Continue“, após fazer o download, irá aparecer uma tela similar a imagem abaixo, na primeira aba que carrega (Workloads) selecione as seguintes opções:

![Visual Studio Installer](https://github.com/jmrqs/get-started/blob/main/img/visual-studio-installer.jpg)

- ASP.NET and web development
- Azure development
- Data storage and processing

Na segunda aba, certifique-se que a opção abaixo está selecionada (existe uma caixa de pesquisa para facilitar):

- SQL Server Express 2019 LocalDB

Na terceira aba (Language packs), selecione o idioma que irá utilizar (o recomendado é inglês por ser padrão de mercado);

E por último, clique em “Install”;

Após a instalação, vai aparecer uma tela para logar, você pode selecionar “Skip this for now” e fazer isto em outro momento caso precise;

Em seguida, na caixa de seleção “Development settings” selecione Visual C# e clique em “Start Visual Studio”.

![Visual Studio Communitty - Personalize your Visual Studio Experience](https://github.com/jmrqs/get-started/blob/main/img/personalize-your-visual-studio-experience.jpg)

Obs.: Caso tenha esquecido de verificar se o SQL Server Express 2019 LocalDB está instalado, abra o Visual Studio Installer que já está instalado na sua máquina e clique em "Modify" na instalação que foi efetuada.

## Definições

### Visual Studio 22 - Versão Community

[TODO]

### LocalDB Express

[TODO]


