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


