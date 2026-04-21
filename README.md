# biblioteca_digital
Repositorio de trabajo colaborativo :thumbsup:


--
-- Base de datos: `biblioteca_digital`
--

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `categorias`
--

DROP TABLE IF EXISTS `categorias`;
CREATE TABLE IF NOT EXISTS `categorias` (
  `id_categoria` int NOT NULL AUTO_INCREMENT,
  `nombre_categoria` varchar(200) COLLATE utf8mb4_spanish2_ci NOT NULL,
  PRIMARY KEY (`id_categoria`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_spanish2_ci;

--
-- Volcado de datos para la tabla `categorias`
--

INSERT INTO `categorias` (`id_categoria`, `nombre_categoria`) VALUES
(1, 'Novela'),
(2, 'Ciencia Ficción'),
(3, 'Historia'),
(4, 'Tecnología'),
(5, 'Educación');

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `libros`
--

DROP TABLE IF EXISTS `libros`;
CREATE TABLE IF NOT EXISTS `libros` (
  `id_libro` int NOT NULL AUTO_INCREMENT,
  `titulo` varchar(100) COLLATE utf8mb4_spanish2_ci NOT NULL,
  `autor` varchar(200) COLLATE utf8mb4_spanish2_ci NOT NULL,
  `id_categoria` int NOT NULL,
  `ano_publicacion` date NOT NULL,
  `isbn` int NOT NULL,
  PRIMARY KEY (`id_libro`),
  KEY `id_categoria` (`id_categoria`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_spanish2_ci;

--
-- Volcado de datos para la tabla `libros`
--

INSERT INTO `libros` (`id_libro`, `titulo`, `autor`, `id_categoria`, `ano_publicacion`, `isbn`) VALUES
(1, 'Cien Años de Soledad', 'Gabriel García Márquez', 1, '1967-05-30', 100001),
(2, 'Dune', 'Frank Herbert', 2, '1965-08-01', 100002),
(3, 'Breve Historia del Tiempo', 'Stephen Hawking', 3, '1988-04-01', 100003),
(4, 'Fundamentos de Bases de Datos', 'Elmasri y Navathe', 4, '2016-01-15', 100004),
(5, 'Aprendiendo SQL', 'Alan Beaulieu', 5, '2020-03-10', 100005);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `prestamos`
--

DROP TABLE IF EXISTS `prestamos`;
CREATE TABLE IF NOT EXISTS `prestamos` (
  `id_prestamo` int NOT NULL AUTO_INCREMENT,
  `id_usuario` int NOT NULL,
  `id_libro` int NOT NULL,
  `fecha_prestamo` date NOT NULL,
  `fecha_devolucion` date DEFAULT NULL,
  PRIMARY KEY (`id_prestamo`),
  KEY `id_usuario` (`id_usuario`),
  KEY `id_libro` (`id_libro`)
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_spanish2_ci;

--
-- Volcado de datos para la tabla `prestamos`
--

INSERT INTO `prestamos` (`id_prestamo`, `id_usuario`, `id_libro`, `fecha_prestamo`, `fecha_devolucion`) VALUES
(1, 1, 1, '2026-04-01', '2026-04-01'),
(2, 2, 2, '2026-04-02', '2026-04-02'),
(3, 3, 3, '2026-04-03', NULL),
(4, 4, 4, '2026-04-05', '2026-04-05'),
(5, 5, 5, '2026-04-06', NULL),
(6, 1, 3, '2026-04-07', '0000-00-00'),
(7, 2, 1, '2026-04-08', NULL);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `usuarios`
--

DROP TABLE IF EXISTS `usuarios`;
CREATE TABLE IF NOT EXISTS `usuarios` (
  `id_usuario` int NOT NULL AUTO_INCREMENT,
  `nombre` varchar(100) COLLATE utf8mb4_spanish2_ci NOT NULL,
  `correo` varchar(200) COLLATE utf8mb4_spanish2_ci NOT NULL,
  `fecha_registro` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id_usuario`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_spanish2_ci;

--
-- Volcado de datos para la tabla `usuarios`
--

INSERT INTO `usuarios` (`id_usuario`, `nombre`, `correo`, `fecha_registro`) VALUES
(1, 'Ana Pérez', 'ana.perez@correo.com', '2026-04-21 14:47:32'),
(2, 'Luis González', 'luis.gonzalez@correo.com', '2026-04-21 14:47:32'),
(3, 'María Torres', 'maria.torres@correo.com', '2026-04-21 14:47:32'),
(4, 'Carlos Rojas', 'carlos.rojas@correo.com', '2026-04-21 14:47:32'),
(5, 'Sofía Muñoz', 'sofia.munoz@correo.com', '2026-04-21 14:47:32');

--
-- Restricciones para tablas volcadas
--

--
-- Filtros para la tabla `libros`
--
ALTER TABLE `libros`
  ADD CONSTRAINT `libros_ibfk_1` FOREIGN KEY (`id_categoria`) REFERENCES `categorias` (`id_categoria`);

--
-- Filtros para la tabla `prestamos`
--
ALTER TABLE `prestamos`
  ADD CONSTRAINT `prestamos_ibfk_1` FOREIGN KEY (`id_usuario`) REFERENCES `usuarios` (`id_usuario`),
  ADD CONSTRAINT `prestamos_ibfk_2` FOREIGN KEY (`id_libro`) REFERENCES `libros` (`id_libro`);
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
