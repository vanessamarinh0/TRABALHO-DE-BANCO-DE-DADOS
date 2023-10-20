# TRABALHO-DE-BANCO-DE-DADOS
# Mercantil 

No nosso trabalho optamos por apresentar um sistema de um mercantil que consiste no cadastro dos clientes que fazem sua compra do mês no estabelecimento. Dentro desse cadastro vai estar contidas informações tanto do cliente quanto do produto que esse indivíduo efetuou a compra, como também informações da pessoa que vendeu a mercadoria para o cliente. Portanto o cadastro é baseado na relação de cliente até a venda do produto.

# Diagrama de Entidade e Relacionamento
![image](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/34771733-a8f0-4130-8ffb-fd8988b34d18)


1. Vamos separar todas as tabelas com seus atributos e indicando sua respectiva chave primária(pk):
   
         cliente(**cod_cliente**, nome_cliente,cpf_cliente,endereco_cliente)

          produto(**cod_produto**, cod_cliente,tipo_produto, marca_produto,valor_produto)
            cod_cliente referencia cliente
             cod_funcionario referencia funcionario

          funcionario(**cod_funcionario**, nome_funcionario,turno_funcionario)
   
3. Vamos analisar o relacionamento entre essas tabelas:

    a. Relacionamento entre *cliente* e *produto*:
     - (1, 1): Um produto só pode ser comprado por um cliente.
	  - (1, n): Um cliente pode comprar vários produtos. 	
		
  	Identificamos que produto tem uma chave estrangeira(fk) vinda de cliente, o **n** da entidade Cliente indo para a entidade Produto.

    Cliente não tem chave estrangeira(fk), apenas sua chave primária(pk) mesmo.

        cliente(**cod_cliente**, nome_cliente,cpf_cliente,endereco_cliente)

        produto(**cod_produto**, cod_cliente,tipo_produto, marca_produto,valor_produto)
            cod_cliente referencia cliente
   
      b. Relacionamento entre *produto* e *funcionario*:
      - (1, 1): Um produto só pode ser vendido por um funcionário.
	  - (1, n): Um funcionário pode vender vários produtos.
  
     Identificamos que produto tem uma chave estrangeira(fk) vinda de cliente, o **n** da entidade Funcionário indo para a entidade Produto.

    Funcionario não tem chave estrangeira(fk), apenas sua chave primária(pk) mesmo.

        funcionario(**cod_funcionario**, nome_funcionario,turno_funcionario)

        produto(**cod_produto**, cod_funcionario,tipo_produto, marca_produto,valor_produto)
            cod_funcionario referencia funcionario

# Modelo Lógico - BrModelo
![img](https://github.com/vanessamarinh0/TRABALHO-DE-BANCO-DE-DADOS/assets/111614156/7404c4ca-5692-42fb-a079-70df69cc3117)

## 👩🏻‍💻 Tecnologias utilizadas
Projeto que utiliza uma variedade de tecnologias de desenvolvimento web para a criação de um sistema com conexão com o banco de dados:

📍 BrModelo

📍PhpMyadmin

📍 PHP

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
