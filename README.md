# Reto_2

Desarrolle la mayoría de ejercicios en clase. Para cada punto cree un programa individual. Al finalizar suba todo a un repo y súbalo al canal reto_2 en slack.

Elija un problema de la vida real (sistema de gestión de biblioteca, negocio de compra-venta, automóvil, etc) que se pueda modelar a través de objetos y clases. Plantee las relaciones de clases, composiciones, propiedades y comportamientos del sistema en uno mas diagramas tipo UML.

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
        + consultarHistorial()
    }

    class Lector {
        - List<Multa> multas
        + reservarLibro(Libro libro)
        + pagarMulta(Multa multa)
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
        + calcularMulta()
    }

    class Reserva {
        - Libro libro
        - Lector lector
        - Date fechaReserva
    }

    class Multa {
        - double monto
        - String motivo
        - boolean pagada
    }

    Biblioteca --> Libro : contiene >
    Biblioteca --> Bibliotecario : contiene >
    Biblioteca --> Usuario : registra >
    Bibliotecario --> Prestamo : administra >
    Libro --> Reserva : puede tener >
    Usuario <|-- Lector : hereda >
    Usuario <|-- Bibliotecario : hereda >
    Prestamo --> Libro : incluye >
    Prestamo --> Lector : pertenece a >
    Lector --> Multa : puede tener >
