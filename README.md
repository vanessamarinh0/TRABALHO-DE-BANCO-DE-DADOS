# TRABALHO-DE-BANCO-DE-DADOS
# Mercantil Atacadão do Sertões

No nosso trabalho optamos por apresentar um sistema de um mercantil que consiste no cadastro dos clientes que fazem sua compra do mês no estabelecimento. Dentro desse cadastro vai estar contidas informações tanto do cliente quanto do produto que esse indivíduo efetuou a compra, como também informações da pessoa que vendeu a mercadoria para o cliente. Portanto o cadastro é baseado na relação de cliente até a venda do produto.

# Diagrama de Entidade e Relacionamento
![julia-mer(FOTO)](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/dedcc57a-61fa-4e66-81f3-27a775f315f2)



1. Vamos separar todas as tabelas com seus atributos e indicando sua respectiva chave primária(pk):
   
         cliente(**cod_cliente**, nome_cliente,cpf_cliente,endereco_cliente)
   
		compra(*cod_compra*, valor_compra, cod_cliente)
   		 	cod_cliente referencia cliente
   
          produto(*cod_produto*, tipo_produto, marca_produto,valor_produto, cod_compra, cod_funcionario)
			cod_compra referenca compra
 			   cod_funcionario referencia funcionario

          funcionario(**cod_funcionario**, nome_funcionario,turno_funcionario)
   
2. Vamos analisar o relacionamento entre essas tabelas:

    a. Relacionamento entre cliente e compra:
     - (1, 1): Uma compra só pode ser feita por um cliente.
	  - (1, n): Um cliente pode fazer várias compras. 	
		
  	Identificamos que compra tem uma chave estrangeira(fk) vinda de cliente, o *n* da entidade Cliente indo para a entidade Compra.

    Cliente não tem chave estrangeira(fk), apenas sua chave primária(pk) mesmo.

        cliente(*cod_cliente*, nome_cliente,cpf_cliente,endereco_cliente)

        compra(*cod_compra*, valor_compra, cod_cliente)
   		 	cod_cliente referencia cliente
   
   b. Relacionamento entre compra e produto:
     - (1, 1): Um produto só pode ser de uma compra.
	  - (1, n): Uma compra pode ter mais de um produto. 	
		
  	Identificamos que produto tem uma chave estrangeira(fk) vinda de compra, o *n* da entidade Compra indo para a entidade Produto.

    Compra não tem chave estrangeira(fk), apenas sua chave primária(pk) mesmo.

        compra(*cod_compra*, valor_compra)
   
          produto(*cod_produto*, tipo_produto, marca_produto,valor_produto, cod_compra)
			cod_compra referenca compra

   
      c. Relacionamento entre produto e funcionario:
      - (1, 1): Um produto só pode ser vendido por um funcionário.
	  - (1, n): Um funcionário pode vender vários produtos.
  
     Identificamos que produto tem uma chave estrangeira(fk) vinda de funcionario, o *n* da entidade Funcionário indo para a entidade Produto.

    Funcionario não tem chave estrangeira(fk), apenas sua chave primária(pk) mesmo.

        funcionario(*cod_funcionario*, nome_funcionario,turno_funcionario)

        produto(*cod_produto*, tipo_produto, marca_produto,valor_produto, cod_funcionario)
            cod_funcionario referencia funcionario
   
   

# Modelo Lógico - BrModelo
![JULIA-LOGICO(CERTO)-FOTO](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/b0b26c4e-1735-4c76-a5a0-c98e8498d17b)

