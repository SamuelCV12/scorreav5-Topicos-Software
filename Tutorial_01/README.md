# Tutorial 05: Laravel, MySQL y phpMyAdmin con Docker en AWS

**Estudiante**: Samuel Correa  
**Identificador**: samuel-correa  

## 📋 Descripción del Proyecto

Despliegue completo de una aplicación Laravel con MySQL y phpMyAdmin utilizando Docker Compose en una instancia AWS EC2 con Amazon Linux 2023.

## 🏗️ Arquitectura del Despliegue

- **Laravel**: Aplicación web en puerto 8081
- **MySQL**: Base de datos en puerto 33061 (solo localhost)
- **phpMyAdmin**: Administrador web en puerto 9081
- **Red Docker**: `samuel-correa-net` (aislada)
- **Volúmenes**: Persistencia de datos garantizada

## 📂 Estructura de Archivos

```
Tutorial_01/example-app/
├── Dockerfile              # Imagen Laravel con PHP 8.4 y Apache
├── .dockerignore           # Exclusiones para el build
├── compose.infra.yaml      # MySQL y phpMyAdmin
├── compose.app.yaml        # Aplicación Laravel
├── evidencias/             # Screenshots del despliegue
└── README.md              # Esta documentación
```

## 🚀 Configuración de Despliegue

### Puertos Asignados (Fila 1)
| Servicio | Puerto Interno | Puerto Host | Acceso |
|----------|----------------|-------------|---------|
| Laravel | 80 | 8081 | Público |
| phpMyAdmin | 80 | 9081 | Público |
| MySQL | 3306 | 33061 | Solo localhost |

### Variables de Entorno (.env)
```bash
STUDENT_ID=samuel-correa
APP_IMAGE=laravel-samuel-correa:1.0
APP_PORT=8081
PMA_PORT=9081
MYSQL_PORT=33061
APP_URL=http://100.27.190.73:8081
DB_DATABASE=samuelcorrea
DB_USERNAME=samuelcorrea
```

## 🌐 URLs de Acceso

- **Laravel**: http://100.27.190.73:8081
- **phpMyAdmin**: http://100.27.190.73:9081

### Rutas de Prueba
- `/` - Página principal
- `/products` - Lista de productos  
- `/products/create` - Crear producto
- `/api/products` - API JSON v1
- `/api/v2/products` - API JSON v2
- `/api/v3/products` - API JSON v3

## 📊 Evidencias del Despliegue

### 1. 🌐 Aplicaciones Web Funcionando

#### Laravel Ejecutándose
![Laravel Home](https://github.com/user-attachments/assets/3630cb96-f3e9-47e9-bfc1-ee23a1a05c5c
)
*Laravel funcionando correctamente en el puerto 8081*

#### phpMyAdmin Accesible
![phpMyAdmin Login](https://github.com/user-attachments/assets/c522b54a-f9a0-4102-9c59-a8d6b344ddf2
)
*phpMyAdmin accesible en el puerto 9081*

#### Funcionalidades Laravel
![Productos Laravel](https://github.com/user-attachments/assets/69f2f895-30e9-497a-a2f7-be8415b3588d
)
*Lista de productos en Laravel*

![API JSON](https://github.com/user-attachments/assets/b37ddbb2-6bc4-4179-93f3-a62e7285bdc5
)
*API REST funcionando correctamente*

### 2. 💾 Base de Datos y Usuario MySQL

#### Base de Datos Creada
![Base de Datos](evidencias/05-mysql-database.png)
*Base de datos `samuelcorrea` creada correctamente*

#### Tablas Generadas por Migraciones
![Tablas MySQL](evidencias/06-mysql-tables.png)
*6 tablas creadas automáticamente por Laravel*

#### Usuario MySQL Configurado
![Usuario MySQL](https://github.com/user-attachments/assets/01e72f32-a789-4279-a2b8-66d1ff0d9750
)
*Usuario `samuelcorrea` con permisos correctos*

#### Datos Almacenados
![Datos Productos](evidencias/08-mysql-data.png)
*Datos guardados correctamente en la base*

### 3. 🔄 Persistencia de Datos

#### Comandos de Reinicio
![Terminal Down](evidencias/09-docker-down.png)
*Deteniendo contenedores para probar persistencia*

![Terminal Up](evidencias/10-docker-up.png)
*Reiniciando contenedores*

#### Verificación Post-Reinicio
![Laravel Post-Restart](evidencias/11-laravel-after-restart.png)
*Laravel funcionando después del reinicio*

![Datos Persistentes](evidencias/12-data-persistent.png)
*Los datos siguen existiendo en MySQL*

