# Reto_2

Desarrolle la mayoría de ejercicios en clase. Para cada punto cree un programa individual. Al finalizar suba todo a un repo y súbalo al canal reto_2 en slack.

Elija un problema de la vida real (sistema de gestión de biblioteca, negocio de compra-venta, automóvil, etc) que se pueda modelar a través de objetos y clases. Plantee las relaciones de clases, composiciones, propiedades y comportamientos del sistema en uno mas diagramas tipo UML.

Para el reto decidi hacer el sistema de biblioteca 
Un Sistema de Gestión de Biblioteca va incluir las siguientes funcionalidades :

Reservas de libros : los usuarios pueden reservar libros si están prestados.
Historial de préstamos : se registra el historial de préstamos y devoluciones de cada usuario.
Multas : cálculo y gestión de multas por devoluciones tardías.

```mermaid
classDiagram
    class Biblioteca {
        - String nombre
        - String direccion
        - List<Libro> coleccionLibros
        - List<Usuario> usuarios
        - List<Prestamo> prestamos
        + agregarLibro(Libro libro)
        + registrarUsuario(Usuario usuario)  
    }

    class Libro {
        - String titulo
        - String autor
        - Categoria categoria
        - Estado estado
        + actualizarEstado(Estado nuevoEstado)
    }

    class Usuario {
        - String nombre
        - String idUsuario
        - List<Prestamo> historialPrestamos
        - List<Multa> multas
        + reservarLibro(Libro libro)
        + pagarMulta(Multa multa)
        + consultarHistorial()
    }

    class Bibliotecario {
        + registrarPrestamo(Prestamo prestamo)
        + registrarDevolucion(Prestamo prestamo)
    }

    class Prestamo {
        - String idPrestamo
        - Libro libro
        - Lector lector
        - Date fechaInicio
        - Date fechaFin
        - Estado estado
    }

    class Reserva {
        - Libro libro
        - Lector lector
        - Date fechaReserva
        + Reservar()
    }

    class Multa {
        - double monto
        - String motivo
        - boolean pagada
        + calcularMulta()
    }

    Biblioteca --> Libro : contiene >
    Biblioteca --> Bibliotecario : contiene >
    Biblioteca --> Usuario : registra >
    Bibliotecario --> Prestamo : administra >
    Libro --> Reserva : puede tener >
    Usuario <-- Bibliotecario : administra >
    Prestamo --> Libro : incluye >
    Prestamo <-- Usuario : puede >
    Usuario --> Reserva : puede >
    Usuario --> Multa : puede tener >