# Códigos PHP
## código.sql
Código SQL é inserido no banco de dados para criar as tabelas, neles cada entidade formam uma tabela, com seus respectivos atributos e os tipos a eles definidos. A chave primária é definida como AUTO_INCREMENT para que um único número seja gerado a cada novo registro inserido na tabela.


	CREATE TABLE cliente (
    cod_cliente INT AUTO_INCREMENT PRIMARY KEY,
    cpf_cliente INT(16),
    endereco_cliente VARCHAR(100),
    nome_cliente VARCHAR(100)
);

	CREATE TABLE compra (
    valaor_compra FLOAT,
    cod_compra INT AUTO_INCREMENT PRIMARY KEY,
    fk_cliente_cod_cliente INT
);

	CREATE TABLE produto (
    cod_produto INT AUTO_INCREMENT PRIMARY KEY,
    tipo_produto VARCHAR(50),
    marca_produto VARCHAR(50),
    valor_produto FLOAT,
    fk_compra_cod_compra INT,
    fk_funcionario_cod_funcionario INT(16)
);

	CREATE TABLE funcionario (
    cod_funcionario INT(16) AUTO_INCREMENT PRIMARY KEY,
    nome_funcionario VARCHAR(100),
    turno_funcionario VARCHAR(50)
);

 	ALTER TABLE compra ADD CONSTRAINT FK_compra_2
    FOREIGN KEY (fk_cliente_cod_cliente)
    REFERENCES cliente (cod_cliente)
    ON DELETE RESTRICT;
 	
 	 ALTER TABLE produto ADD CONSTRAINT FK_produto_2
    FOREIGN KEY (fk_compra_cod_compra)
    REFERENCES compra (cod_compra)
    ON DELETE RESTRICT;
	
 	ALTER TABLE produto ADD CONSTRAINT FK_produto_3
    FOREIGN KEY (fk_funcionario_cod_funcionario)
    REFERENCES funcionario (cod_funcionario)
    ON DELETE RESTRICT;

## inserirdados.sql
Insere dados nas tabelas.

	INSERT INTO cliente (cod_cliente, cpf_cliente, endereco_cliente, nome_cliente) VALUES
	(1, '12345678900', 'Rua Exemplo, 123', 'Janaina'),
	(2, '98765432101', 'Avenida Principal, 456', 'Alberto'),
	(3, '55555555555', 'Travessa do Centro, 789', 'Carlos'),
	(4, '11122233344', 'Rua da Amostra, 789', 'Daiana'),
	(5, '44433322211', 'Avenida Central, 987', 'Rosa'),
	(6, '99988877766', 'Rua da Simulação, 567', 'Rafaela'),
	(7, '77788899900', 'Avenida Modelo, 345', 'Mario'),
	(8, '22233344455', 'Travessa Abstrata, 123', 'Claudio'),
	(9, '66677788899', 'Rua Genérica, 789', 'Marcia'),
	(10, '33344455566', 'Avenida Imaginária, 234', 'Sandra');
	INSERT INTO compra (valaor_compra, cod_compra,fk_cliente_cod_cliente) VALUES
	(62.2,1,1),
	(75.5,2,2),
	(89.99,3,3),
	(68.5,4,4),
	(32.4,5,5),
	(95.25,6,6),
	(45.99,7,7),
	(120,8,8),
	(54.75,9,9),
	(125.75,10,10);
	INSERT INTO funcionario (cod_funcionario, nome_funcionario, turno_funcionario) VALUES
	(1, 'Pedro Almeida', 'Noite'),
	(2, 'Mariana Costa', 'Noite'),
	(3, 'João Silva', 'Manhã'),
	(4, 'Maria Santos', 'Tarde'),
	(5, 'Fernando Souza', 'Noite'),
	(6, 'Carlos Gomes', 'Tarde'),
	(7, 'Luiz Oliveira', 'Manhã'),
	(8, 'Isabela Rodrigues', 'Tarde'),
	(9, 'Larissa Carvalho', 'Manhã'),
	(10, 'Ana Pereira', 'Manhã');
	INSERT INTO produto (cod_produto, tipo_produto, marca_produto, valor_produto, fk_compra_cod_compra, fk_funcionario_cod_funcionario) VALUES
	(1,'Alimentos', 'Nestlé', 10.0,1,1),
	(2,'Móveis', 'IKEA', 10.01,2,2),
	(3,'Vestuário', 'Nike', 9.99,3,3),
	(4,'Eletrônico', 'Sony', 9.99,4,4),
	(5,'Eletrônico', 'Sony', 19.99,5,5),
	(6,'Vestuário', 'Nike', 9.99,6,6),
	(7,'Móveis', 'IKEA', 25.51,7,7),
	(8,'Alimentos', 'Nestlé', 20.01,8,8),
	(9,'Eletrônico', 'Sony', 19.99,9,9),
	(10, 'Vestuário', 'Nike', 9.99,10,10);
 
