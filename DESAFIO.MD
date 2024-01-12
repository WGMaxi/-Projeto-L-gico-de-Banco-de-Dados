# Modelagem
![image](https://github.com/WGMaxi/-Projeto-L-gico-de-Banco-de-Dados/assets/118560480/e8de0815-35fa-4412-a70e-d553a54336cb)
## Código Modelagem
-- criação do banco de dados para o cenário de E-commmerce <br /> 
create database ecommerce; <br /> 

use ecommerce; <br /> 

	-- criar tabela cliente <br /> 
create table cliente( <br /> 
		idcliente int auto_increment primary key, <br /> 
        nome varchar(45) not null, <br /> 
        lastnome varchar(45) not null, <br /> 
        cpf char(14) not null, <br /> 
        endereço varchar(45) not null, <br /> 
        constraint unique_cpf_client unique(cpf) <br /> 
); <br /> 

alter table cliente auto_increment=1; <br /> 
    -- criar tabela produto <br /> 
create table produto( <br /> 
		idproduto int auto_increment primary key, <br /> 
        categoria enum('eletronicos','magazine','móveis') not null, <br /> 
        descrição varchar(45), <br /> 
        valor varchar(11), <br /> 
        avaliação float default 0 <br /> 
);         <br /> 
-- criar tabela tipo de pagamento <br /> 
 create table tipo_pagamento( <br /> 
		idpagamento int, <br /> 
        idpedidocliente int, <br /> 
        tipo_pagamento enum('Boleto','Cartão','Pix') not null, <br /> 
        limite float, <br /> 
        primary key (idpagamento,idpedidocliente) <br /> 
);  <br /> 

	-- criar tabela pedido <br /> 
create table pedido( <br /> 
		idpedido int auto_increment primary key, <br /> 
        idpedidocliente int, <br /> 
        pedidostatus enum('cancelado','entregue','em processamento','confirmado') not null default 'em processamento', <br /> 
        descrição varchar(255), <br /> 
        Frete float default 10, <br /> 
        idpagamento boolean default false, <br /> 
        constraint fk_tipo_pagamento_pedido foreign key (idpedidocliente) references cliente(idcliente) <br /> 
	);  <br /> 
    
	-- criar tabela estoque <br /> 
        create table estoque( <br /> 
		idestoque int auto_increment primary key, <br /> 
        location varchar(45), <br /> 
        quantidade int default 0 <br /> 
);  <br /> 
    
	-- criar tabela fornecedor <br /> 
 create table fornecedor( <br /> 
		idfornecedor int auto_increment primary key, <br /> 
        socialname varchar(255) not null, <br /> 
        cnjp_f char(18) not null, <br /> 
        contato varchar(45), <br /> 
        constraint unique_fornecedor unique(cnjp_f) <br /> 
);    <br /> 
	-- criar tabela vendedor <br /> 
  create table vendedor( <br /> 
		idterceiro int auto_increment primary key, <br /> 
        socialname varchar(255) not null, <br /> 
        cnjp_v char(18), <br /> 
        cpf_v char(14), <br /> 
        nomefantasia varchar(255), <br /> 
        contato varchar(45), <br /> 
        vlocation varchar(255) not null, <br /> 
        constraint unique_CNPJ_vendedor unique (cnjp_v), <br /> 
        constraint unique_CPF_vendedor unique (cpf_v) <br /> 
);       <br /> 
  
  create table Produto_vendedor( <br /> 
		Produto_idProduto int, <br /> 
        Terceiro_idTerceiro int, <br /> 
		quantidade int default 1, <br /> 
        primary key(Produto_idProduto,Terceiro_idTerceiro), <br /> 
        constraint fk_vendedor foreign key (Produto_idProduto) references vendedor(idterceiro), <br /> 
        constraint fk_produto foreign key (Terceiro_idTerceiro) references produto(idproduto) <br /> 
);      <br /> 


  create table Produto_pedido( <br /> 
		Pedido_idPedido int, <br /> 
        Produto_idProduto int, <br /> 
		quantidade int default 1, <br /> 
        ppstatus enum ('disponivel','sem estoque') default 'disponivel', <br /> 
        primary key(Pedido_idPedido,Produto_idProduto), <br /> 
        constraint fk_ppedido foreign key (Pedido_idPedido) references pedido(idpedido), <br /> 
        constraint fk_pproduto foreign key (Produto_idProduto) references produto(idproduto) <br /> 
);   <br />    

  create table Produto_estoque( <br /> 
		Produto_idProdutoe int, <br /> 
        Estoque_idEst int, <br /> 
		elocation VARCHAR(255)NOT NULL, <br /> 
        primary key(Produto_idProdutoe, Estoque_idEst), <br /> 
        constraint fk_pe_produto foreign key (Produto_idProdutoe) references produto(idproduto), <br /> 
        constraint fk_pe_estoque foreign key (Estoque_idEst) references estoque(idestoque) <br /> 
        
);   <br /> 


 create table productsupplier( <br /> 
		Fornecedor_idFornecedor int, <br /> 
        Produto_idProduto int, <br /> 
		quantidade int not null	, <br /> 
        primary key(Fornecedor_idFornecedor, Produto_idProduto), <br /> 
        constraint fk_supplier_supplier foreign key (Fornecedor_idFornecedor) references fornecedor(idfornecedor), <br /> 
        constraint fk_produto_supplier foreign key (Produto_idProduto) references produto(idproduto) <br /> 
 );   <br /> 
 
 
