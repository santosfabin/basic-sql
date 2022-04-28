# SQL

- Ajuda
    
    *TODOS OS COMANDOS SQL NORMALMENTE ESTÃO EM MAIUSCULO*
    
    MOUSE2 "Nem Query"
    ou
    seleciona a Databe q quiser, e clique em "New Query"
    
    para fazer apenas o comando aonde quer, basta selecionar as linhas (deixandos elas azulsinhas selecionadas), e apertar f5
    
    CTRL + SHIFT + U == UPPERCASE
    
    CRUD
    
    C - CREATE
    
    R - READ
    
    U - UPDATE
    
    D - DELETE
    

---

- Inicio
    
    CLICK: "New Query"
    
    create database Learning2
    vai criar uma database com o nome Learning2
    f5
    feresh na pasta "Dataases"
    
    drop database Learning2
    vai apagar o database
    
    para restaurar um banco de dados vc tem q:
    MOUSE2 em cima do "Dataases"
    CLICK em Restore Dataase...
    quando abrir uma aba:
    CLICK na opcao em baixo de "Dataase:", ou seja, CLICK em "Device:"
    CLICK nos "..." ao lado direito
    "add"
    

---

- Tipos de dados
    1. Boleanos
        1. De início ele é iniciado como NULO, e pode receber o valor 1, 0 ou NULO
        2. Quando você for iniciar o valor boleano, ele normalmente vai ser do tipo BIT
    2. Caractere
        1. Quando você for iniciar o valor caractere, ele normalmente vai ser do tipo CHAR, VARCHAR ou NVARCHAR
            1. CHAR = ele tem uma quantidade FIXA de caracteres, ocupando todo o espaço desejado (memório)
            2. VARCHAR ou NVARCHAR= ele permite inserir até a quantidade que foi definida, e ele so vai ocupar o espaço preenchido
    3. Números
        - Inteiros
            
            
            | TINYINT | 0 a 255 | 1 byte |
            | --- | --- | --- |
            | SMALLINT | 2^15 (-32.768) a 2^15-1 (32.767) | 2 bytes |
            | INT | 2^31 (-2.147.483.648) a 2^31-1 (2.147.483.647) | 4 bytes |
            | BIGINT | 2^63 (-9.223.372.036.854.775.808) a 2^63-1 (9.223.372.036.854.775.807) | 8 bytes |
        - Valores aproximados
            
            
            | float | - 1,79E+308 a -2,23E-308, 0 e 2,23E-308 a 1,79E+308 | Depende do valor de n |
            | --- | --- | --- |
            | real | - 3,40E + 38 a -1,18E - 38, 0 e 1,18E - 38 a 3,40E + 38 | 4 bytes |
    4. Temporais
        
        
        | DATE | aaaa/mm/dd |
        | --- | --- |
        | DATETIME | aaaa/mm/dd:hh:mm:ss |
        | DATETIME2 | aaaa/mm/dd:hh:mm:sssssss |
        | SMALLDATETIME | ‘1900-01-01:00:00:00’ até ‘2079-06-06:23:59:59’ |
        | TIME | ‘00:00:00.0000000' até ‘23:59:59.9999999’ |
        | DATETIMEODSET | data e hora com fuso horário |

---

- CREATE
    - CREATE DATABESE
        - É usado para criar uma DATABASE
            - como se fosse uma pasta para suas tabelas
        - Então é dentro da DATABESE que ficará todas as informações e tabelas
        - Sintaxe
            
            ```sql
            CREATE DATABASE nome_da_db
            GO
            ```
            
    
    ---
    
    - CREATE TABLE
        - Ela criará a tabela para guardar as informações
        - Sintaxe
            
            ```sql
            CREATE TABLE nome tabela(
            	coluna1 tipo restricaoDaColuna,
            	coluna2 tipo,
            	coluna3 tipo,
            	...
            )
            GO
            ```
            
    
    ---
    
    - Restrições
        
        
        | NOT NULL | não permite valores nulos |
        | --- | --- |
        | UNIQUE | força TODOS os valores em uma coluna serem diferentes |
        | AUTO_INCREMENT | faz todos os próximos valores serem diferentes e em sequência
        (MySQL) |
        | IDENTITY(1,1) | faz todos os próximos valores serem diferentes e em sequência
        (valor inicial, quanto vai aumentar)
        (T-SQL/SQL Server) |
        | PRIMARY KEY | uma junção de NOT NULL e UNIQUE |
        | FOREIGN KEY | identifica unicamente uma linha em outra tabela |
        | CHECK | força uma condição específica em uma coluna |
        | DEFAULT | força um valor padrão quando nenhum valor é passado |
    
    ---
    
    - Exemplo
        
        ```sql
        CREATE DATABASE tbYoutube
        GO
        
        CREATE TABLE tbcanal (
        	canalid INT PRIMARY KEY,
        	nome VARCHAR(150) NOT NULL,
        	contagemInscritos INT DEFAULT 0,
        	dataCriacao DATETIME NOT NULL
        );
        
        CREATE TABLE tbvideo(
        	videoid INT PRIMARY KEY,
        	nome VARCHAR(150) NOT NULL,
        	vizualizacoes INT DEFAULT 0,
        	likes INT DEFAULT 0,
        	deslikes INT DEFAULT 0,
        	duracao INT NOT NULL,
        	canalid INT FOREIGN KEY REFERENCES tbCANAL(canalid)
        );
        
        SELECT *
        FROM tbcanal
        
        SELECT *
        FROM tbvideo
        ```
        

---

- NOT NULL
    - Sintaxe
        
        ```sql
        CREATE TABLE carteiraMotorista(
        	id INT NOT NULL
        	nome VARCHAR(255) NOT NULL,
        	idade INT CHECK (idade >= 18)
        );
        ```
        
    - Então ele é uma restrição para a entrada de dados
        - e caso mande o dado SEM preencher, ele retornará um erro

---

- UNIQUE
    - Ela é uma forma de restrição
        - ou seja, ela restringe a entrada de dados de uma forma que nenhum outro dado seja igual ao outro
    - Sintaxe
        
        ```sql
        CREATE TABLE carteiramotorista(
        	id INT NOT NULL,
        	nome VARCHAR(200),
        	idade INT CHECK (idade >=18),
        	codigocnh INT NOT NULL UNIQUE
        );
        ```
        

---

- IDENTITY(1, 1)
    - Ele criará uma sequência de um valor inicial, e aumentará de tantos em tantos
        - ou seja, ela vai incrementar automaticamente, sem precisar setar um valor para ele
    - Sintaxe
        
        ```sql
        CREATE TABLE pessoa(
            id INT IDENTITY(1,1) PRIMARY KEY,
        );
        ```
        
    - É importante utilizar
        
        ```php
        SET IDENTITY_INSERT nomeTabela ON;
        ```
        
        - Ela ativa a função para atribuir automaticamente a primary key

---

