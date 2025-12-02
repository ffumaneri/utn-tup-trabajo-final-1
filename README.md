# Trabajo Final: Sistema de Gestión de Rutinas de Gimnasio

## Programación 4 - UTN

---

## Descripción del Proyecto

Se debe desarrollar un sistema web completo para la gestión de rutinas de gimnasio que permita crear, visualizar, modificar y eliminar rutinas de entrenamiento. El sistema estará compuesto por un frontend moderno, un backend RESTful y una base de datos relacional.

---

## Objetivos de Aprendizaje

- Implementar una arquitectura cliente-servidor completa
- Desarrollar una API RESTful con FastAPI
- Utilizar ORM para el manejo de la base de datos
- Crear una interfaz de usuario reactiva con React
- Gestionar el estado de la aplicación en el frontend
- Implementar operaciones CRUD completas
- Trabajar con bases de datos relacionales (PostgreSQL)

---

## Tecnologías Requeridas

### Frontend
- **React** (con Vite como build tool, deseable)
- **Material UI** (opcional - se puede elegir otro conjunto de componentes como Ant Design, Chakra UI, etc.)
- **Axios** o **Fetch API** para comunicación con el backend

### Backend
- **Python 3.10+**
- **FastAPI** como framework web
- **SQLModel** o **SQLAlchemy** como ORM para acceso a la base de datos
- **Pydantic** para validación de datos
- **Uvicorn** como servidor ASGI

### Base de Datos
- **PostgreSQL** (obligatorio)

---

## Modelo de Datos

### Rutina
Una rutina representa un plan de entrenamiento y contiene:
- **ID**: Identificador único (generado automáticamente)
- **Nombre**: Nombre descriptivo de la rutina (requerido, único)
- **Descripción**: Descripción opcional de la rutina
- **Fecha de creación**: Timestamp de cuando fue creada
- **Ejercicios por día**: Colección de ejercicios organizados por día de la semana

### Día de la Semana
Los días válidos son:
- Lunes
- Martes
- Miércoles
- Jueves
- Viernes
- Sábado
- Domingo

**Importante**: Una rutina puede tener ejercicios para todos los días de la semana o solo para días específicos (por ejemplo, solo Martes y Jueves, o Lunes, Miércoles y Viernes).

### Ejercicio
Cada ejercicio dentro de una rutina contiene:
- **ID**: Identificador único (generado automáticamente)
- **Nombre**: Nombre del ejercicio (requerido) - por ejemplo: "Press de banca", "Sentadillas", "Dominadas"
- **Día de la semana**: Día en el que se debe realizar (requerido)
- **Series**: Número de series a realizar (requerido)
- **Repeticiones**: Número de repeticiones por serie (requerido)
- **Peso**: Peso en kilogramos (opcional) - puede ser nulo para ejercicios de peso corporal
- **Notas**: Observaciones adicionales sobre el ejercicio (opcional)
- **Orden**: Orden en que se debe realizar el ejercicio dentro del día

---

## Funcionalidades Requeridas

### 1. Alta de Rutina
- Crear una nueva rutina con nombre y descripción
- Agregar ejercicios a la rutina especificando:
  - Día de la semana
  - Nombre del ejercicio
  - Series
  - Repeticiones
  - Peso (opcional)
  - Notas (opcional)
- Validar que el nombre de la rutina sea único
- Validar que todos los campos requeridos estén completos
- Permitir agregar múltiples ejercicios en diferentes días

### 2. Baja de Rutina
- Eliminar una rutina existente del sistema
- Mostrar confirmación antes de eliminar
- Al eliminar una rutina, se deben eliminar todos sus ejercicios asociados (cascada)

### 3. Modificación de Rutina
- Editar el nombre y descripción de una rutina
- Agregar nuevos ejercicios a la rutina
- Modificar ejercicios existentes (nombre, series, repeticiones, peso, notas)
- Eliminar ejercicios de la rutina
- Cambiar el orden de los ejercicios dentro de un día
- Validar los datos antes de guardar los cambios

