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
     
![codigo php](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/8e31cd63-ce30-4c20-8196-8c227aeec5a1)

## inserirdados.sql
Insere dados nas tabelas.

	INSERT INTO cliente (cod_cliente, cpf_cliente, endereco_cliente, nome_cliente)
	VALUES
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
	INSERT INTO compra (valaor_compra, cod_compra,fk_cliente_cod_cliente)
	VALUES
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
	INSERT INTO funcionario (cod_funcionario, nome_funcionario, turno_funcionario)
	VALUES
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
	INSERT INTO produto (cod_produto, tipo_produto, marca_produto, valor_produto, fk_compra_cod_compra, fk_funcionario_cod_funcionario)
	VALUES
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

![inserir php](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/bf328410-3dc6-4222-b023-1eead1425357)
![inserir](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/f7174e14-c708-416d-9a63-f4aaf04e60fd)


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
 
## header.php
Cria um cabeçalho para todas as páginas php.
	
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <meta name="viewport" content="width=device-width, initial-scale=1.0">
	    <link rel="stylesheet" href="mercantil.css">
	    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KK94CHFLLe+nY2dmCWGMq91rCGa5gtU4mk92HdvYe+M/SXH301p5ILy+dN9+nJOZ" crossorigin="anonymous">
	    <title>Mercantil</title>
	</head>
	<body>
	
	            <nav class="navbar navbar-expand-lg body-tertiary" style="background-color: #352ec143;">
	        <div class="container-fluid">
	            <a class="navbar-brand">Mercantil</a>
	            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
	            <span class="navbar-toggler-icon"></span>
	          </button> 
	            <div class="collapse navbar-collapse" id="navbarSupportedContent">
	                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
	                    <li class="nav-item">
	                        <a class="nav-link" href="mercantil.php">Home</a>
	                    </li>
	                    <li class="nav-item">
	                        <a class="nav-link" href="tabela.php">Tabela</a>
	                    </li>
	                    <li class="nav-item dropdown">
	                        <a class="nav-link" href="graficos.php">Gráficos</a>
	                    </li>
	                </ul>
	                <form class="d-flex" role="Search">
	                    <input class="form-control me-2" type="Search" placeholder="Pesquisar" aria-label="Search">
	                    <button class="btn btn-outline-success" type="submit">Pesquisar</button>
	                </form>
	            </div>
	        </div>
	    </nav>

![hea der php](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/5234a16d-0aab-453a-8a18-4a2582aaee85)

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

 ![mer cantil php](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/9757f084-a140-46e6-87f9-002949acd764)

## index.php
Página php para salvar informações das respectivas entidades criadas no modelo relacional (cliente, compra, funcionário e produto).
	
	<?php include 'header.php';?>
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <meta name="viewport" content="width=device-width, initial-scale=1.0">
	    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KK94CHFLLe+nY2dmCWGMq91rCGa5gtU4mk92HdvYe+M/SXH301p5ILy+dN9+nJOZ" crossorigin="anonymous">
	    <title>CRUD PHP</title>
	</head>
	<body style="background-image: url('imagem.jpeg'); background-size: cover; min-height: 100%;
	background-repeat: no-repeat;
	background-position: center center;">
	    <form method="post" action="salvar.php">
	    <div class="container" style="text-align: center; margin-left: 70px; margin-top: 50px; height: 340px; width: 550px; border: 2px solid black; border-radius: 10px;">
	        <h1>CLIENTE</h1>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            CPF: <input class="form-control" name="cpf_cliente">
	            </div>
	        </div>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Endereço: <input class="form-control" name="end_cliente">
	            </div>
	        </div>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Nome: <input class="form-control" name="nome_cliente">
	            </div>
	        </div>
	        <br>
	    </div>
	    <div class="container" style="text-align: center; margin-left: 70px; margin-top: 50px; height: 180px; width: 550px; border: 2px solid black; border-radius: 10px;">
	        <h1>COMPRA</h1>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Valor: <input class="form-control"  name="valor_compra">
	            </div>
	        </div>
	        <br>
	    </div>
	    <div class="container" style="text-align: center; margin-left: 70px; margin-top: 50px; height: 250px; width: 550px; border: 2px solid black; border-radius: 10px;">
	        <h1>FUNCIONÁRIO</h1>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Nome: <input class="form-control" name="nome_funcionario">
	            </div>
	        </div>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Turno: <input class="form-control" name="turno_funcionario">
	            </div>
	        </div>
	        <br>
	    </div>
	    <div class="container" style="text-align: center; margin-left: 70px; margin-top: 50px; height: 340px; width: 550px; border: 2px solid black; border-radius: 10px;">
	        <h1>PRODUTO</h1>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Tipo: <input class="form-control" name="tipo_produto">
	            </div>
	        </div>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Marca: <input class="form-control" name="marca_produto">
	            </div>
	        </div>
	        <br>
	        <div class="row">
	            <div class="col-sm">
	            Valor: <input class="form-control"  name="valor_produto">
	            </div>
	        </div>
	        <br>
	    </div>
	
	    <div class="row" style="text-align: center; margin-left: 70px; margin-top: 10px; height: 50px; width: 550px;">
	                <button type="submit" class=" btn btn-primary">Salvar</button>
	                <br>
	                <br>
	    </div>
	    </form>
	</body>
	</html>
 ![index phpp](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/393973fd-fd51-469c-91ec-f544d9053789)

 ## salvar.php
