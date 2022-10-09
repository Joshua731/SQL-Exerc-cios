# SQL-Exerc-cios
Lista de resoluções de exercícios do livro "SQL Curso Prático" de Celso Oliveira

## Parte I

### Capítulo 2: Projetando bancos de dados
#### Exercício 1
##### Resposta:
Gênero x Filme = n:n;

Filme x Categoria = 1:n;

Locação x Filme = n:n;

Cliente x Locação = 1:n;


#### Exercício 2
##### Resposta:
Vendedor x Imóvel = 1:1;

Imóvel x Oferta = 1:n;

Comprador x Oferta = 1:n;

Imóvel x Estado = n:n;

Estado x Cidade = 1:n;

Cidade x Bairro = 1:n;

Bairro x Faixa_Imóvel = 1:n;

#### Exercício 3
##### Resposta:
###### Atributos:

Loja = CDLoja, NMLoja, CDPedido;

Pedido = CDPedido, QtPedido, CDProduto, CDLoja, DTPedido;

Cliente = CDCliente, NMCliente;

Produto = CDProduto, NMProduto, VLProduto;

Automóvel = CDAutomovel, MCAutomovel, CDCliente;

###### Relacionamentos:

Loja x Pedido = 1:n;

Pedido x Cliente = 1:n;

Produto x Pedido = n:n;

Automóvel x Cliente = 1:n;

