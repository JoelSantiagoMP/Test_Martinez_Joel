# Test_Martinez_Joel

# DOCUMENTACION DE LA ESTRUCTURA DE BASE DE DATOS DE LA LIBRERÍA MUNDO DE SOFIA

## Justificación del diseño:

## Tabla Autores:

#### Autores presenta los campos id_autor, que es la llave primaria autoincremental identificadora del autor, presenta su nombre con una longitud de varchar de 100 para poder ingresar nombres largos en caso de que los tenga, lo mismo con apellido1 y apellido2. Apellido2 a diferencia de nombre y apellido1 es posible que sea null, ya que consideré que no era vital conocer el segundo apellido del autor.
#### Presenta su fecha de nacimiento(fecha_naci) en formato DATE, que permitirá almacenar la fecha exacta, y su nacionalidad es un varchar(50) por si tiene mas de 1 nacionalidad.

## Tabla Clientes:

#### Clientes presenta un campo id_cliente que es llave primaria autoincremental y su propósito es ser el identificador principal de cada cliente, ya que no vi conveniente solicitar la cédula porque en los requerimientos no se solicitaba este dato. También presenta su nombre varchar(100), para que pueda escribirlo, pensé que con un único campo de nombre podría bastar, tiene una longitud que cubriría una gran mayoría de nombres completos del país, escogí no añadir campos de apellido porque no sueles llamar a un cliente por su nombre y apellido, con el nombre y su identificador asumí que sería suficiente. Posee su campo de e-mail not null y con característica UNIQUE, para que no se pueda repetir, también un telefono, lo hice varchar para no consumir memoria en exceso de la base de datos, y no lo puse único porque razoné de que puede ser que 2 clientes, por ejemplo un padre y su hijo, usen el mismo número telefónico para comunicación. También se solicita un dato de dirección que es varchar(100), pero este si es opcional añadirlo.

## Tabla libros:

#### Libros tiene su campo ISBN_libro, que es un varchar, ya que es un código a nivel nacional, a su vez ese ISBN es llave primaria identificadora del libro, ya que es un dato irrepetible de cada libro. Posee su título que es not null, porque es obligatorio saber como se llama el libro, datos de editorial, categoria son varchar no nulos también. Se agregó el campo fecha_publicacion, requisito solicitado por el cliente en formato DATE, el precio que es DECIMAL para llevar un valor preciso, y el stock que es un valor entero no null, en la tabla del libro ningún campo es null, ya que no debería ser posible omitir datos importantes del libro.

## Tabla Pedidos:

#### Pedidos tiene su id_pedido, llave primaria autoincremental identificadora de cada pedido, posee una cantidad, que representa la cantidad de libros que se vendieron en ese pedido, fecha compra en formatodate, estado que es un enum con 3 estados posibles y la llave foranea id_cliente que representa que cliente hizo que pedido.

## Tabla Transacciones:

#### Transacciones tiene su llave primaria id_transaccion, autoincremental que identifica cada transaccion hecha, tiene la llave foranea id_pedido, para conectar las transacciones hechas a los pedidos hechos, tiene un metodo, que representa el metodo de pago que es varchar(50) not null, monto que es el valor de transaccion, un decimal(10,2) para calculos precisos de valor de venta y por ultimo una fecha de transaccion en tipo de dato DATE.

## Tabla Libros_Pedidos:

#### Esta tabla surge por la relación que existe entre libros y pedidos, que por naturaleza es de muchos a muchos, surge como necesidad de mapear individualmente que libros salen en que pedido y vice versa, por eso posee datos id_pedido e ISBN_pedido, que ambas son llaves primarias y foraneas de sus respectivos datos de otras tablas.

## Tabla Autor_Libro:

#### Esta tabla surge por la relación que existe entre Autores y Libros, que por naturaleza es de muchos a muchos, surge como necesidad de mapear indivualmente qué autor o qué autores participaron en la escritura de qué libro, o cuáles libros pertenecen a cierto autor. Por eso posee las llaves primarias y foraneas de ISBN_libro e id_autor.


## Relaciones entre tablas

Las relaciones principales entre estas tablas son:

Autores (1:M) autor_libro / Libros (1:M) autor_libro
¿Por qué?
Esta tabla (autor_libro) surge por el rompimiento de la relacion (N:M) entre las tablas Autores y Libros.


Libros (1:M) libros_pedidos / Pedidos (1:M) libros_pedidos
¿Por qué? 
Esta tabla (libros_pedidos) surge por el rompimiento de la relación (N:M) entre las tablas Libros y Pedidos.

Clientes (1:M) Pedidos
¿Por qué?
Esta relación es indicada por este motivo lógico: un cliente puede realizar ningún o muchos pedidos, pero un pedido pertenece a un único cliente, entonces la relación resultante es la expresada.

Pedidos (1:M) Transacciones
¿Por qué?
Esta relacion puede entenderse por el siguiente motivo: Un pedido puede tener muchas transacciones, ya sea pagos por crédito a varias cuotas, u otros motivos. Pero una transacción solo puede pertenecer a un pedido en específico, por eso esta relación está indicada de este modo.
