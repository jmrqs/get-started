# Criando um projeto completo do zero

Este t�pico aborda desde a instala��o dos softwares at� rodar na m�quina o projeto do frontend batendo no backend e apresentando os dados consultados no banco de dados.

*Obs.�: Algumas defini��es podem ser encontradas no final da p�gina.*

*Obs.�: Como instalar os softwares tamb�m est� incluso nesta documenta��o.*

## O projeto ser� composto por:

- Frontend - React
- Backend - API em C#
- Banco de dados - SQL Server

## Fluxo:

[TODO]

## Softwares necess�rios:

- Visual Studio 22 - Vers�o Community + SQL Server Express 2019 LocalDB

## - Frontend - React

[TODO]

## - Backend:- API em C#

[TODO]

## - Banco de dados - SQL Server

Esta parte ser� dividida nas seguintes partes:

- Criar o banco de dados
- Criar as tabelas no banco de dados
- Inserir dados no banco de dados

Primeiro vamos criar a base de dados, para isto vamos no Visual Studio instalado e clicar no menu em "View" > "SQL Server Object Explorer", ao clicar em "SQL Server" haver� um servidor de banco de dados correspondente ao LocalDB Express (algo como "(localdb)(...))") e, se expandir a pasta "Databases" n�o haver� nenhum banco de dados l�, vamos criar o primeiro. Para isto vamos clicar com o bot�o direito sobre esta pasta "Databases" e depois em "Add New Database":

![SQL Server Object Explorer - Add New Database](https://github.com/jmrqs/get-started/blob/main/img/sql-server-object-exporer-add-new-database.jpg)

Em "Database Name" que ir� aparecer informe "db-customers" (vamos padronizar este nome por enquanto para usarmos como refer�ncia em todo projeto) e clique em "OK".

Como segundo passo, agora vamos criar a tabela do banco de dados. Para isto clique com o bot�o direito no banco de dados criado "db-customers", depois em "New Query" e copie essa query (nome dado ao texto utilizado para fazer opera��es no banco de dados):

~~~sql
CREATE TABLE Customers (
	CustomerId INT IDENTITY(1,1) PRIMARY KEY,
	Document VARCHAR(18) NOT NULL ,
	CustomerName VARCHAR(100) NOT NULL,
	Mail VARCHAR(20) NOT NULL
);
~~~

Que ficaria basicamente ap�s ser populado (�ltimo passo abaixo):

Servidor: db-customers
Banco de dados: Customers

|CustomerId|Document        |CustomerName       |Mail                |
|----------|----------------|-------------------|--------------------|
| 1        | 111.111.111-11 | Nome do cliente 1 | cliente1@gmail.com |
| 2        | 222.222.222-22 | Nome do cliente 2 | cliente2@gmail.com |

Basicamente essa query � composta por:

- Na primeira linha inicia a sintaxe para criar uma tabela chamada Customers e dentro dela (o que est� entre abre e fecha par�nteses acima) possui os nomes das colunas;
- Na segunda linha � criado um Id (identificador) para cada cliente que for inserido posteriormente, ao criar um cliente n�o precisa informar qual id ele ser�, como est� IDENTITY(1,1) ele vai fazer o acr�scimo automaticamente de 1 a 1. N�o � poss�vel passar o id via c�digo quando ele j� � incrementado autom�tico;
- Ainda na segunda linha, ele est� como PRIMARY KEY, ou seja, � um identificador �nico (n�o repete) e toda tabela possui uma e somente uma chave prim�ria. Elas n�o podem ser nulas;
- E continuando mais uma vez na segunda linha, o CustomerId � do tipo INT, que � um tipo n�mero sem v�rgula ou pontos (inteiro) que est� entre	-2.147.483.648 to 2.147.483.647, se for necess�rio um n�mero maior, por exemplo, ou � uma base que insere muitos dados e esse n�mero for pequeno pode-se utilizar BIGINT que possui um tamanho bem maior, consulte [aqui](https://learn.microsoft.com/en-us/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql?view=sql-server-ver16) os tipos de dados poss�veis;
- Na terceira linha � tipo � VARCHAR de no m�ximo 18 caracteres, ou seja, recebe um texto e como possui NOT NULL na frente este campo n�o pode ser inserido vazio;
- Na quarta linha o limite � de um texto de 20 caracteres, no m�ximo.

E por �ltimo vamos inserir um cliente:

~~~sql
INSERT INTO Customers (Document, CustomerName, Mail) VALUES ('111.111.111-11', 'Nome do cliente 1', 'cliente1@gmail.com');
INSERT INTO Customers (Document, CustomerName, Mail) VALUES ('222.222.222-22', 'Nome do cliente 2', 'cliente2@gmail.com');
~~~

A composi��o desta parte � feita por:

- INSERT INTO � refer�ncia a inserir na tabela, no caso tabela Customer, em seguida entre par�nteses � informado quais campos v�o ser inseridos, ap�s em VALUES quais valores v�o ser inseridos nestes campos;
- Os campos textos precisam ser colocados entre aspas simples '' para delimitar o contexto;

Como foi dito anteriormente, o CustomerId n�o � passado pois ele � incrementado automaticamente.

Extra:

para consultar se os dados foram inseridos corretamente execute com aster�sco para selecionar todas colunas:

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

Visual Studio 22 - Vers�o Community + SQL Server Express 2019 LocalDB

Acesse [o link](https://visualstudio.microsoft.com/downloads/) e baixe a vers�o Community clicando no bot�o �Free Download�;

![Visual Studio Communitty - Download button](https://github.com/jmrqs/get-started/blob/main/img/visual-studio-community-download-button.jpg)

Abra o instalador (Visual Studio Installer) e clique em �Continue�, ap�s fazer o download, ir� aparecer uma tela similar a imagem abaixo, na primeira aba que carrega (Workloads) selecione as seguintes op��es:

![Visual Studio Installer](https://github.com/jmrqs/get-started/blob/main/img/visual-studio-installer.jpg)

- ASP.NET and web development
- Azure development
- Data storage and processing

Na segunda aba, certifique-se que a op��o abaixo est� selecionada (existe uma caixa de pesquisa para facilitar):

- SQL Server Express 2019 LocalDB

Na terceira aba (Language packs), selecione o idioma que ir� utilizar (o recomendado � ingl�s por ser padr�o de mercado);

E por �ltimo, clique em �Install�;

Ap�s a instala��o, vai aparecer uma tela para logar, voc� pode selecionar �Skip this for now� e fazer isto em outro momento caso precise;

Em seguida, na caixa de sele��o �Development settings� selecione Visual C# e clique em �Start Visual Studio�.

![Visual Studio Communitty - Personalize your Visual Studio Experience](https://github.com/jmrqs/get-started/blob/main/img/personalize-your-visual-studio-experience.jpg)

Obs.: Caso tenha esquecido de verificar se o SQL Server Express 2019 LocalDB est� instalado, abra o Visual Studio Installer que j� est� instalado na sua m�quina e clique em "Modify" na instala��o que foi efetuada.

## Defini��es

### Visual Studio 22 - Vers�o Community

[TODO]

### LocalDB Express

[TODO]