## conexao.php
Arquivo que conecta ao banco de dados.

	<?php

	$servidor = "localhost" ;
	$usuario = "root" ;
	$senha = "";
	$banco_de_dados = "trabalho";

	$conexao =  mysqli_connect($servidor, $usuario, $senha, $banco_de_dados);
	/* MYSQLI CONNECT - ele conecta ao banco */

	?>
## mercantil.php
Página inicial que direciona para outras páginas.

	<?php include 'header.php';?>
	<!DOCTYPE html>
	<html lang="en">
	<head>
    	<meta charset="UTF-8">
    	<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<link rel="stylesheet" href="mercantil.css">
		<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KK94CHFLLe+nY2dmCWGMq91rCGa5gtU4mk92HdvYe+M/SXH301p5ILy+dN9+nJOZ" crossorigin="anonymous">
  		<title>Mercantil</title>
	</head>
	<body style="background-image: url('imagem.jpeg'); background-size: cover; min-height: 100%;
	background-repeat: no-repeat;
	background-position: center center;" >
  	  <h1 style="position: absolute; text-align: center; margin-left: 117px; margin-top: 200px; font-family: fantasy; font-weight: bold; color: #352ec143;">BEM VINDO AO <br> MERCANTIL <br> ATACADÃO DO SERTÃO</h1>
    
	  <div style="text-align: center; margin-left: 69px; margin-right: auto; margin-top: 400px; height: 250px; width: 450px;  background-color: #352ec143; border-radius: 30px; box-shadow: 0.5em 0.5em 0.5em #85caffe9; font-family: fantasy;">
		<br><br>
	 	<h1>CADASTRA-SE</h1>
   		<br><br>
		<button style="height: 60px; width: 225px; font-family: fantasy; border-radius: 30px;" onclick="window.open('http://localhost/bancodedadostrab/index.php')">Clique aqui!</button>
  	  </div>
	</body>
	</html>
 
## index.php
Página php para salvar informações das respectivas entidades criadas no modelo relacional (cliente, compra, funcionário e produto).



## 👩🏻‍💻 Tecnologias utilizadas
Projeto que utiliza uma variedade de tecnologias de desenvolvimento web para a criação de um sistema com conexão com o banco de dados:

📍 BrModelo

📍PhpMyadmin

📍 MySQL

📍 SQL

📍 HTML

📍 CSS

📍 Visual Studio Code (VSCode)

📍 GitHub

## 👥 Autores
[Alanna Lopes](https://github.com/AlanaLopes)

[Ana Luiza](https://github.com/Nalu2)

[Antonio Jhonatta](https://github.com/Jhonatta-oliveira)

[Francisca Vanessa](https://github.com/vanessamarinh0)

[Júlia Barros](https://github.com/Juliabarros-info)

[Pedro Wesley](https://github.com/byID887766pedro)


* **Criador do Diagrama de Entidade e Relacionamento** - *BrModelo* - [Júlia Barros](https://github.com/Juliabarros-info) 
* **Desenvolvedores** - *PHP, HTML, CSS* - [Alanna Lopes](https://github.com/AlanaLopes), [Ana Luiza](https://github.com/Nalu2) e [Pedro Wesley](https://github.com/byID887766pedro)
* **Criadores do README** - *GitHub* - [Antonio Jhonatta](https://github.com/Jhonatta-oliveira) e [Francisca Vanessa](https://github.com/vanessamarinh0)
