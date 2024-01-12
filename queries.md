use ecommerce;

-- Selecionar todos os vendedores <br /> 
SELECT * FROM vendedor; <br /> 

-- Selecionar todos os clientes e pedidos relacionados <br /> 
SELECT * FROM cliente c, pedido p <br /> 
WHERE c.idcliente = p.idpedidocliente; <br /> 

-- Selecionar nome, último nome e ID do pedido para clientes <br /> 
SELECT c.nome, c.lastnome, p.idpedido <br /> 
FROM cliente c <br /> 
INNER JOIN pedido p ON c.idcliente = p.idpedidocliente; <br /> 

-- Selecionar todos os clientes e pedidos com informações de produtos <br /> 
SELECT * <br /> 
FROM cliente <br /> 
INNER JOIN pedido ON cliente.idcliente = pedido.idpedidocliente <br /> 
INNER JOIN produto ON pedido.idpedido = produto.idproduto; <br /> 

-- Verificar se algum vendedor também é fornecedor <br /> 
SELECT v.idterceiro, v.socialname AS nome_vendedor, v.nomefantasia AS nome_fantasia_vendedor, f.socialname AS nome_fornecedor <br /> 
FROM vendedor v <br /> 
LEFT JOIN fornecedor f ON v.idterceiro = f.idfornecedor; <br /> 

-- Relação de produtos, fornecedores e estoques <br /> 
SELECT p.descrição AS nome_produto, f.socialname AS nome_fornecedor, e.location AS local_estoque <br /> 
FROM produto p <br /> 
INNER JOIN productsupplier ps ON p.idproduto = ps.Produto_idProduto <br /> 
INNER JOIN fornecedor f ON ps.Fornecedor_idFornecedor = f.idfornecedor <br /> 
INNER JOIN produto_estoque pe ON p.idproduto = pe.Produto_idProdutoe <br /> 
INNER JOIN estoque e ON pe.Estoque_idEst = e.idestoque; <br /> 

-- Relação de nomes dos fornecedores e nomes dos produtos <br /> 
SELECT f.socialname AS nome_fornecedor, p.descrição AS nome_produto <br /> 
FROM fornecedor f <br /> 
INNER JOIN productsupplier ps ON f.idfornecedor = ps.Fornecedor_idFornecedor <br /> 
INNER JOIN produto p ON ps.Produto_idProduto = p.idproduto; <br /> 


-- Contar o número de pedidos para cada cliente <br /> 
SELECT c.idcliente, COUNT(*) AS numero_de_pedidos <br /> 
FROM cliente c <br /> 
INNER JOIN pedido o ON c.idcliente = o.idpedidocliente <br /> 
INNER JOIN produto_pedido p ON p.Pedido_idPedido = o.idpedido <br /> 
GROUP BY c.idcliente; <br /> 