- AUTO_INCREMENT
    - Ele criará uma sequência de um valor inicial 1 e aumentará de 1 em 1
        - ou seja, não é necessário setar um valor para ele
    - Sintaxe
        
        ```sql
        CREATE TABLE pessoa(
            id INT AUTO_INCREMENT PRIMARY KEY,
            NOME varchar(255) NOT NULL,
            IDADE int NOT NULL
        );
        ```
        

---

- PRIMARY KEY
    - PRIMARY KEY = chave primária
        - ou PK
    - Ela é um elemento em uma tabela que é usada para identificar uma única linha da tabela
        - ou seja, na tabela de PRIMARY KEY não haverá itens repetidos
        - e ela é chamada de tabela pai
    - Sintaxe
        
        ```sql
        nome_coluna tipo_de_dados PRIMARY KEY
        ```
        

---

- FOREIGN KEY
    - FOREIGN KEY = chave estrangeira
        - ou FK
    - É uma coluna na tabela que identifica uma única  linha de OUTRA tabela
        - ou seja, ela não contém os dados, mas ela se torna uma referência para os dados
    - Assim ela é uma PRIMARY KEY (chave primária) para outras tabelas
        - e ela é chamada de tabela referenciadora ou de tabela filho
    - Sintaxe
        
        ```sql
        coluna_pk INT FOREIGN KEY REFERENCES tabela(coluna_pk)
        --primeiro é setado o MESMO nome da PRIMARY KEY da outra tabela
        --setado o para INTEIRO
        --é setado que ela é uma FOREIGN KEY (chave estrangeira)
        --mostra que é referenciado ah uma tabela
        --nome da tabela referenciada
        --(nome da coluna da PRIMARY KEY) que será sendo referenciada como FOREIGN KEY
        ```
        

---

- INSERT INTO
    - Sintaxe1
        
        ```sql
        INSERT INTO nomeTabela(coluna1, coluna2)
        VALUES(valor1, valor2)
        VALUES(valor1, valor2)
        VALUES(valor1, valor2)
        ```
        
    - Exemplos
        - Criando
            
            ```sql
            CREATE TABLE aula(
            	id INT PRIMARY KEY,
            	nome VARCHAR(200)
            );
            ```
            
        - Inserindo uma linha de valores
            
            ```sql
            INSERT INTO aula (id,nome)
            VALUES (1, 'aula1')
            SELECT *
            FROM aula
            ```
            
        - Inserindo várias linha de valores
            
            ```sql
            INSERT INTO aula (id, nome)
            VALUES
            (2, 'aula 2'),
            (3, 'aula 3'),
            (4, 'aula 4');
            
            SELECT * FROM aula
            ```
            
    
    ---
    
    - Sintaxe2
        - Inserir uma coluna de uma tabela pra outra
        
        ```sql
        INSERT INTO tabelaA (coluna1)
        SELECT coluna2
        FROM tabelaB
        ```
        
    - Exemplos da Sintaxe2
        - Criando rapidamente
            
            ```sql
            SELECT * INTO tabelanova FROM aula
            
            SELECT * FROM tabelanova
            ```
            
    
    ---
    
    - Exemplo completo
    
    ```sql
    CREATE TABLE exemplo1
    (
    	coluna1 VARCHAR(10) NOT NULL,
    	coluna2 INT DEFAULT 0
    );
    --
    INSERT INTO exemplo1 (coluna1, coluna2)
    VALUES('1', 1)
    --
    SELECT *
    FROM exemplo1
    --
    INSERT INTO exemplo1 (coluna1, coluna2)
    VALUES
    ('2',2),
    ('3',3),
    ('4',4);
    --
    CREATE TABLE exemplo2
    (
    	coluna1 VARCHAR(10) NOT NULL,
    	coluna2 INT DEFAULT 0
    );
    INSERT INTO exemplo2 (coluna1, coluna2)
    VALUES
    ('1',1)
    --
    SELECT *
    FROM exemplo2
    --
    INSERT INTO exemplo2 (coluna1)
    SELECT coluna1
    FROM exemplo1
    
    SELECT *
    FROM exemplo2
    ```
    

---

- UPDATE
    - Sintaxe
        
        ```sql
        UPDATE nomeTabela
        SET coluna1 = valor1
        		coluna2 = valor2
        WHERE condicao
        ```
        
        <aside>
        ❗ é importante o WHERE pois sem ele o comando irá mudar TODO o banco de dados
        
        </aside>
        
    
    ---
    
    - Exemplo
        - Tabela
            
            ```sql
            CREATE TABLE aula(
            	id INT PRIMARY KEY,
            	nome VARCHAR(150) NOT NULL
            );
            
            INSERT INTO aula(id, nome)
            VALUES
            (1,'aula 1'),
            (2,'aula 2'),
            (3,'aula 3'),
            (4,'aula 4');
            
            SELECT * FROM aula
            ```
            
        
        ---
        
        - Execução SEM o WHERE
            
            ```sql
            UPDATE aula
            SET nome = 'teste'
            ```
            
        
        ---
        
        - Execução COM o WHERE
            
            ```sql
            UPDATE aula
            SET NOME = 'mudar'
            WHERE id = 3
            ```
            
            ```sql
            UPDATE aula
            SET nome = 'par'
            WHERE id % 2 = 0
            ```
            

---

- ALTER TABLE
    - Sintaxe
        
        ```sql
        ALTER TABLE nomeTabela
        acao/condicoes
        ```
        
    
    ---
    
    - Exemplos do que se pode fazer
        1. Add, remover ou alterar uma coluna
        2. Setar valores padrões para uma coluna
        3. Add ou remover restrições de colunas
        4. Renomear uma tabela
    
    ---
    
    - Exemplos
        - Tabela
            
            ```sql
            CREATE TABLE youtube
            (
            id INT PRIMARY KEY,
            nome VARCHAR(150) NOT NULL UNIQUE,
            categoria VARCHAR(200) NOT NULL,
            datacriacao DATETIME NOT NULL
            );
            ```
            
        - Adicionado uma tabela
            
            ```sql
            ALTER TABLE youtube
            add ativo bit
            
            SELECT * FROM youtube
            ```
            
        - Alterando uma coluna
            
            ```sql
            ALTER TABLE youtube
            ALTER COLUMN categoria VARCHAR(300) NOT NULL
            ```
            

---

- CHECK CONSTRAINT
    - Sintaxe
        
        ```sql
        CREATE TABLE carteiraMotorista(
        	id INT NOT NULL
        	nome VARCHAR(255) NOT NULL,
        	idade INT CHECK ( idade >= 18 )
        );
        ```
        
    - Então ele é uma restrição para a entrada de dados
        - e caso mande o dado para preencher, ele retornará um erro

---