### 4. Búsqueda de Rutinas
- Buscar rutinas por nombre (búsqueda parcial, no case-sensitive)
- Mostrar resultados en tiempo real mientras se escribe
- Si no hay resultados, mostrar mensaje apropiado

### 5. Visualización de Rutinas
- Listar todas las rutinas existentes con información resumida
- Ver el detalle completo de una rutina específica
- Mostrar los ejercicios organizados por día de la semana
- Mostrar solo los días que tienen ejercicios asignados
- Presentar la información de forma clara y organizada

---

## Requerimientos del Backend (FastAPI)

### Endpoints de la API

Implementar los siguientes endpoints RESTful:

#### Rutinas
- `GET /api/rutinas` - Listar todas las rutinas
- `GET /api/rutinas/{id}` - Obtener detalle de una rutina específica
- `GET /api/rutinas/buscar?nombre={texto}` - Buscar rutinas por nombre
- `POST /api/rutinas` - Crear una nueva rutina
- `PUT /api/rutinas/{id}` - Actualizar una rutina existente
- `DELETE /api/rutinas/{id}` - Eliminar una rutina

#### Ejercicios (opcional, si se desea gestionar de forma independiente)
- `POST /api/rutinas/{id}/ejercicios` - Agregar ejercicio a una rutina
- `PUT /api/ejercicios/{id}` - Actualizar un ejercicio
- `DELETE /api/ejercicios/{id}` - Eliminar un ejercicio

### Validaciones del Backend
- Validar que los datos recibidos cumplan con el formato esperado
- Verificar que el nombre de la rutina sea único
- Validar que series y repeticiones sean números positivos
- Validar que el peso (si se proporciona) sea un número positivo
- Validar que el día de la semana sea válido
- Retornar códigos de estado HTTP apropiados (200, 201, 400, 404, 500, etc.)
- Retornar mensajes de error descriptivos

### Manejo de Errores
- Implementar manejo de excepciones apropiado
- Retornar respuestas con formato consistente
- Incluir mensajes de error claros para el usuario

---

## Requerimientos del Frontend (React + Vite)

### Componentes Principales Sugeridos

- **Listado de Rutinas**: Pantalla principal con todas las rutinas
- **Formulario de Creación**: Para dar de alta una nueva rutina
- **Formulario de Edición**: Para modificar una rutina existente
- **Vista de Detalle**: Para visualizar una rutina completa
- **Barra de Búsqueda**: Para filtrar rutinas por nombre
- **Componente de Ejercicio**: Para mostrar/editar ejercicios individuales

### Características de la Interfaz

- Navegación intuitiva entre las diferentes pantallas
- Formularios con validación del lado del cliente
- Mensajes de confirmación para operaciones destructivas (eliminar)
- Feedback visual para operaciones exitosas o fallidas
- Loading states mientras se realizan peticiones al backend
- Diseño responsive (adaptable a diferentes tamaños de pantalla)
- Organización visual clara de ejercicios por día de la semana

### Gestión del Estado
- Implementar gestión de estado apropiada (puede ser con useState, useContext, etc.)
- Manejar el estado de loading y errores
- Actualizar la interfaz después de cada operación CRUD

---

## Documentación Requerida

### README.md del Backend

El README del backend **debe incluir obligatoriamente**:

1. **Descripción del proyecto**: Breve descripción de la API

2. **Requisitos previos**:
   - Versión de Python requerida
   - PostgreSQL instalado

3. **Instalación**:
   - Comandos para crear un entorno virtual
   - Comando para instalar dependencias desde requirements.txt

4. **Configuración de la Base de Datos**:
   - **String de conexión a PostgreSQL**: Explicar claramente cómo configurarlo
   - Formato del string de conexión
   - Variables de entorno necesarias
   - Ejemplo de archivo `.env` o configuración
   - Instrucciones para crear la base de datos
   - Instrucciones para ejecutar migraciones (si aplica)

