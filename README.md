SELECT CONCAT(clientes.nombre, ' ', clientes.apellido) AS NombreCompleto, clientes.direccion, clientes.correoElectronico
FROM clientes
JOIN pedidos ON clientes.ID = pedidos.ID_cliente
WHERE pedidos.fecha >= NOW() - INTERVAL 30 DAY;
SELECT productos.nombre, SUM(ventas.cantidad) AS TotalVendido
FROM productos
JOIN ventas ON productos.ID = ventas.ID_producto
WHERE ventas.fecha >= NOW() - INTERVAL 1 MONTH
GROUP BY productos.nombre
ORDER BY TotalVendido DESC;
SELECT CONCAT(clientes.nombre, ' ', clientes.apellido) AS NombreCompleto, COUNT(pedidos.ID) AS CantidadPedidos
FROM clientes
JOIN pedidos ON clientes.ID = pedidos.ID_cliente
WHERE pedidos.fecha >= NOW() - INTERVAL 1 YEAR
GROUP BY clientes.ID
ORDER BY CantidadPedidos DESC;
UPDATE productos
SET precio = precio * 1.1
WHERE categoria = 'Camisetas';
DELETE FROM pedidos
WHERE NOT EXISTS (SELECT 1 FROM ventas WHERE ventas.ID_pedido = pedidos.ID);
CREATE VIEW vista_clientes_pedidos AS
SELECT CONCAT(clientes.nombre, ' ', clientes.apellido) AS NombreCompleto, pedidos.fecha, pedidos.total
FROM clientes
JOIN pedidos ON clientes.ID = pedidos.ID_cliente;