- DELETE
    
    <aside>
    ❗ **É importante também colocar uma condição para o DELETE**
    
    - caso contrário ele irá apagar $***TUDO***$ que está na tabela
    </aside>
    
    - Sintaxe
        
        ```sql
        DELETE FROM nomeTabela
        WHERE condicao
        ```
        
    
    ---
    
    - Exemplo
        
        ```sql
        DELETE FROM aula
        WHERE nome <> 'par'
        
        SELECT * FROM AULA
        ```
        
    
    ---
    
    - Para renomear no SQL-SERVER é um comando específico
        - EXEC
            - Sintaxe
                
                ```sql
                EXEC sp_RENAME 'nomeTabela.nomeColuna', 'nomeColunaNova', 'tipo'
                ```
                
            - Exemplos
                - Alterando o nome de uma coluna
                    
                    ```sql
                    EXEC SP_RENAME 'youtube.nome', 'nomeCanal', 'COLUMN'
                    ```
                    
                - Alterando o nome da tabela
                    
                    ```sql
                    EXEC SP_RENAME 'youtube', 'youtube2'
                    ```
                    

---

- DROP
    - Sintaxe
        
        ```sql
        DROP TIPO nomeTabela
        ```
        
    
    ---
    
    - Excluir TABLE
        - ela provavelmente só será excluída se não tiver sendo referenciada
        
        ```sql
        DROP TABLE nomeTabela
        ```
        
    
    ---
    
    - Excluir DATABASE
        - é necessário que DATABASE não esteja em uso
        
        ```sql
        DROP DATABASE nomeDataBase
        ```
        
    
    ---
    
    - Excluir o conteúdo dentro da tabela
        - TRUNCATE
            
            ```sql
            TRUNCATE TABLE aula
            ```
            
    
    ---
    
    - Exemplo geral
        
        ```sql
        CREATE TABLE apagar1
        (
        	id INT PRIMARY KEY,
        	nome VARCHAR(10)
        );
        
        CREATE TABLE apagar2
        (
        	id INT PRIMARY KEY,
        	nome VARCHAR(10)
        );
        DROP TABLE apagar1
        DROP TABLE apagar2
        
        SELECT * FROM apagar1
        SELECT * FROM apagar2
        ```
        

---

- VIEWS
    - Sintaxe
        
        ```sql
        CREATE VIEW [pessoas simplificado] AS 
        SELECT firstname, middlename, lastname
        FROM person.person
        WHERE title = 'ms.'
        ```
        
    - Ela criará uma tabela com as condições requeridas, simplificando sua busca

---

- Select/FROM
    - SELECT faz a seleção das colunas
    - FROM seleciona a DATABASE
    
    VAI SELECIONAR TUDO
    
    ```sql
    SELECT *
    ```
    
    VAI SELECIONAR APENAS na coluna
    
    ```sql
    SELECT coluna1
    ```
    
    VAI SELECIONAR APENAS na coluna1 e coluna2
    
    ```sql
    SELECT coluna,coluna2
    ```
    
    VAI PEGAR DA TABELA person.Person
    
    ```sql
    SELECT DISTINCT coluna1,coluna2
    FROM person.Person
    ```
    
    ---
    
    1. EXEMPLOS:
        
        ```sql
        SELECT firstname, lastname
        FROM person.person
        ```
        
        ```sql
        SELECT DISTINCT firstname
        FROM person.Person
        ```
        

---

- WHERE
    
    Trabalha com operadores de comparação
    
    | =
     | igual |
    | --- | --- |
    | <
     | menor |
    | >
     | maior |
    | >= | maior ou igual |
    | <= | menor ou igual |
    | <> | diferente de |
    | AND | operador logico E |
    | OR | operador logico OU |
    
    ---
    
    EXEMPLOS:
    
    ```sql
    SELECT *
    FROM person.Person
    WHERE lastname = 'miller'
    ```
    
    ```sql
    SELECT *
    FROM person.Person
    WHERE lastname = 'miLler' AND firstname = 'anna'
    ```
    
    ```sql
    SELECT *
    FROM PRODUCTION.PRODUCT
    WHERE ListPrice > 1500 and ListPrice < 5000
    ```
    
    ```sql
    SELECT *
    FROM PRODUCTION.PRODUCT
    WHERE color <> 'red'
    ```
    
    ---
    
    EXERCICIOS:
    
    ```sql
    SELECT *
    FROM PRODUCTION.PRODUCT
    WHERE weight > 500 and weight <= 700
    ```
    
    ```sql
    SELECT *
    FROM HumanResources.Employee
    WHERE MaritalStatus = 'm' and SalariedFlag = 1
    ```
    
    ```sql
    SELECT *
    FROM Person.Person
    WHERE FirstName = 'peter' and LastName = 'krebs'
    ```
    
    ```sql
    SELECT EmailAddress
    FROM person.EmailAddress
    WHERE BusinessEntityID = 26
    ```
    

---

- IN
    
    É usado junto com o WHERE
    
    - verifica se um valor corresponde com qualquer valor passado na lista de valores
    - ele é como o between, porem so nos valores escritos, o between é todos os valores dentro dos escolhidos
    - ele tbm é mais rápido
    
    ---
    
    EXEMPLOS:
    
    - valor IN(valor1,valor2)
    color IN('blue','black')
    valor IN (SELECT valor FROM NomeDaTabela)
        
        ```sql
        SELECT *
        FROM Person.Person
        WHERE BusinessEntityID IN(2,7,13)
        ```
        
        ```sql
        SELECT *
        FROM Person.Person
        WHERE BusinessEntityID NOT IN(2,7,13)
        ```
        
    

---

- COUNT
    
    Trabalha com quantidade de linha
    
    EXEMPLOS:
    
    ```sql
    SELECT COUNT(*)
    FROM tabela
    ```
    
    ```sql
    SELECT COUNT(DISTINCT coluna1)
    FROM tabela
    ```
    
    ```sql
    SELECT COUNT(title)
    FROM Person.Person
    ```
    
    ```sql
    SELECT COUNT(DISTINCT title)
    FROM Person.Person
    ```
    
    ---
    
    EXERCICIOS:
    
    - 1
        
        ```sql
        SELECT COUNT(name)
        FROM Production.Product
        ```
        
    - 2
        
        ```sql
        SELECT COUNT(size)
        FROM Production.Product
        ```
        
    - 3
        
        ```sql
        SELECT COUNT(DISTINCT size)
        FROM Production.Product
        ```
        
    

---

- TOP
    
    TOP ele vai limitar a quantidade de dados
    
    EXEMPLOS:
    
    ```sql
    SELECT TOP 10 *
    FROM tabela
    ```
    
    ```sql
    SELECT TOP 10 *
    FROM production.product
    WHERE color = 'black'
    ```
    

---

- ORDER BY
    
    Vai ordenar por ordem crescente ou decrescente
    
    EXEMPLOS:
    
    ```sql
    SELECT coluna1, coluna2
    FROM tabela
    ORDER BY coluna1 asc
    ```
    
    ```sql
    SELECT coluna1, coluna2
    FROM tabela
    ORDER BY coluna1 desc
    ```
    
    ```sql
    SELECT *
    FROM Person.Person
    ORDER BY FirstName asc
    ```
    
    ```sql
    SELECT *
    FROM Person.Person
    ORDER BY FirstName desc
    ```
    
    F
    
    ```sql
    SELECT *
    FROM Person.Person
    ORDER BY FirstName asc, lastname desc
    ```
    
    ---
    
    EXERCICIOS:
    
    ```sql
    SELECT TOP 10 Productid
    FROM Production.Product
    ORDER BY listprice desc
    ```
    
    ```sql
    SELECT name, ProductNumber
    FROM Production.Product
    WHERE ProductID >= 1 and ProductID <= 4
    ```
    
    ```sql
    
    SELECT TOP 4 name, Productnumber
    FROM Production.Product
    ORDER BY ProductID asc
    ```
    

