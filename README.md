OpticaJoesva - Arquitectura de Clases

Este repositorio contiene la arquitectura de clases del sistema de gestión para la óptica "OpticaJoesva", diseñada con un enfoque en la separación de responsabilidades a través de capas (Modelo, DAO, Controlador) y la implementación de patrones de diseño clave para mejorar la mantenibilidad, escalabilidad y claridad del código.

1. Arquitectura de Capas

El diseño sigue un enfoque de arquitectura de tres capas, comúnmente utilizada en aplicaciones empresariales basadas en el patrón MVC (Modelo-Vista-Controlador).

1.1. Capa del Modelo (com.optica.modelo)

Contiene todas las entidades de negocio del sistema, sus atributos y la lógica específica del dominio.

Entidades Principales: Usuario, Rol, Permiso, Cliente, Producto, Recibo.

Lógica de Negocio: Se observa en métodos como Usuario.checkPassword(), Cliente.calcularEdad(), y Recibo.calcularSaldoPendiente().

Lookups/Catálogos: Incluye clases para manejar datos de referencia como FormaPago, TipoProducto, MaterialLente, etc.

1.2. Capa de Acceso a Datos (DAO - com.optica.dao)

Esta capa es responsable de la persistencia y la recuperación de datos desde la base de datos (presumiblemente MySQL, dada la clase ConexionMySQL).

Patrón DAO: Define la interfaz genérica IDAO<T> con operaciones CRUD (obtenerPorId, obtenerTodos, insertar, actualizar, eliminar), implementada por clases específicas como UsuarioDAOImpl, ClienteDAOImpl, etc.

1.3. Capa de Controladores (com.optica.controlador)

Actúa como la capa de presentación y lógica de control (Servlets en este caso), manejando las peticiones del usuario (HTTP requests) y coordinando la interacción entre la Vista (JSP/HTML) y el Modelo/DAO.

Controladores: LoginServlet, UsuarioServlet, ClienteServlet.

Utilizan las implementaciones DAO obtenidas a través del DAOFactory.

2. Patrones de Diseño Implementados

Se han aplicado varios patrones de diseño para estructurar componentes específicos:

Patrón

Clase/Componente

Propósito

Singleton

ConexionMySQL

Asegura que solo exista una única instancia de la clase de conexión a la base de datos en toda la aplicación, gestionando eficientemente los recursos de conexión.

Factory Method

DAOFactory

Centraliza la lógica de creación de las implementaciones DAO (UsuarioDAOImpl, ClienteDAOImpl, etc.), desacoplando la capa de controladores de las implementaciones concretas.

Builder

ProductoBuilder

Simplifica la construcción de objetos complejos (Producto) paso a paso, especialmente útil si el objeto tiene muchos atributos opcionales.

Facade

OperacionesVentaFacade

Proporciona una interfaz simple y unificada para subsistemas complejos (como el proceso de una venta), encapsulando interacciones con múltiples DAOs (Recibo, DetalleRecibo, Producto).

3. Visualización del Diagrama

El diagrama de clases que describe esta arquitectura fue generado utilizando el lenguaje PlantUML.

Para visualizar o renderizar el archivo .puml que contiene el código de la arquitectura, se requiere el motor de renderizado Graphviz. La mayoría de las herramientas y extensiones de PlantUML utilizan Graphviz internamente.

Diagrama generado con PlantUML y renderizado usando Graphviz.