Código utilizado para salvar as informações inseridas, das respectivas entidades, no banco de dados.

	<?php
	include 'conexao.php';
	
	$cpf_cliente = $_POST['cpf_cliente'];
	$end_cliente = $_POST['end_cliente'];
	$nome_cliente = $_POST['nome_cliente'];
	
	$valor_compra = $_POST['valor_compra']; 
	
	$nome_funcionario = $_POST['nome_funcionario'];
	$turno_funcionario = $_POST['turno_funcionario'];
	
	$tipo_produto = $_POST['tipo_produto'];
	$marca_produto = $_POST['marca_produto'];
	$valor_produto = $_POST['valor_produto'];
	
	if (mysqli_query($conexao, "INSERT INTO cliente(cpf_cliente, endereco_cliente, nome_cliente) VALUES ('$cpf_cliente', '$end_cliente', '$nome_cliente')")) {
	    $id = mysqli_insert_id($conexao);
	}
	if (mysqli_query($conexao, "INSERT INTO compra(valaor_compra, fk_cliente_cod_cliente) VALUES ('$valor_compra', '$id')")) {
	    $id2 = mysqli_insert_id($conexao);
	}
	if (mysqli_query($conexao, "INSERT INTO funcionario(nome_funcionario, turno_funcionario) VALUES ('$nome_funcionario', '$turno_funcionario')")) {
	    $id3 = mysqli_insert_id($conexao);
	}
	if (mysqli_query($conexao, "INSERT INTO produto(fk_funcionario_cod_funcionario,fk_compra_cod_compra,tipo_produto, marca_produto, valor_produto) VALUES ('$id3','$id2','$tipo_produto', '$marca_produto', '$valor_produto')")) {
	    $id4 = mysqli_insert_id($conexao);
	}
	header('location: index.php');
	
	?>
## listar.php
Código utilizado para fazer as consultas.

	<?php
		include 'conexao.php';
	        $listarSQL = mysqli_query($conexao, "SELECT * FROM cliente");
	    $listarSQL2 = mysqli_query($conexao, "SELECT * FROM compra");
	    $listarSQL3 = mysqli_query($conexao, "SELECT * FROM funcionario");
	    $listarSQL4 = mysqli_query($conexao, "SELECT * FROM produto");
	    $listarSQL5 = mysqli_query($conexao, "SELECT cpf_cliente FROM cliente");
	    $listarSQL6 = mysqli_query($conexao, "SELECT nome_funcionario FROM funcionario WHERE turno_funcionario = 'Noite'");
	    $listarSQL7 = mysqli_query($conexao, "SELECT cod_produto FROM produto WHERE tipo_produto = 'Eletrônico'");
	    $listarSQL8 = mysqli_query($conexao, "SELECT marca_produto FROM produto ");
	    $listarSQL9 = mysqli_query($conexao, "SELECT DISTINCT nome_cliente FROM cliente ORDER BY (nome_cliente)");
	    $listarSQL10 = mysqli_query($conexao, "SELECT cod_compra FROM compra WHERE valaor_compra < 50.00");
	?>