---

- BETWEEN
    
    É usado para encontrar valor entre um valor mínimo e máximo
    
    EXEMPLOS:
    
    1. valor BETWEEN mínimo AND máximo
        
        ```sql
        SELECT *
        FROM Production.Product
        WHERE ListPrice BETWEEN 1000 AND 1500
        ```
        
        ```sql
        SELECT *
        FROM Production.Product
        WHERE ListPrice NOT BETWEEN 1000 AND 1500
        ```
        
        ```sql
        SELECT *
        FROM HumanResources.Employee
        WHERE HireDate BETWEEN '2009/01/01' and '2010/01/01'
        ```
        

---

- LIKE
    
    LIKE	usado para encontrar dados q vc sabe alguma coisa do nome
    
    | % | == |  não importa oq vem depois, e é pra VARIAS letras |
    | --- | --- | --- |
    | _  | == | é apenas para UMA letra qualquer |
    
    EXEMPLOS:
    
    ```sql
    SELECT *
    FROM Person.Person
    WHERE FirstName LIKE 'ovi%'
    ```
    
    ```sql
    SELECT *
    FROM Person.Person
    WHERE FirstName LIKE '%to'
    ```
    
    ```sql
    SELECT *
    FROM Person.Person
    WHERE FirstName LIKE '%essa%'
    ```
    
    ```sql
    SELECT *
    FROM Person.Person
    WHERE FirstName LIKE '%ro_'
    ```
    
    ```sql
    SELECT *
    FROM Person.Person
    WHERE FirstName LIKE '_ro%'
    ```
    
    ```sql
    SELECT COUNT (FirstName)
    FROM Person.Person
    WHERE FirstName LIKE '%to'
    ```
    
    ```sql
    SELECT COUNT (DISTINCT FirstName)
    FROM Person.Person
    WHERE FirstName LIKE '%to'
    ```
    

---

- Operações matemáticas
    - ROUND
        - Ele arredonda o valor
        - Sintaxe
            - ROUND(tabela, coluna, precisão decimal)
        - Utilização
            - ROUND(LineTotal, 2, 2)
        - Exemplo:
            
            ```jsx
            SELECT ROUND(linetotal, 2), ROUND(linetotal, 2, 2), linetotal
            FROM Sales.SalesOrderDetail
            ```
            
    
    ---
    
    - SQRT
        - == Raiz quadrada
        - Exemplo:
            
            ```jsx
            SELECT SQRT(linetotal)
            FROM Sales.SalesOrderDetail
            ```
            
    
    ---
    
    - MIN/MAX/SUM/AVG
        
        São funções de agregação, basicamente agregam ou combinam dados de uma tabela em 1 resultado so
        
        | AS |
        | --- |
        | renomeia a tabela final para nome |
        
        | SUM |
        | --- |
        | soma de tudo naquela coluna |
        
        | MIN |
        | --- |
        | o valor MINIMO naquela coluna |
        
        | MAX |
        | --- |
        | o valor MAXIMO naquela coluna |
        
        | AVG |
        | --- |
        | a MEDIA dos valores naquela coluna |
        
        ---
        
        EXEMPLOS:
        
        ```sql
        SELECT TOP 10 SUM(linetotal) AS "SOMA"
        FROM Sales.SalesOrderDetail
        ```
        
        ```sql
        SELECT MIN(linetotal) AS "MINIMO"
        FROM sales.SalesOrderDetail
        ```
        
        ```sql
        SELECT MAX(linetotal) AS "MAXIMO"
        FROM sales.SalesOrderDetail
        ```
        
        ```sql
        SELECT AVG(linetotal) AS "MEDIA"
        FROM sales.SalesOrderDetail
        ```
        
    
    ---
    
    - Resumo
        
        
        | AVG() |
        | --- |
        | = Retorna o valor médio de uma coluna específica |
        
        | BINARY_CHECKSUM() |
        | --- |
        | = O valor do BINARY_CHECKSUM computado sobre uma linha ou uma tabela ou sobre uma lista de expressões. BINARY CHECKSUM é usada para detectar alterações em uma linha ou uma tabela. |
        
        | CHECKSUM() |
        | --- |
        | = O valor de CHECKSUM computado sobre uma linha ou uma tabela, ou sobre uma lista de expressões. CHECKSUM é usada para construir índices de hash. |
        
        | CHECKSUM_AGG() |
        | --- |
        | = O valor de CHECKSUM de um grupo. Valores nulos são ignorados. |
        
        | COUNT() |
        | --- |
        | = Retorna o número de linhas |
        
        | COUNT_BIG() |
        | --- |
        | = igual ao COUNT mas o COUNT_BIG sempre retorna um tipo de dados bigint. |
        
        | COUNT() |
        | --- |
        | = Retorna o número de linhas |
        
        | STDEV() |
        | --- |
        | = Desvio padrão de todos os valores |
        
        | STDEVP() |
        | --- |
        | = Desvio padrão da população |
        
        | VAR() |
        | --- |
        | = Variância estatistica de todos os valores |
        
        | VARP() |
        | --- |
        | = Variância estatística de todos os valores da população |

---

- GROUP BY
    
    vai dividir o resultado da pesquisa em grupos, para cada grupo vc pode aplicar uma função de agregação, por exemplo: calcular a soma dos itens; contar o numero de itens daquele grupo
    
    EXEMPLOS:
    
    ```sql
    SELECT coluna1,funcaoAgregacao(coluna2)
    FROM nameTabela
    GROUP BY coluna1
    ```
    
    - Ele agrupa todos os iguais
    - Ele soma todos os iguais e deixa na linha a frente
        
        ```sql
        SELECT TOP 10 Productid, COUNT(productid) AS "quantidade"
        FROM Sales.SalesOrderDetail
        GROUP BY ProductID
        ORDER BY quantidade desc
        ```
        
        ```sql
        SELECT firstname, COUNT(FirstName) AS "QUANTIDADE"
        FROM Person.Person
        WHERE FirstName LIKE 'f%'
        GROUP BY FirstName
        ORDER BY FirstName
        ```
        
        ```sql
        SELECT color,AVG(listprice)
        FROM Production.Product
        GROUP BY color
        ```
        
    
    ---
    
    EXERCICIOS:
    
    ```sql
    SELECT MiddleName, COUNT(middlename) AS "QUANTIDADE"
    FROM Person.Person
    GROUP BY MiddleName
    ```
    
    ```sql
    SELECT productid, AVG(orderqty)
    FROM sales.SalesOrderDetail
    GROUP BY ProductID
    ```
    
    ```sql
    SELECT TOP 10 ProductID, SUM(linetotal) AS "TOTAL"
    FROM sales.SalesOrderDetail
    GROUP BY ProductID
    ORDER BY TOTAL desc
    ```
    
    ```sql
    SELECT ProductID, COUNT(productid) AS "CONTAGEM", AVG(OrderQty) AS "MEDIA"
    FROM Production.WorkOrder
    GROUP BY ProductID
    ```
    

