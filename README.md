# 📚 Base de Datos: biblioteca_digital

## 🗂️ Estructura y Datos

### 📁 Tabla: categorias
```sql
DROP TABLE IF EXISTS categorias;

CREATE TABLE IF NOT EXISTS categorias (
    id_categoria INT NOT NULL AUTO_INCREMENT,
    nombre_categoria VARCHAR(200) COLLATE utf8mb4_spanish2_ci NOT NULL,
    PRIMARY KEY (id_categoria)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO categorias (id_categoria, nombre_categoria) VALUES
(1, 'Novela'),
(2, 'Ciencia Ficción'),
(3, 'Historia'),
(4, 'Tecnología'),
(5, 'Educación');
📚 Tabla: libros
DROP TABLE IF EXISTS libros;

CREATE TABLE IF NOT EXISTS libros (
    id_libro INT NOT NULL AUTO_INCREMENT,
    titulo VARCHAR(100) NOT NULL,
    autor VARCHAR(200) NOT NULL,
    id_categoria INT NOT NULL,
    ano_publicacion DATE NOT NULL,
    isbn INT NOT NULL,
    PRIMARY KEY (id_libro),
    KEY id_categoria (id_categoria)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO libros VALUES
(1, 'Cien Años de Soledad', 'Gabriel García Márquez', 1, '1967-05-30', 100001),
(2, 'Dune', 'Frank Herbert', 2, '1965-08-01', 100002),
(3, 'Breve Historia del Tiempo', 'Stephen Hawking', 3, '1988-04-01', 100003),
(4, 'Fundamentos de Bases de Datos', 'Elmasri y Navathe', 4, '2016-01-15', 100004),
(5, 'Aprendiendo SQL', 'Alan Beaulieu', 5, '2020-03-10', 100005);
🔄 Tabla: prestamos
DROP TABLE IF EXISTS prestamos;

CREATE TABLE IF NOT EXISTS prestamos (
    id_prestamo INT NOT NULL AUTO_INCREMENT,
    id_usuario INT NOT NULL,
    id_libro INT NOT NULL,
    fecha_prestamo DATE NOT NULL,
    fecha_devolucion DATE DEFAULT NULL,
    PRIMARY KEY (id_prestamo),
    KEY id_usuario (id_usuario),
    KEY id_libro (id_libro)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO prestamos VALUES
(1, 1, 1, '2026-04-01', '2026-04-01'),
(2, 2, 2, '2026-04-02', '2026-04-02'),
(3, 3, 3, '2026-04-03', NULL),
(4, 4, 4, '2026-04-05', '2026-04-05'),
(5, 5, 5, '2026-04-06', NULL),
(6, 1, 3, '2026-04-07', '0000-00-00'),
(7, 2, 1, '2026-04-08', NULL);
👤 Tabla: usuarios
DROP TABLE IF EXISTS usuarios;

CREATE TABLE IF NOT EXISTS usuarios (
    id_usuario INT NOT NULL AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    correo VARCHAR(200) NOT NULL,
    fecha_registro TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id_usuario)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO usuarios VALUES
(1, 'Ana Pérez', 'ana.perez@correo.com', '2026-04-21 14:47:32'),
(2, 'Luis González', 'luis.gonzalez@correo.com', '2026-04-21 14:47:32'),
(3, 'María Torres', 'maria.torres@correo.com', '2026-04-21 14:47:32'),
(4, 'Carlos Rojas', 'carlos.rojas@correo.com', '2026-04-21 14:47:32'),
(5, 'Sofía Muñoz', 'sofia.munoz@correo.com', '2026-04-21 14:47:32');
🔗 Relaciones (Claves Foráneas)
ALTER TABLE libros
ADD CONSTRAINT fk_libros_categoria
FOREIGN KEY (id_categoria) REFERENCES categorias(id_categoria);

ALTER TABLE prestamos
ADD CONSTRAINT fk_prestamos_usuario
FOREIGN KEY (id_usuario) REFERENCES usuarios(id_usuario),
ADD CONSTRAINT fk_prestamos_libro
FOREIGN KEY (id_libro) REFERENCES libros(id_libro);
✅ Notas
Base de datos relacional en MySQL
Motor: InnoDB
Soporte de claves foráneas
Codificación: utf8mb4
