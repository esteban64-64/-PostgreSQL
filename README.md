# Bases de Datos Relacionales en PostgreSQL
## Índice
1.	Introducción al modelo relacional
2.	Relaciones: tablas, atributos, dominios y tuplas
3.	Claves primarias y foráneas
4.	Índices en PostgreSQL
5.	Integridad referencial
6.	Cascadas (ON DELETE / ON UPDATE)
7.	Ejemplos prácticos
8.	Buenas prácticas y lectura recomendada
   
## 1. Introducción al modelo relacional

Una base de datos relacional organiza la información en tablas (relations), donde los datos se representan en filas (tuplas) y columnas (atributos).
 Este modelo busca garantizar la consistencia, coherencia y eficiencia en la gestión de datos.
Palabras clave:

●	Relation → Relación / Tabla

●	Tuple → Tupla / Fila

●	Attribute → Atributo / Columna

●	Domain → Dominio / Conjunto de valores válidos

## 2. Relaciones: Tablas, atributos, dominios y tuplas

●	Tabla (Relation): conjunto de datos organizados en filas y columnas.

●	Atributo (Attribute): columna que describe una propiedad del dato.

●	Dominio (Domain): valores permitidos para un atributo (ejemplo: edades ≥ 0).

●	Tupla (Tuple): fila o registro dentro de una tabla.

Ejemplo SQL:

    CREATE TABLE Estudiantes (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(50),
    edad INT CHECK (edad >= 0)
    );

## 3. Claves primarias y foráneas
●	Clave primaria (Primary Key): identificador único de cada registro.

●	Clave foránea (Foreign Key): conecta una tabla con otra, garantizando relaciones correctas.

  
  Ejemplo SQL:

    CREATE TABLE Cursos (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(50)
    );
  

     CREATE TABLE Inscripciones (
      id SERIAL PRIMARY KEY,
      estudiante_id INT REFERENCES Estudiantes(id),
      curso_id INT REFERENCES Cursos(id)
    );


Buenas prácticas:

 ✔ Usar claves cortas y numéricas.
 
 ✔ Evitar valores nulos en claves primarias.

 ## 4. indices en PostgreSQL
 Los índices (Indexes) aceleran la búsqueda de información.
 
●	B-tree Index: el más común, eficiente en búsquedas por rangos.

●	Hash Index: útil en comparaciones de igualdad, menos versátil.

ejemplo SQL:

        CREATE INDEX idx_nombre_estudiante
        ON Estudiantes(nombre);
      
Ventajas:

 ✔ Mejoran la velocidad de consultas.
 
 ✔ Reducen el tiempo de búsqueda en grandes volúmenes de datos.
 
Desventajas:

  Ocupan espacio adicional.
 
  Pueden ralentizar inserciones o actualizaciones.
 

## 5. Integridad referencial

Es la garantía de que las relaciones entre tablas se mantengan consistentes.

Se logra con restricciones de claves foráneas y reglas de actualización/eliminación.

## 6. Cascadas (ON DELETE / ON UPDATE)

Una cascada define qué sucede cuando se actualiza o elimina un registro relacionado.

●	ON DELETE CASCADE: si se elimina un registro padre, se eliminan sus hijos.

●	ON UPDATE CASCADE: si se actualiza la clave primaria, se actualiza en las tablas hijas.

●	SET NULL: los registros hijos quedan con valor NULL.

●	SET DEFAULT: se asigna un valor por defecto.

●	NO ACTION / RESTRICT: no permite la acción si hay dependencias.

Ejemplo SQL:
    CREATE TABLE Inscripciones (
    id SERIAL PRIMARY KEY,
    estudiante_id INT REFERENCES Estudiantes(id) ON DELETE CASCADE
    );

## 7. Ejemplos prácticos
Insertar registros:
    INSERT INTO Estudiantes (nombre, edad) VALUES ('Ana', 20);
    INSERT INTO Cursos (nombre) VALUES ('Bases de Datos');

Eliminar con cascada:
    DELETE FROM Estudiantes WHERE id = 1;
-- Esto eliminará también sus inscripciones (ON DELETE CASCADE)

## 8. Buenas prácticas y lectura recomendada

●	Usar claves primarias simples y consistentes.

●	Crear índices solo cuando realmente se necesiten.

●	Definir restricciones claras para mantener integridad.

●	Documentarse en:

●	Documentación oficial PostgreSQL - SQL Tutorial

●	PostgreSQL - Índices