---

- HAVING
    
    É usada em junção com o GROUP BY para filtrar resultados de um agrupamento
    
    - ele é basicamente um WHERE para o GROUP BY
    - WHERE É USADO ANTES DO DOS DADOS SEREM AGRUPADOS
        
        ```sql
        SELEC coluna1, funcaoAgregacao(coluna2)
        FROM nomeTabela
        GROUP BY coluna1
        HAVING condicao
        ```
        
    
    ---
    
    EXEMPLOS:
    
    ```sql
    SELECT firstname, COUNT(firstname) AS "QUANTIDADE"
    FROM Person.Person
    GROUP BY FirstName
    HAVING COUNT(firstname) > 10
    ```
    
    ```sql
    SELECT ProductID, SUM(LineTotal) AS "TOTAL"
    FROM sales.SalesOrderDetail
    GROUP BY ProductID
    HAVING SUM(linetotal) BETWEEN 162000 AND 500000
    ```
    
    ```sql
    SELECT FirstName, COUNT(firstname)
    FROM Person.person
    WHERE Title LIKE 'mr.'
    GROUP BY FirstName
    HAVING COUNT(firstname) > 10
    ```
    
    ---
    
    EXERCICIOS:
    
    ```sql
    SELECT StateProvinceID, COUNT(stateprovinceid) AS "QUANTIDADE"
    FROM person.Address
    GROUP BY StateProvinceID
    HAVING COUNT(stateprovinceid) > 1000
    ```
    
    ```sql
    SELECT ProductID,AVG(linetotal)
    FROM sales.SalesOrderDetail
    GROUP BY ProductID
    HAVING AVG(linetotal) < 1000000
    ```
    

---

- AS
    - AS renomeia a coluna
    - É possível fazer a nomenclatura assim
        
        ```sql
        FROM Person.Person AS p
        ```
        
        ```sql
        FROM Person.Person p
        ```
        
    
    EXEMPLOS:
    
    ```sql
    SELECT TOP 10 ListPrice AS "PREÇO do produto"
    FROM Production.Product
    ```
    
    ```sql
    SELECT TOP 10 AVG(listprice) AS "PREÇO MEDIO"
    FROM Production.Product
    ```
    
    ---
    
    EXERCICIOS:
    
    ```sql
    SELECT FirstName AS "PRIMEIRO NOME", LastName AS "SOBRE NOME"
    FROM person.Person
    ```
    
    ```sql
    SELECT ProductNumber AS "NUMERO DO PRODUTO"
    FROM Production.Product
    ```
    
    ```sql
    SELECT UnitPrice AS "PREÇO UNITARIO"
    FROM sales.SalesOrderDetail
    ```
    

---

