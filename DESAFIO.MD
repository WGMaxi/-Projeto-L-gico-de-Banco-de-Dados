# Modelagem
![image](https://github.com/WGMaxi/-Projeto-L-gico-de-Banco-de-Dados/assets/118560480/e8de0815-35fa-4412-a70e-d553a54336cb)
## Código Modelagem
-- criação do banco de dados para o cenário de E-commmerce
create database ecommerce;

use ecommerce;

	-- criar tabela cliente
create table cliente(
		idcliente int auto_increment primary key,
        nome varchar(45) not null,
        lastnome varchar(45) not null,
        cpf char(14) not null,
        endereço varchar(45) not null,
        constraint unique_cpf_client unique(cpf)
);

alter table cliente auto_increment=1;
    -- criar tabela produto
create table produto(
		idproduto int auto_increment primary key,
        categoria enum('eletronicos','magazine','móveis') not null,
        descrição varchar(45),
        valor varchar(11),
        avaliação float default 0
);        
-- criar tabela tipo de pagamento
 create table tipo_pagamento(
		idpagamento int,
        idpedidocliente int,
        tipo_pagamento enum('Boleto','Cartão','Pix') not null,
        limite float,
        primary key (idpagamento,idpedidocliente)
); 

	-- criar tabela pedido
create table pedido(
		idpedido int auto_increment primary key,
        idpedidocliente int,
        pedidostatus enum('cancelado','entregue','em processamento','confirmado') not null default 'em processamento',
        descrição varchar(255),
        Frete float default 10,
        idpagamento boolean default false,
        constraint fk_tipo_pagamento_pedido foreign key (idpedidocliente) references cliente(idcliente)
	); 
    
	-- criar tabela estoque
        create table estoque(
		idestoque int auto_increment primary key,
        location varchar(45),
        quantidade int default 0
); 
    
	-- criar tabela fornecedor
 create table fornecedor(
		idfornecedor int auto_increment primary key,
        socialname varchar(255) not null,
        cnjp_f char(18) not null,
        contato varchar(45),
        constraint unique_fornecedor unique(cnjp_f)
);   
	-- criar tabela vendedor
  create table vendedor(
		idterceiro int auto_increment primary key,
        socialname varchar(255) not null,
        cnjp_v char(18),
        cpf_v char(14),
        nomefantasia varchar(255),
        contato varchar(45),
        vlocation varchar(255) not null,
        constraint unique_CNPJ_vendedor unique (cnjp_v),
        constraint unique_CPF_vendedor unique (cpf_v)
);      
  
  create table Produto_vendedor(
		Produto_idProduto int,
        Terceiro_idTerceiro int,
		quantidade int default 1,
        primary key(Produto_idProduto,Terceiro_idTerceiro),
        constraint fk_vendedor foreign key (Produto_idProduto) references vendedor(idterceiro),
        constraint fk_produto foreign key (Terceiro_idTerceiro) references produto(idproduto)
);     


  create table Produto_pedido(
		Pedido_idPedido int,
        Produto_idProduto int,
		quantidade int default 1,
        ppstatus enum ('disponivel','sem estoque') default 'disponivel',
        primary key(Pedido_idPedido,Produto_idProduto),
        constraint fk_ppedido foreign key (Pedido_idPedido) references pedido(idpedido),
        constraint fk_pproduto foreign key (Produto_idProduto) references produto(idproduto)
);     

  create table Produto_estoque(
		Produto_idProdutoe int,
        Estoque_idEst int,
		elocation VARCHAR(255)NOT NULL,
        primary key(Produto_idProdutoe, Estoque_idEst),
        constraint fk_pe_produto foreign key (Produto_idProdutoe) references produto(idproduto),
        constraint fk_pe_estoque foreign key (Estoque_idEst) references estoque(idestoque)
        
);  


 create table productsupplier(
		Fornecedor_idFornecedor int,
        Produto_idProduto int,
		quantidade int not null	,
        primary key(Fornecedor_idFornecedor, Produto_idProduto),
        constraint fk_supplier_supplier foreign key (Fornecedor_idFornecedor) references fornecedor(idfornecedor),
        constraint fk_produto_supplier foreign key (Produto_idProduto) references produto(idproduto)
 );  
 
 