## tabela.php
Os resultados das consultas.

	<?php include 'header.php';?>
	<?php
	include 'listar.php';
	include 'conexao.php';
	?>
	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8">
		<title>Tabela PHP</title>
		<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet">
		<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js"></script>
	</head>
	<body style="background-image: url('imagem2.jpeg'); background-size: cover; min-height: 100%;
	background-repeat: no-repeat;
	background-position: center center;">
		<br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>DADOS DA TABELA CLIENTE</h1>
				<thead>
					<tr>
						<th scope="col">Código</th>
						<th scope="col">CPF</th>
						<th scope="col">Endereço</th>
						<th scope="col">Nome</th>
					</tr>
				</thead>
				<?php while ($cliente = mysqli_fetch_assoc($listarSQL)) { ?>
				<tbody>
					<tr>
						<td><?php echo $cliente['cod_cliente']; ?></td>
						<td><?php echo $cliente['cpf_cliente']; ?></td>
						<td><?php echo $cliente['endereco_cliente']; ?></td>
	                    <td><?php echo $cliente['nome_cliente']; ?></td>
					</tr>
	
				</tbody>
				<?php } ?>
			</table>
		</div>
	
	    <br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>DADOS DA TABELA COMPRA</h1>
				<thead>
					<tr>
						<th scope="col">Valor</th>
						<th scope="col">Código</th>
					</tr>
				</thead>
				<?php while ($compra = mysqli_fetch_assoc($listarSQL2)) { ?>
				<tbody>
					<tr>
						<td><?php echo $compra['valaor_compra']; ?></td>
						<td><?php echo $compra['cod_compra']; ?></td>
					</tr>
	
				</tbody>
				<?php } ?>
			</table>
		</div>
	
	    <br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>DADOS DA TABELA FUNCIONÁRIO</h1>
				<thead>
					<tr>
						<th scope="col">Código</th>
						<th scope="col">Nome</th>
	                    <th scope="col">Turno</th>
					</tr>
				</thead>
				<?php while ($funcionario = mysqli_fetch_assoc($listarSQL3)) { ?>
				<tbody>
					<tr>
						<td><?php echo $funcionario['cod_funcionario']; ?></td>
						<td><?php echo $funcionario['nome_funcionario']; ?></td>
	                    <td><?php echo $funcionario['turno_funcionario']; ?></td>
					</tr>
	
				</tbody>
				<?php } ?>
			</table>
		</div>
	
	    <br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>DADOS DA TABELA PRODUTO</h1>
				<thead>
					<tr>
						<th scope="col">Código</th>
						<th scope="col">Tipo</th>
	                    <th scope="col">Marca</th>
						<th scope="col">Valor</th>
					</tr>
				</thead>
				<?php while ($produto = mysqli_fetch_assoc($listarSQL4)) { ?>
				<tbody>
					<tr>
						<td><?php echo $produto['cod_produto']; ?></td>
						<td><?php echo $produto['tipo_produto']; ?></td>
	                    <td><?php echo $produto['marca_produto']; ?></td>
						<td><?php echo $produto['valor_produto']; ?></td>
					</tr>
	
				</tbody>
				<?php } ?>
			</table>
		</div>
	
		<br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>CPF DOS CLIENTES</h1>
				<thead>
					<tr>
						<th scope="col">CPF</th>
					</tr>
				</thead>
				<?php while ($cpf_cliente = mysqli_fetch_assoc($listarSQL5)) { ?>
				<tbody>
					<tr>
						<td><?php echo $cpf_cliente['cpf_cliente']; ?></td>
					</tr>
	
				</tbody>
				<?php } ?>
			</table>
		</div>
	
		<br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>NOME DOS FUNCIONÁRIOS QUE TRABALHAM NO TURNO DA NOITE</h1>
				<thead>
					<tr>
						<th scope="col">Nome</th>
					</tr>
				</thead>
				<?php while ($nome_funcionario = mysqli_fetch_assoc($listarSQL6)) { ?>
				<tbody>
					<tr>
						<td><?php echo $nome_funcionario['nome_funcionario']; ?></td>
					</tr>
				</tbody>
				<?php } ?>
			</table>
		</div>
	
		<br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>CÓDIGO DOS PRODUTOS ELETRÔNICOS</h1>
				<thead>
					<tr>
						<th scope="col">Código</th>
					</tr>
				</thead>
				<?php while ($cod_produto = mysqli_fetch_assoc($listarSQL7)) { ?>
				<tbody>
					<tr>
						<td><?php echo $cod_produto['cod_produto']; ?></td>
					</tr>
				</tbody>
				<?php } ?>
			</table>
		</div>
	
		<br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>MARCA DOS PRODUTOS</h1>
				<thead>
					<tr>
						<th scope="col">Marca</th>
					</tr>
				</thead>
				<?php while ($marca_produto = mysqli_fetch_assoc($listarSQL8)) { ?>
				<tbody>
					<tr>
						<td><?php echo $marca_produto['marca_produto']; ?></td>
					</tr>
				</tbody>
				<?php } ?>
			</table>
		</div>
	
		<br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>NOME DOS CLIENTES EM ORDEM ALFABÉTICA</h1>
				<thead>
					<tr>
						<th scope="col">Nome</th>
					</tr>
				</thead>
				<?php while ($nome_cliente = mysqli_fetch_assoc($listarSQL9)) { ?>
				<tbody>
					<tr>
						<td><?php echo $nome_cliente['nome_cliente']; ?></td>
					</tr>
				</tbody>
				<?php } ?>
			</table>
		</div>
	
		<br><br><br>
		<div class="container col-md-6 offset-md-3">
			<table  class="table  table-hover">
	        <h1>CÓDIGO DA COMPRA COM VALOR MENOR DE $50.00 REAIS</h1>
				<thead>
					<tr>
						<th scope="col">Código</th>
					</tr>
				</thead>
				<?php while ($cod_compra = mysqli_fetch_assoc($listarSQL10)) { ?>
				<tbody>
					<tr>
						<td><?php echo $cod_compra['cod_compra']; ?></td>
					</tr>
				</tbody>
				<?php } ?>
			</table>
		</div>
	    
	</body>
	</html>

 ![tabela phpp](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/a42376af-bbc1-4479-96ff-46965589d2b7)

 ## graficos.php
 Gráfico referente as respectivas entidades.
 
	 <?php include 'header.php';?>
	<?php
	// Configuração da conexão com o banco de dados
	$servidor = "localhost";
	$usuario = "root";
	$senha = "";
	$banco_de_dados = "trabalho";
	
	$conexao = mysqli_connect($servidor, $usuario, $senha, $banco_de_dados);
	
	// Consulta SQL para obter os dados da tabela "compra" (excluindo a chave estrangeira)
	$query = "SELECT valaor_compra, cod_compra FROM compra";
	$result = mysqli_query($conexao, $query);
	
	// Array para armazenar os dados
	$data = array();
	
	while ($row = mysqli_fetch_assoc($result)) {
	    $valaor_compra = $row['valaor_compra'];
	    $cod_compra = $row['cod_compra'];
	
	    // Adicione os dados ao array
	    $data[] = array($cod_compra, $valaor_compra);
	}
	
	mysqli_close($conexao);
	?>
	
	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
	    <script type="text/javascript">
	        google.charts.load('current', {'packages': ['corechart']});
	        google.charts.setOnLoadCallback(drawChart);
	
	        function drawChart() {
	            var data = new google.visualization.DataTable();
	            data.addColumn('string', 'Código da Compra');
	            data.addColumn('number', 'Valor da Compra');
	
	            <?php
	            foreach ($data as $row) {
	                $cod_compra = $row[0];
	                $valaor_compra = $row[1];
	
	                echo "data.addRow(['$cod_compra', $valaor_compra]);";
	            }
	            ?>
	
	            var options = {
	                title: 'Compras e seus Valores',
	                chart: {
	                    title: 'Compras e seus Valores'
	                }
	            };
	
	            var chart = new google.visualization.BarChart(document.getElementById('barchart'));
	
	            chart.draw(data, google.charts.Bar.convertOptions(options));
	        }
	    </script>
	</head>
	<body>
	    <h1>Gráfico de Compras e Valores</h1>
	    <div id="barchart" style="width: 900px; height: 500px;"></div>
	</body>
	</html>
## 👩🏻‍💻 Tecnologias utilizadas
Projeto que utiliza uma variedade de tecnologias de desenvolvimento web para a criação de um sistema com conexão com o banco de dados:

📍 BrModelo

📍PhpMyadmin

📍PHP

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