- JOINS
    
    ![Untitled](SQL%2068edc743329443aab617800a1c2a61f5/Untitled.png)
    
    - INNER JOIN
        - Retorna APENAS os resultados que CORRESPONDEM tanto na tabela A quanto na tabela B
            - É a intersecção entre as duas tabelas
                
                ![Untitled](SQL%2068edc743329443aab617800a1c2a61f5/Untitled%201.png)
                
            
            > EXEMPLO:
            > 
            > - TABELAS
            > 
            > | Tabela | A | Tabela | B |
            > | --- | --- | --- | --- |
            > | id | nome | id | nome |
            > | 1 | Pedro | 1 | Jonas |
            > | 2 | Leandro | 2 | Pedro |
            > | 3 | Mario | 3 | Mario |
            > 
            > ---
            > 
            > - ENTRADA
            > 
            > ```sql
            > SELECT * 
            > FROM tabelaA
            > INNER JOIN tabelaB ON tabelaA.nome
            > ```
            > 
            > ---
            > 
            > - SAÍDA
            > 
            > | id | nome | id | nome |
            > | --- | --- | --- | --- |
            > | 1 | Pedro | 2 | Pedro |
            > | 3 | Mario | 3 | Mario |
        
        ---
        
        - Exemplo de duas colunas
            1. Repare que ele mostrará separadamente
                
                ```sql
                SELECT TOP 10 *
                FROM PERSON.PERSON
                
                SELECT TOP 10 *
                FROM person.EmailAddress
                ```
                
        
        ---
        
        - Exemplos
            - Juntando colunas específicas da tabela
                
                ```sql
                SELECT p.businessEntityid, p.FirstName, p.LastName, pe.EmailAddress
                FROM Person.Person AS p
                INNER JOIN person.EmailAddress PE on p.BusinessEntityID = pe.BusinessEntityID
                ```
                
                ```sql
                SELECT pr.ListPrice, pr.Name, pc.name
                FROM Production.Product pr
                INNER JOIN Production.ProductSubcategory pc on pc.ProductSubcategoryID = pr.ProductSubcategoryID
                ```
                
            - Juntando tudo das tabelas
                - ele junta todas as colunas q são iguais
                
                ```sql
                SELECT TOP 10 *
                FROM Person.BusinessEntityAddress ba
                INNER JOIN Person.Address pa ON pa.AddressID = ba.AddressID
                ```
                
        
        ---
        
        - Exercício
            
            ```sql
            SELECT pa.businessentityid, [pp.Name](http://pp.name/), pa.phonenumbertypeid, pa.phonenumber
            FROM person.PhoneNumberType pp
            INNER JOIN person.PersonPhone pa ON pp.PhoneNumberTypeID = pa.PhoneNumberTypeID
            ```
            
            ```sql
            SELECT pa.AddressID, pa.City, ps.StateProvinceID, ps.Name
            FROM person.StateProvince ps
            INNER JOIN person.Address pa ON pa.StateProvinceID = ps.StateProvinceID
            ```
            
            ```sql
            SELECT *
            FROM person.Person pp
            INNER JOIN sales.PersonCreditCard pc
            ON pp.BusinessEntityID = pc.BusinessEntityID
            -- 19118 itens
            ```
            
    
    ---
    
    - FULL OUTER JOIN
        - Vai retornar um conjunto de todos os registros correspondentes as duas tabelas (tabelaA e tabelaB) quando são iguais
        - Caso não houver valores IGUAIS ele irá preencher com null
        - É a união entre as duas tabelas
            
            ![Untitled](SQL%2068edc743329443aab617800a1c2a61f5/Untitled%202.png)
            
            > EXEMPLO:
            > 
            > - TABELAS
            > 
            > | Tabela | A | Tabela | B |
            > | --- | --- | --- | --- |
            > | id | nome | id | nome |
            > | 1 | Pedro | 1 | Jonas |
            > | 2 | Leandro | 2 | Pedro |
            > | 3 | Mario | 3 | Mario |
            > 
            > ---
            > 
            > - ENTRADA
            > 
            > ```sql
            > SELECT *
            > FROM tabelaA
            > FULL OUTER JOIN tabelaA ON TabelaA.nome = tabelaB.nome
            > ```
            > 
            > ---
            > 
            > - SAÍDA
            > 
            > | id | nome | id | nome |
            > | --- | --- | --- | --- |
            > | 1 | Pedro | 2 | Pedro |
            > | 2 | Leandro | NULL | NULL |
            > | 3 | Mario | 3 | Mario |
            > | NULL | NULL | 1 | Jonas |
            
    
    ---
    
    - LEFT OUTER JOIN
        - OU também LEFT JOIN
        - Retorna um conjunto de todos os registros da **tabelaA**
        - Quando os registros da tabelaB forem correspondentes a tabelaA, ele trará esses valores
        - Quando não houver registros correspondentes ele preencherá com null
        - Isso equivale a tabelaA \ tabelaB ou tabelaA - tabelaB
            
            ![Untitled](SQL%2068edc743329443aab617800a1c2a61f5/Untitled%203.png)
            
            > EXEMPLO:
            > 
            > - TABELAS
            > 
            > | Tabela | A | Tabela | B |
            > | --- | --- | --- | --- |
            > | id | nome | id | nome |
            > | 1 | Pedro | 1 | Jonas |
            > | 2 | Leandro | 2 | Pedro |
            > | 3 | Mario | 3 | Mario |
            > 
            > ---
            > 
            > - ENTRADA
            > 
            > ```sql
            > SELECT *
            > FROM tabelaA
            > LEFT JOIN tabelaA ON TabelaA.nome = tabelaB.nome
            > ```
            > 
            > ---
            > 
            > - SAÍDA
            > 
            > | id | nome | id | nome |
            > | --- | --- | --- | --- |
            > | 1 | Pedro | 2 | Pedro |
            > | 2 | Leandro | NULL | NULL |
            > | 3 | Mario | 3 | Mario |
        
        ---
        
        - Exemplos
            
            ```sql
            SELECT *
            FROM person.Person pp
            LEFT JOIN sales.PersonCreditCard pc
            ON pp.BusinessEntityID = pc.BusinessEntityID
            -- 19972 itens
            WHERE pc.BusinessEntityID IS NULL     -- F
            ```
            
            - — F
            
            ```sql
            SELECT pp.FirstName, pp.MiddleName, pp.LastName, pe.EmailAddress
            FROM Person.Person pp
            LEFT JOIN Person.EmailAddress pe
            ON pp.BusinessEntityID = pe.BusinessEntityID
            ```
            
            ```sql
            SELECT pe.EmailAddress, pw.PasswordHash, pw.PasswordSalt
            FROM Person.EmailAddress pe
            LEFT JOIN Person.Password pw
            ON pw.BusinessEntityID = pe.BusinessEntityID
            ```
            
    
    ---
    
    - RIGHT OUTER JOIN
        - OU também RIGHT JOIN
        - Retorna um conjunto de todos os registros da **tabelaB**
        - Quando os registros da tabelaA forem correspondentes a tabelaB, ele trará esses valores
        - Quando não houver registros correspondentes ele preencherá com null
        - Isso equivale a tabelaB \ tabelaA ou tabelaB - tabelaA
            
            ![Untitled](SQL%2068edc743329443aab617800a1c2a61f5/Untitled%204.png)
            
            > EXEMPLO:
            > 
            > - TABELAS
            > 
            > | Tabela | A | Tabela | B |
            > | --- | --- | --- | --- |
            > | id | nome | id | nome |
            > | 1 | Pedro | 1 | Jonas |
            > | 2 | Leandro | 2 | Pedro |
            > | 3 | Mario | 3 | Mario |
            > 
            > ---
            > 
            > - ENTRADA
            > 
            > ```sql
            > SELECT *
            > FROM tabelaA
            > RIGHT JOIN tabelaB ON TabelaA.nome = tabelaB.nome
            > ```
            > 
            > ---
            > 
            > - SAÍDA
            > 
            > | id | nome | id | nome |
            > | --- | --- | --- | --- |
            > | NULL | NULL | 1 | Jonas |
            > | 1 | Pedro | 2 | Pedro |
            > | 3 | Mario | 3 | Mario |
    
    ---
    
    - SELF JOIN
        - Sintaxe
            
            ```sql
            SELECT nome_coluna
            FROM tabelaA, tabelaB
            WHERE condicao
            ```
            
        - Exemplo
            
            ```sql
            SELECT a.ContactName, a.Region, b.ContactName, b.Region
            FROM Customers a, Customers b
            WHERE a.Region = b.region
            ```
            
        - Exemplo
            
            ```sql
            SELECT a.firstname, a.hiredate, b.firstname, b.hiredate
            FROM Employees a, Employees b
            WHERE DATEPART(year, a.hiredate) = DATEPART(year, b.hiredate)
            ```
            
        - Exemplo
            
            ```sql
            SELECT a.ProductID, a.Discount, b.ProductID, b.Discount
            FROM [Order Details] a, [Order Details] b
            WHERE a.Discount = b.Discount
            ```
            

---

- UNION
    - Esse operador junta dois ou mais resultados de uma operação de SELECT
    - Ele REMORE as DUPLICATAS
        - Com exceção da operação UNION ALL
            - ele vai deixar as duplicatas
    - Ele não junta por algum tipo de ordem, é pela forma de otimização própria dele
    
    ---
    
    Exemplos:
    
    ```sql
    SELECT Productid, Name, ProductNumber
    FROM Production.Product
    WHERE name like'%Chain%'
    UNION
    SELECT  Productid, Name, ProductNumber
    FROM Production.Product
    WHERE name like '%Decal%'
    ORDER BY name
    ```
    
    ```sql
    SELECT firstname, title, MiddleName
    FROM Person.Person
    WHERE Title = 'mr.'
    UNION
    SELECT firstname, title, MiddleName
    FROM Person.Person
    WHERE MiddleName = 'a'
    ```
    
    ```sql
    SELECT pp.FirstName,  pp.Title
    FROM Person.Person pp
    UNION
    SELECT pp.FirstName, pp.Title
    FROM Person.Person pp
    ```
    

---

