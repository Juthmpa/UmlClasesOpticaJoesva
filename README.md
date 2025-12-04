# OpticaJoesva - Arquitectura de Clases

Este repositorio contiene la arquitectura de clases del sistema de gestión para la óptica **"OpticaJoesva"**, diseñada con un enfoque en la separación de responsabilidades a través de capas (Modelo, DAO, Controlador) y la implementación de patrones de diseño clave para mejorar la mantenibilidad, escalabilidad y claridad del código.

---

## Arquitectura de Capas

El diseño sigue un enfoque de arquitectura de tres capas, utilizado en aplicaciones empresariales basadas en el patrón MVC (Modelo-Vista-Controlador).

---

### **1.1. Capa del Modelo (com.optica.modelo)**

Contiene todas las entidades de negocio del sistema, sus atributos y la lógica específica del dominio.

**Entidades Principales:**  
Usuario, Rol, Permiso, Cliente, Producto, Recibo.

**Lógica de Negocio:**  
Se observa en métodos como:  
- `Usuario.checkPassword()`  
- `Cliente.calcularEdad()`  
- `Recibo.calcularSaldoPendiente()`

**Búsquedas/Catálogos:**  
Incluye clases para manejar datos de referencia como `FormaPago`, `TipoProducto`, `MaterialLente`, etc.

---

### **1.2. Capa de Acceso a Datos (DAO - com.optica.dao)**

Esta capa es responsable de la persistencia y la recuperación de datos desde la base de datos (presumiblemente MySQL, dada la clase `ConexionMySQL`).

**Patrón DAO:**  
Define la interfaz genérica `IDAO` con operaciones CRUD:  
- `obtenerPorId`  
- `obtenerTodos`  
- `insertar`  
- `actualizar`  
- `eliminar`  

Implementada por clases específicas como `UsuarioDAOImpl`, `ClienteDAOImpl`, etc.

---

### **1.3. Capa de Controladores (com.optica.controlador)**

Actúa como la capa de presentación y lógica de control (Servlets), manejando las peticiones del usuario y coordinando la interacción entre la Vista (JSP/HTML) y el Modelo/DAO.

**Controladores:**  
- `LoginServlet`  
- `UsuarioServlet`  
- `ClienteServlet`

Estos utilizan las implementaciones DAO obtenidas a través del `DAOFactory`.

---

## Patrones de Diseño Implementados

Se han aplicado varios patrones de diseño para estructurar componentes específicos:

| Patrón              | Clase/Componente         | Propósito |
|--------------------|---------------------------|-----------|
| **Semifallo**      | `ConexionMySQL`           | Asegura que solo existe una instancia de la conexión a la BD, gestionando eficientemente los recursos. |
| **Método de fábrica** | `DAOFactory`            | Centraliza la lógica de creación de las implementaciones DAO y desacopla a los controladores. |
| **Constructor (Builder)** | `ProductoBuilder`   | Facilita la creación de objetos `Producto` complejos paso a paso. |
| **Fachada**        | `OperacionesVentaFacade`  | Proporciona una interfaz simple para procesos complejos como una venta, interactuando con múltiples DAO. |

---

## Visualización del Diagrama

El diagrama de clases fue generado utilizando **PlantUML**.

Para visualizar o renderizar el archivo `.puml` que contiene la arquitectura, se requiere el motor de renderizado **Graphviz**. La mayoría de herramientas y extensiones de PlantUML lo usan internamente.

**Diagrama generado con PlantUML y renderizado usando Graphviz.**