5. **Ejecución**:
   - Comando para iniciar el servidor
   - Puerto en el que corre la aplicación
   - URL para acceder a la documentación automática de FastAPI (Swagger)

6. **Endpoints disponibles**: Listado de endpoints principales

7. **Estructura del proyecto**: Breve explicación de la organización de archivos

### README.md del Frontend

El README del frontend **debe incluir obligatoriamente**:

1. **Descripción del proyecto**: Breve descripción de la aplicación

2. **Requisitos previos**:
   - Versión de Node.js requerida
   - npm o yarn

3. **Instalación**:
   - Comando para instalar dependencias

4. **Configuración**:
   - URL del backend (variable de entorno o archivo de configuración)
   - Cómo configurar la URL de la API

5. **Ejecución**:
   - Comando para iniciar en modo desarrollo
   - Puerto en el que corre la aplicación
   - Comando para compilar para producción

6. **Tecnologías utilizadas**: Listado de las principales librerías

7. **Estructura del proyecto**: Breve explicación de la organización de componentes

---

## Criterios de Evaluación

### Funcionalidad (40%)
- Todas las operaciones CRUD funcionan correctamente
- La búsqueda funciona apropiadamente
- Validaciones del lado del servidor y cliente
- Manejo correcto de errores

### Código (30%)
- Código limpio y bien organizado
- Uso apropiado de las tecnologías requeridas
- Buenas prácticas de programación
- Separación de responsabilidades
- Comentarios donde sea necesario

### Base de Datos (15%)
- Diseño correcto del modelo de datos
- Uso apropiado de relaciones
- Integridad referencial
- Índices apropiados (si corresponde)

### Documentación (15%)
- README completos y claros
- Instrucciones fáciles de seguir
- Configuración bien explicada
- Proyecto ejecutable siguiendo los README

---

## Entregables

1. **Código fuente del Backend**:
   - Código completo y funcional
   - archivo requirements.txt con todas las dependencias
   - README.md con instrucciones completas

2. **Código fuente del Frontend**:
   - Código completo y funcional
   - package.json con todas las dependencias
   - README.md con instrucciones completas

3. **Scripts de Base de Datos** (opcional):
   - Script para crear las tablas
   - Script con datos de ejemplo (opcional)

4. **Documentación adicional** (opcional):
   - Diagrama del modelo de datos
   - Capturas de pantalla de la aplicación funcionando

---

## Consideraciones Adicionales

### Opcionales (para destacar)
- Implementar paginación en el listado de rutinas
- Agregar filtros adicionales (por día de la semana, por tipo de ejercicio)
- Implementar autenticación de usuarios
- Permitir duplicar rutinas existentes
- Agregar estadísticas (rutinas más populares, días más entrenados, etc.)
- Implementar drag & drop para reordenar ejercicios
- Agregar un calendario para planificar qué rutina hacer cada día
- Exportar rutinas en formato PDF o CSV

### Recomendaciones
- Comenzar por el backend y probar los endpoints con herramientas como Postman o la documentación automática de FastAPI
- Crear primero el modelo de datos y asegurarse de que funciona correctamente
- Implementar las funcionalidades de forma incremental (primero el listado, luego el alta, etc.)
- Probar cada funcionalidad antes de pasar a la siguiente
- Hacer commits frecuentes en Git con mensajes descriptivos
- No dejar la documentación para el final

---

## Notas Importantes

- Ambos README (frontend y backend) son **obligatorios** y parte de la evaluación
- El proyecto debe poder ejecutarse siguiendo únicamente las instrucciones de los README
- La configuración de la base de datos debe estar **claramente explicada** en el README del backend
- Se espera que el código esté limpio, organizado y siga las convenciones de cada tecnología