- DATEPART
    - Introdução (não obrigatório)
        
        > (não obrigatorio) — início
        > 
        > - É uma expressão que retorna um tipo INT
        > - Uma expressão que é resolvida para um dos seguintes tipos de dados:
        >     - date
        >     - datetime
        >     - datetimeoffset
        >     - datetime2
        >     - smalldatetime
        >     - time
        > 
        > ---
        > 
        > - Sintaxe
        >     
        >     ```sql
        >     DATEPART ( datepart , date )
        >     ```
        >     
        > 
        > ---
        > 
        > - Argumentos
        >     
        >     
        >     | datepart | Abreviações |
        >     | --- | --- |
        >     | year | yy, yyyy |
        >     | quarter | qq, q |
        >     | month | mm, m |
        >     | dayofyear | dy, y |
        >     | day | dd, d |
        >     | week | wk, ww |
        >     | weekday | dw |
        >     | hour | hh |
        >     | minute | mi, n |
        >     | second | ss, s |
        >     | millisecond | ms |
        >     | microsecond | mcs |
        >     | nanosecond | ns |
        >     | tzoffset | tz |
        >     | iso_week | isowk, isoww |
        > 
        > ---
        > 
        > - Valor retornado
        >     
        >     
        >     | datepart | Valor retornado |
        >     | --- | --- |
        >     | year, yyyy, yy | 2007 |
        >     | quarter, qq, q | 4 |
        >     | month, mm, m | 10 |
        >     | dayofyear, dy, y | 303 |
        >     | day, dd, d | 30 |
        >     | week, wk, ww | 44 |
        >     | weekday, dw | 3 |
        >     | hour, hh | 12 |
        >     | minute, n | 15 |
        >     | second, ss, s | 32 |
        >     | millisecond, ms | 123 |
        >     | microsecond, mcs | 123456 |
        >     | nanosecond, ns | 123456700 |
        >     | tzoffset, tz | 310 |
        >     | iso_week, isowk, isoww | 44 |
        > 
        > ---
        > 
        > - Argumentos week e weekday de datepart
        >     
        >     
        >     | SET DATEFIRST argumento | week retornado | weekday retornado |
        >     | --- | --- | --- |
        >     | 1 | 16 | 6 |
        >     | 2 | 17 | 5 |
        >     | 3 | 17 | 4 |
        >     | 4 | 17 | 3 |
        >     | 5 | 17 | 2 |
        >     | 6 | 17 | 1 |
        >     | 7 | 16 | 7 |
        > 
        > ---
        > 
        > - Argumentos year, month e day de datepart
        >     - Os valores retornados para DATEPART (**year**, *date*), DATEPART (**month**, *date*) e DATEPART (**day**, *date*) são iguais aos retornados pelas funções [YEAR](https://docs.microsoft.com/pt-br/sql/t-sql/functions/year-transact-sql?view=sql-server-ver15), [MONTH](https://docs.microsoft.com/pt-br/sql/t-sql/functions/month-transact-sql?view=sql-server-ver15) e [DAY](https://docs.microsoft.com/pt-br/sql/t-sql/functions/day-transact-sql?view=sql-server-ver15), respectivamente.
        >     
        >     ---
        >     
        >     - iso_week datepart
        >         
        >         
        >         | Primeiro dia da semana | Primeira semana do ano contém | Semanas atribuídas duas vezes | Usado por/em |
        >         | --- | --- | --- | --- |
        >         | Sunday | 1º de janeiro,
        >         Primeiro sábado,
        >         1 a 7 dias do ano | Sim | Estados Unidos |
        >         | Monday | 1º de janeiro,
        >         Primeiro domingo,
        >         1 a 7 dias do ano | Sim | A maior parte da Europa e do Reino Unido |
        >         | Monday | 4 de janeiro,
        >         Primeira quinta-feira,
        >         4 a 7 dias do ano | Não | ISO 8601, Noruega e Suécia |
        >         | Monday | 7 de janeiro,
        >         Primeira segunda-feira,
        >         7 dias do ano | Não |  |
        >         | Quarta-feira | 1º de janeiro,
        >         Primeira terça-feira,
        >         1 a 7 dias do ano | Sim |  |
        >         | Sábado | 1º de janeiro,
        >         Primeira sexta-feira,
        >         1 a 7 dias do ano | Sim |  |
        >         | 7 | 16 | 7 |  |
        >     
        >     ---
        >     
        >     - tzoffset
        >         - `DATEPART` retorna o valor **tzoffset** (**tz**) como o número de minutos (com sinal). Esta instrução retorna uma diferença de fuso horário de 310 minutos:
        >         
        >         ```sql
        >         SELECT DATEPART (tzoffset, '2007-05-10 00:00:01.1234567 +05:10');
        >         ```
        >         
        >         - `DATEPART` renderiza o valor de tzoffset da seguinte maneira:
        >             - Para datetimeoffset e datetime2 e, tzoffset retorna a diferença de
        >             tempo em minutos, em que a diferença para datetime2 é sempre de 0
        >             minuto.
        >             - Para tipos de dados que podem ser convertidos implicitamente em **datetimeoffset** ou **datetime2**, `DATEPART` retorna a diferença de tempo em minutos. Exceção: outros tipos de dados de data/hora.
        >             - Parâmetros de todos os outros tipos resultam em erro.
        > 
        > ---
        > 
        > - **Argumento smalldatetime de date**
        >     - Se o tipo de dados do argumento *date* não tiver a *datepart* especificada, `DATEPART` retornará o padrão para essa *datepart* apenas quando um literal for especificado para *date*.
        >     - Por exemplo, o ano-mês-dia padrão para qualquer tipo de dados de **date** é 1900-01-01. Esta instrução tem argumentos de parte de data para *datepart*, um argumento de hora para *date* e ela retorna `1900, 1, 1, 1, 2`.
        >         
        >         ```sql
        >         SELECT DATEPART(year, '12:10:30.123')  
        >             ,DATEPART(month, '12:10:30.123')  
        >             ,DATEPART(day, '12:10:30.123')  
        >             ,DATEPART(dayofyear, '12:10:30.123')  
        >             ,DATEPART(weekday, '12:10:30.123');
        >         ```
        >         
        >     - Se *date* é especificada como uma variável ou coluna de tabela e o tipo de dados dessa variável ou coluna não tem a *datepart* especificada, `DATEPART` retorna o erro 9810. Neste exemplo, a variável *@t* tem um tipo de dados **time**. O exemplo falha porque o ano da parte de data é inválido para o tipo de dados **time**:
        >         
        >         ```sql
        >         DECLARE @t time = '12:10:30.123';
        >         SELECT DATEPART(year, @t);
        >         ```
        >         
        > - Frações de segundo
        >     - Estas instruções mostram que `DATEPART` retorna frações de segundos:
        >         
        >         ```sql
        >         SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
        >         SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
        >         SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700
        >         ```
        >         
        > 
        > (não obrigatorio) —fim
        > 
    - Conteúdo
        
        > Dia
        > 
        > 
        > ```sql
        > SELECT SalesOrderID, DATEPART(day, orderdate) Mes
        > FROM Sales.SalesOrderHeader
        > ```
        > 
        
        > Mês
        > 
        > 
        > ```sql
        > SELECT SalesOrderID, DATEPART(month, orderdate) Mes
        > FROM Sales.SalesOrderHeader
        > ```
        > 
        
        > Ano
        > 
        > 
        > ```sql
        > SELECT SalesOrderID, DATEPART(year, orderdate) Mes
        > FROM Sales.SalesOrderHeader
        > ```
        > 
        
        ---
        
        - Exemplos completos:
            
            ```sql
            SELECT AVG(totaldue) Media, DATEPART(DAY, orderdate) Dia
            FROM Sales.SalesOrderHeader
            GROUP BY DATEPART(DAY, orderdate)
            ORDER BY dia
            ```
            
            ```sql
            SELECT AVG(totaldue) Media, DATEPART(MONTH, orderdate) Mes
            FROM Sales.SalesOrderHeader
            GROUP BY DATEPART(MONTH, orderdate)
            ORDER BY mes
            ```
            
            ```sql
            SELECT AVG(totaldue) Media, DATEPART(YEAR, orderdate) Ano
            FROM Sales.SalesOrderHeader
            GROUP BY DATEPART(YEAR, orderdate)
            ORDER BY ano
            ```
            
            ```sql
            SELECT DATEPART(YEAR, orderdate) Ano, DATEPART(MONTH, orderdate) Mes, DATEPART(DAY, orderdate) Dia
            FROM Sales.SalesOrderHeader
            GROUP BY DATEPART(YEAR, orderdate), DATEPART(MONTH, orderdate), DATEPART(DAY, orderdate)
            ORDER BY dia, mes, ano
            ```
            

---

- Manipulação de String
    - Introdução:
        
        [https://docs.microsoft.com/pt-br/sql/t-sql/functions/string-functions-transact-sql?view=sql-server-ver15](https://docs.microsoft.com/pt-br/sql/t-sql/functions/string-functions-transact-sql?view=sql-server-ver15)
        
    
    ---
    
    - CONCAT
        - Ele vai juntar as String, os atribulos da tabelas
            - ele não juntará SEM ESPAÇOS
        - Exemplo SEM ESPAÇO:
            
            ```jsx
            SELECT CONCAT(FirstName, LastName)
            FROM Person.Person
            ```
            
        - Exemplo COM ESPAÇO:
            
            ```jsx
            SELECT CONCAT(FirstName,' ', LastName)
            FROM Person.Person
            ```
            
    
    ---
    
    - UPPER
        - Ele irá deixar todas as Strings maiúsculas
        - Exemplo:
            
            ```jsx
            SELECT UPPER(firstname)
            FROM Person.Person
            ```
            
    
    ---
    
    - LOWER
        - Ele irá deixar todas as Strings minúsculas
        - Exemplo:
            
            ```jsx
            SELECT LOWER(firstname)
            FROM Person.Person
            ```
            
    
    ---
    
    - LEN
        - Ele mostrará o tamanho da palavra
        - Exemplo:
            
            ```jsx
            SELECT firstname, LEN(firstname) Quantidade
            FROM Person.Person
            ORDER BY firstname
            ```
            
    
    ---
    
    - SUBSTRING
        - Sintaxe
            - SUBSTRING(tabela, inicio, fim)
        - Utilização
            - SUBSTRING(firstname, 1, 3)
        - Exemplo:
            
            ```jsx
            SELECT firstname, SUBSTRING(firstname, 1, 3)
            FROM Person.Person
            ```
            
    
    ---
    
    - REPLACE
        - Ele substitui
        - Seintaxe
            - REPLACE(tabela, item que vai ser substituido, item final)
        - Exemplo:
            
            ```jsx
            SELECT ProductNumber, REPLACE(productnumber, '-', '#')
            FROM Production.Product
            ```
            
    
    ---
    
    > Exemplo Geral
    > 
    > 
    > ```sql
    > SELECT CONCAT(UPPER(firstname), ' ', SUBSTRING(LOWER(LastName),1,2),'.'), LEN(CONCAT(UPPER(firstname), ' ', LOWER(LastName))) qtd_letras
    > FROM Person.Person
    > ```
    > 

---

- Sub SELECT
    
    > Exemplo 1:
    > 
    > - Exemplo SEM ele:
    >     
    >     ```sql
    >     SELECT *
    >     FROM Production.Product
    >     
    >     SELECT AVG(listprice)
    >     FROM Production.Product
    >     
    >     SELECT *
    >     FROM Production.Product
    >     WHERE ListPrice > 438.6662
    >     ```
    >     
    > - Exemplo COM ele:
    >     
    >     ```sql
    >     SELECT *
    >     FROM Production.Product
    >     WHERE ListPrice > (SELECT AVG(listprice) FROM Production.Product)
    >     ```
    >     
    
    > Exemplo 2:
    > 
    > - Exemplo SEM ele:
    >     
    >     ```sql
    >     SELECT *
    >     FROM person.person
    >     WHERE businessentityid IN (5, 6, 15)
    >     
    >     SELECT *
    >     FROM humanresources.employee
    >     WHERE jobtitle = 'Design Engineer'
    >     ```
    >     
    > - Exemplo COM ele:
    >     
    >     ```sql
    >     SELECT firstname
    >     FROM Person.Person
    >     WHERE BusinessEntityID IN(
    >     SELECT BusinessEntityID
    >     FROM HumanResources.Employee
    >     WHERE JobTitle = 'Design engineer')
    >     ```
    >     
    
    > Exemplo 3:
    > 
    > 
    > ```sql
    > SELECT *
    > FROM Person.Address pa
    > WHERE StateProvinceID IN(
    > SELECT StateProvinceID 
    > FROM Person.StateProvince
    > WHERE name = 'alberta')
    > ```
    > 

---

- X
    
    <aside>
    💡 F == important
    
    </aside>
    
    ```sql
    SELECT 19972 - 19118
    ```
    
    ```sql
    SELECT COUNT(*)
    FROM Production.Product
    WHERE ListPrice > 1500
    ```
    
    ```sql
    SELECT COUNT(DISTINCT (city))
    FROM Person.Address
    ```
    
    ```sql
    SELECT DISTINCT (city)
    FROM Person.Address
    ```
    
    ```sql
    SELECT COUNT(color)
    FROM Production.Product
    WHERE color IN('red') and ListPrice BETWEEN 500 AND 1000
    ```
    
    ```sql
    SELECT count (*)
    FROM Production.Product
    WHERE name LIKE '%road%'
    ```
    

---

- REFERÊNCIAS — F
    - Todos os créditos para:
        1. [https://www.youtube.com/watch?v=rX2I7OjLqWE](https://www.youtube.com/watch?v=rX2I7OjLqWE)
            1. [https://drive.google.com/file/d/1LCofjYj-pV1asBLrxtgPDsbqMFRefHW5/view](https://drive.google.com/file/d/1LCofjYj-pV1asBLrxtgPDsbqMFRefHW5/view)
            2. [https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/databases/northwind-pubs/instnwnd.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/databases/northwind-pubs/instnwnd.sql)
        2. Microsoft
            1. [https://docs.microsoft.com/pt-br/sql/t-sql/functions/datepart-transact-sql?view=sql-server-ver15](https://docs.microsoft.com/pt-br/sql/t-sql/functions/datepart-transact-sql?view=sql-server-ver15)
            2. [https://docs.microsoft.com/pt-br/sql/t-sql/data-types/numeric-types?view=sql-server-ver15](https://docs.microsoft.com/pt-br/sql/t-sql/data-types/numeric-types?view=sql-server-ver15)