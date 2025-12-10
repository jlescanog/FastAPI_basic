# Posts API - FastAPI

Una API REST moderna y escalable construida con **FastAPI** para gestionar posts. Este proyecto demuestra conceptos clave de desarrollo de APIs en Python incluyendo modelos de datos con validación, operaciones CRUD, manejo de errores HTTP y documentación automática.

## 🎯 Propósito del Proyecto

Este proyecto es una aplicación educativa que implementa un servidor de API REST completo utilizando FastAPI. Permite gestionar una colección de posts con las siguientes funcionalidades:

- **Crear posts** con información del autor, contenido y timestamps
- **Listar todos los posts** disponibles
- **Obtener un post específico** por su ID
- **Actualizar posts** existentes
- **Eliminar posts** de la colección

El proyecto demuestra mejores prácticas en desarrollo de APIs incluyendo validación de datos, manejo de excepciones HTTP, estructuración de código y documentación automática interactiva.

## 🚀 Características Principales

- **FastAPI**: Framework moderno y de alto rendimiento para construir APIs REST
- **Validación de datos**: Uso de Pydantic para validación automática de esquemas
- **Documentación automática**: Swagger UI y ReDoc integrados
- **Manejo de errores**: Excepciones HTTP bien estructuradas
- **Operaciones CRUD**: Endpoints completos para crear, leer, actualizar y eliminar recursos
- **UUIDs únicos**: Identificadores únicos para cada post

## 🛠️ Tecnologías Utilizadas

- **Python 3.8+**
- **FastAPI 0.115.12**: Framework web de alto rendimiento
- **Uvicorn 0.34.0**: Servidor ASGI
- **Pydantic 2.11.1**: Validación de datos y serialización

## 📋 Requisitos Previos

- Python 3.8 o superior
- pip (gestor de paquetes de Python)
- Git (opcional, para clonar el repositorio)

## 💻 Instalación

### En Windows, Linux o macOS

#### 1. Clonar el repositorio
```bash
git clone https://github.com/jlescanog/class_fastapi.git
cd class_fastapi
```

#### 2. Crear un entorno virtual (recomendado)

**En Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**En Linux/macOS:**
```bash
python3 -m venv venv
source venv/bin/activate
```

#### 3. Instalar dependencias
```bash
pip install -r requirements.txt
```

## ▶️ Ejecutar la Aplicación

Con el entorno virtual activado, ejecuta:

```bash
uvicorn main:app --reload
```

**Opciones útiles:**
- `--reload`: Reinicia el servidor automáticamente al detectar cambios en el código
- `--host 0.0.0.0`: Permite acceso desde otras máquinas en la red
- `--port 8000`: Especifica el puerto (por defecto es 8000)

**Ejemplo con opciones personalizadas:**
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

## 📚 Documentación Interactiva

Una vez que el servidor esté corriendo, accede a:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

Aquí puedes visualizar, documentar y probar todos los endpoints de la API de forma interactiva.

## 🔌 Endpoints Disponibles

### GET `/`
Retorna un mensaje de bienvenida.

```bash
curl http://localhost:8000/
```

### GET `/posts`
Obtiene la lista completa de todos los posts.

```bash
curl http://localhost:8000/posts
```

**Respuesta:**
```json
[
  {
    "id": "uuid-string",
    "title": "Mi Primer Post",
    "author": "Juan",
    "content": "Contenido del post",
    "created_at": "2025-12-10T10:30:00",
    "published_at": null,
    "published": false
  }
]
```

### POST `/posts/create`
Crea un nuevo post.

```bash
curl -X POST http://localhost:8000/posts/create \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Mi Nuevo Post",
    "author": "Juan Pérez",
    "content": "Este es el contenido de mi primer post",
    "published": true
  }'
```

**Body esperado:**
```json
{
  "title": "string",
  "author": "string",
  "content": "string",
  "published": false,
  "published_at": null
}
```

### GET `/posts/{post_id}`
Obtiene un post específico por su ID.

```bash
curl http://localhost:8000/posts/550e8400-e29b-41d4-a716-446655440000
```

### PUT `/posts/update/{post_id}`
Actualiza un post existente.

```bash
curl -X PUT http://localhost:8000/posts/update/550e8400-e29b-41d4-a716-446655440000 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Post Actualizado",
    "author": "Juan Pérez",
    "content": "Contenido actualizado"
  }'
```

### DELETE `/posts/delete/{post_id}`
Elimina un post.

```bash
curl -X DELETE http://localhost:8000/posts/delete/550e8400-e29b-41d4-a716-446655440000
```

## 📦 Estructura del Proyecto

```
class_fastapi/
├── main.py           # Archivo principal con la aplicación FastAPI
├── requirements.txt  # Dependencias del proyecto
├── README.md        # Este archivo
└── __pycache__/     # Cache de Python (se genera automáticamente)
```

## 🔍 Conceptos Demonstrados

Este proyecto implementa conceptos fundamentales de desarrollo de APIs:

### 1. **Modelos Pydantic**
```python
class Post(BaseModel):
    id: str
    title: str
    author: str
    content: Text
    created_at: datetime
    published_at: Optional[datetime]
    published: bool = False
```

### 2. **Validación Automática**
Pydantic valida automáticamente los tipos de datos y los requisitos de entrada.

### 3. **Operaciones CRUD**
- **C**reate: POST `/posts/create`
- **R**ead: GET `/posts` y GET `/posts/{post_id}`
- **U**pdate: PUT `/posts/update/{post_id}`
- **D**elete: DELETE `/posts/delete/{post_id}`

### 4. **Manejo de Errores HTTP**
```python
raise HTTPException(status_code=404, detail='Post no encontrado')
```

### 5. **Identificadores Únicos (UUIDs)**
Cada post recibe un identificador único generado automáticamente.

## 🧪 Pruebas Manuales

### Con curl:

**Crear un post:**
```bash
curl -X POST http://localhost:8000/posts/create \
  -H "Content-Type: application/json" \
  -d '{"title":"Test","author":"Usuario","content":"Contenido","published":false}'
```

**Listar posts:**
```bash
curl http://localhost:8000/posts
```

**Obtener un post específico:**
```bash
curl http://localhost:8000/posts/YOUR_POST_ID
```

**Actualizar un post:**
```bash
curl -X PUT http://localhost:8000/posts/update/YOUR_POST_ID \
  -H "Content-Type: application/json" \
  -d '{"title":"Actualizado","author":"Usuario","content":"Nuevo contenido"}'
```

**Eliminar un post:**
```bash
curl -X DELETE http://localhost:8000/posts/delete/YOUR_POST_ID
```

## 📝 Mejoras Futuras

Las siguientes mejoras podrían agregarse al proyecto:

- Base de datos persistente (SQLAlchemy, PostgreSQL)
- Autenticación y autorización (JWT)
- Rate limiting para limitar peticiones
- Búsqueda y filtrado avanzados
- Paginación de resultados
- Logging y monitoreo
- Tests unitarios e integración
- Docker para containerización
- Validaciones adicionales y reglas de negocio

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Para cambios importantes:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está disponible bajo la licencia MIT. Ver el archivo LICENSE para más detalles.

## 👨‍💻 Autor

**jlescanog** - [GitHub](https://github.com/jlescanog)

## 📞 Soporte

Si tienes preguntas o encuentras problemas, abre un issue en el repositorio de GitHub.

---

**Última actualización:** 10 de diciembre de 2025