#### Exercício 4
##### Resposta da letra A:
![MER EX 4 A](https://user-images.githubusercontent.com/88397658/194727838-04b00a50-e04e-45ad-91b8-2c147bae2e40.png)

##### Resposta da letra B:

![MER EX 4 B](https://user-images.githubusercontent.com/88397658/194728810-4e7739f0-2a54-4ad4-93b7-4425def0a68c.png)

##### Resposta da letra C:
![MER EX 4 C](https://user-images.githubusercontent.com/88397658/194729299-a5e5a6bc-c03d-4932-b29a-fc4580da49af.png)


### Capítulo 3: Normalização de dados

#### Resposta:
Generalizando, todas as relações n:n, dentre as quais existem essa condição: Gênero x Filme & Locação x Filme (Exercício 1, Capítulo 2), Imóvel x Estado (Exercício 2, Capítulo 2) e Produto x Pedido (Exercício 3, Capítulo 2), devem obedecer a Primeira Forma Normal, pois uma relação n:n deve virar duas relações 1:n sendo intermediada por uma tabela Gênero_Filme/Locação_Filme/Imóvel_Estado/Produto_Pedido, por exemplo, para evitar valores repetidos.

### Capítulo 4: Criando um banco de dados
#### Resposta do exercício 1:

##### TABELAS

CREATE TABLE VENDEDOR (

CDVENDEDOR INTEGER NOT NULL, 

NMVENDEDOR VARCHAR(40) NULL,

NMENDERECO VARCHAR(40) NULL, 

NRCPF DECIMAL (11) NULL,

NMCIDADE VARCHAR(20) NULL,

NMBAIRRO VARCHAR(20) NULL,

SGESTADO CHAR(2) NULL,

TELEFONE VARCHAR(20) NULL,

EMAIL VARCHAR(80) NULL);


ALTER TABLE VENDEDOR

ADD ( PRIMARY KEY (CDVENDEDOR));



CREATE TABLE COMPRADOR (

CDCOMPRADOR INTEGER NOT NULL,

NMVENDEDOR VARCHAR(40) NULL,

NMENDERECO VARCHAR(40) NULL, 

NRCPF DECIMAL (11) NULL,

NMCIDADE VARCHAR(20) NULL,

NMBAIRRO VARCHAR(20) NULL,

SGESTADO CHAR(2) NULL,

TELEFONE VARCHAR(20) NULL,

EMAIL VARCHAR(80) NULL 
);


ALTER TABLE COMPRADOR

ADD ( PRIMARY KEY (CDCOMPRADOR) )



CREATE TABLE IMOVEL (

CDMOVEL INTEGER NOT NULL,

CDVENDEDOR INTEGER NOT NULL,

CDBAIRRO INTEGER NOT NULL,

CDCIDADE INTEGER NOT NULL,

SGESTADO CHAR(2) NOT NULL,

NMENDERECO VARCHAR(40) NULL, 

NRAREAUTIL DECIMAL (10,2) NULL,

NRAREATOTAL DECIMAL (10,2) NULL,

DSIMOVEL VARCHAR(300) NULL,

VLPRECO DECIMAL (16,2) NULL,

NROFERTAS INTEGER NULL,

STVENDIDO CHAR(1) NULL,

DTLANCTO DEFAULT SYSDATE,

IMOVEL_INCDICADO INTEGER NULL
);


ALTER TABLE IMOVEL

ADD (PRIMARY KEY (CDMOVEL));


ALTER TABLE IMOVEL

ADD (FOREYGN KEY (CDVENDEDOR)

REFERENCES VENDEDOR);


ALTER TABLE IMOVEL

ADD (FOREYGN KEY (CDBAIRRO)

REFERENCES BAIRRO);


ALTER TABLE IMOVEL

ADD (FOREYGN KEY (CDCIDADE)

REFERENCES CIDADE);


ALTER TABLE IMOVEL

ADD (FOREYGN KEY (SGESTADO)

REFERENCES ESTADO);


CREATE TABLE OFERTA (

CDIMOVEL INTEGER NOT NULL, 

CDCOMPRADOR INTEGER NOT NULL,

VLOFERTA NUMBER (16,2) NULL,

DTOFERTA DEFAULT SYSDATE

);


ALTER TABLE OFERTA

ADD (

FOREYGN KEY (CDIMOVEL)

REFERENCES IMOVEL

);

ALTER TABLE OFERTA

ADD (

FOREYGN KEY (CDCOMPRADOR)

REFERENCES COMPRADOR

);


CREATE TABLE ESTADO (

SGESTADO CHAR(2) NOT NULL, 

NMESTADO VARCHAR(20) NULL, 

);


ALTER TABLE ESTADO

ADD (PRIMARY KEY (SGESTADO));


CREATE TABLE CIDADE (

SGESTADO CHAR(2) NOT NULL, 

CDCIDADE INTEGER NOT NULL,

NMCIDADE VARCHAR(20) NULL, 

);


ALTER TABLE CIDADE

ADD (PRIMARY KEY (CDCIDADE));


ALTER TABLE CIDADE

ADD (FOREIGN KEY (SGESTADO)

REFERENCES ESTADO);


CREATE TABLE BAIRRO (

SGESTADO CHAR(2) NOT NULL, 

CDCIDADE INTEGER NOT NULL,

CDBAIRRO INTEGER NOT NULL,

NMBAIRRO VARCHAR(20) NULL, 

);


ALTER TABLE BAIRRO

ADD (PRIMARY KEY (CDBAIRRO));


ALTER TABLE BAIRRO

ADD (FOREIGN KEY (SGESTADO)

REFERENCES ESTADO);


ALTER TABLE BAIRRO

ADD (FOREIGN KEY (CDCIDADE)

REFERENCES CIDADE);


CREATE TABLE FAIXA_IMOVEL (

CDFAIXA INTEGER NOT NULL,

VLMINIMO DECIMAL(14, 2) NULL, 


VLMAXIMO DECIMAL(14, 2) NULL,

);



ALTER TABLE FAIXA_IMOVEL

ADD (PRIMARY KEY (CDFAIXA));


##### RELAÇÕES

VENDEDOR X IMOVEL = N:N;

COMPRADOR X OFERTA = 1:N;

OFERTA X IMOVEL = 1:N;

IMOVEL X BAIRRO = N:N;

CIDADE X BAIRRO = 1:N;

ESTADO CIDADE = 1:N.

#### Resposta do exercício 2:

CREATE INDEX nm_vendedor_index ON VENDEDOR

(NMVENDEDOR ASC);



CREATE INDEX nm_vendedor_index ON COMPRADOR

(NMCOMPRADOR ASC);

#### Resposta do exercício 3:


CREATE INDEX cd_imovel_index ON OFERTA

(CDIMOVEL ASC);


CREATE INDEX vl_oferta_index ON OFERTA

(CDIMOVEL DESC);



### Capítulo 5: Incluindo, atualizando e excluindo linhas nas tabelas

#### Resposta do exercício 1:

INSERT INTO ESTADO VALUES ('RS', 'RIO GRANDE DO SUL');


INSERT INTO ESTADO VALUES ('ES', 'ESPÍRITO SANTO');

#### Resposta do exercício 2:

INSERT INTO CIDADE VALUES (1, 'PORTO ALEGRE', 'RS');

INSERT INTO CIDADE VALUES (1, 'VITÓRIA', 'ES');

#### Resposta do exercício 3:

INSERT INTO BAIRRO VALUES (1, 'BELÉM NOVO', 1, 'RS'); 

INSERT INTO BAIRRO VALUES (1, 'PRAIA DO CANTO', 1, 'ES'); 

#### Resposta do exercício 4:

INSERT INTO VENDEDOR VALUES (5, 'JOSHUA CAVAZZANI', 'RUA NILO PEÇANHA, 100', 'jo.cvzn1001@gmail.com'); 

INSERT INTO VENDEDOR VALUES (6, 'SOFIA CAVAZZANI', 'RUA NILO PEÇANHA, 112', 'sofis.cvzn@gmail.com');


#### Resposta do exercício 5:

INSERT INTO IMOVEL VALUES (7, 5, 1, 1, 'RS', 'Avenida Alberto Bins, 69', 330, 660, 99900, 6);

INSERT INTO IMOVEL VALUES (8, 6, 1, 1, 'ES', 'Rua Flamboyans, 69', 520, 720, 199900, 7);


#### Resposta do exercício 6:


INSERT INTO COMPRADOR VALUES (5, 'FELIPE CAVAZZANI', 'RUA VENCESLAU BRAZ, 90', 'felipe.cavazzani@outlook.com');

INSERT INTO COMPRADOR VALUES (6, 'MAURICIO CAVAZZANI', 'RUA RUSSIA, 94', 'mauricio.cavazzani@gmail.com');



#### Resposta do exercício 7:


INSERT INTO OFERTA VALUES (5, 7, 88800, '06/09/2019');

INSERT INTO OFERTA VALUES (6, 6, 111100, '22/02/2022');


#### Resposta do exercício 8:

UPDATE IMOVEL

SET VLPRECO = VLPRECO * 1.10;


#### Resposta do exercício 9:

UPDATE IMOVEL

SET VLPRECO = VLPRECO - (VLPRECO * 0.05)

WHERE CDVENDEDOR = 1;


#### Resposta do exercício 10:

UPDATE OFERTA

SET VLOFERTA = VLOFERTA * 1.05

WHERE CDCOMPRADOR = 2;


#### Resposta do exercício 11:

UPDATE COMPRADOR

SET NMENDERECO = 'RANANAS, 45'

WHERE CDCOMPRADOR = 3;


UPDATE COMPRADOR

SET NMENDERECO = 'RANANAS, 45', ESTADO = 'RJ

WHERE CDCOMPRADOR = 3;


#### Resposta do exercício 12:

UPDATE OFERTA

SET VLORFERTA = 101000

WHERE CDCOMPRADOR = 2 AND CDIMOVEL = 4;


#### Resposta do exercício 13:

DELETE FROM OFERTA

WHERE CDCOMPRADOR = 3 AND CDIMOVEL = 1;


#### Resposta do exercício 14:

DELE FROM CIDADE

WHERE CDCIDADE = 3 AND SGESTADO = 'SP';


#### Último exercício da parte I(15):

INSERT INTO FAIXA_IMOVEL VALUES (4, 'BAIXO', 230, 230000);

INSERT INTO FAIXA_IMOVEL VALUES (5, 'MÉDIO', 2300, 320000);

FIM!
