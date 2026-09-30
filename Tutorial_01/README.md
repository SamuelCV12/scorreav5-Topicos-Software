# Tutorial 05: Laravel, MySQL y phpMyAdmin con Docker en AWS

**Estudiante**: Samuel Correa  
**Identificador**: samuel-correa  
**Fecha**: Septiembre 2026  

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
![Laravel Home](evidencias/01-laravel-home.png)
*Laravel funcionando correctamente en el puerto 8081*

#### phpMyAdmin Accesible
![phpMyAdmin Login](evidencias/02-phpmyadmin-login.png)
*phpMyAdmin accesible en el puerto 9081*

#### Funcionalidades Laravel
![Productos Laravel](evidencias/03-laravel-products.png)
*Lista de productos en Laravel*

![API JSON](evidencias/04-laravel-api.png)
*API REST funcionando correctamente*

### 2. 💾 Base de Datos y Usuario MySQL

#### Base de Datos Creada
![Base de Datos](evidencias/05-mysql-database.png)
*Base de datos `samuelcorrea` creada correctamente*

#### Tablas Generadas por Migraciones
![Tablas MySQL](evidencias/06-mysql-tables.png)
*6 tablas creadas automáticamente por Laravel*

#### Usuario MySQL Configurado
![Usuario MySQL](evidencias/07-mysql-user.png)
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

## 🐳 Comandos Docker Utilizados

### Construcción de Imagen
```bash
docker build -t laravel-samuel-correa:1.0 .
docker run --rm laravel-samuel-correa:1.0 php artisan key:generate --show
```

### Despliegue de Infraestructura
```bash
docker compose -f compose.infra.yaml up -d --wait --wait-timeout 240
docker compose -f compose.infra.yaml ps
```

### Despliegue de Aplicación
```bash
docker compose -f compose.app.yaml up -d
docker compose -f compose.app.yaml exec --user www-data app php artisan migrate --force
```

### Verificación de Persistencia
```bash
docker compose -f compose.app.yaml down
docker compose -f compose.infra.yaml down
docker compose -f compose.infra.yaml up -d --wait --wait-timeout 240
docker compose -f compose.app.yaml up -d
```

## 📈 Estado Final del Despliegue

### Contenedores Activos
- ✅ `samuel-correa-infra-mysql-1` - **Healthy**
- ✅ `samuel-correa-infra-phpmyadmin-1` - **Running** 
- ✅ `samuel-correa-app-app-1` - **Running**

### Base de Datos
- ✅ Base: `samuelcorrea`
- ✅ Usuario: `samuelcorrea` 
- ✅ Tablas: 6 (users, products, comments, jobs, cache, personal_access_tokens)
- ✅ Persistencia: Garantizada con volúmenes Docker

### Red Docker
- ✅ Red: `samuel-correa-net`
- ✅ Aislamiento: Completo de otros estudiantes
- ✅ Comunicación interna: Funcional entre contenedores

## 🔐 Credenciales de Acceso

### phpMyAdmin (Root)
- **Usuario**: `root`
- **Contraseña**: `8b4b01270caa2db053062647edcac0c295316b2048808f45`

### Base de Datos Aplicación
- **Usuario**: `samuelcorrea`  
- **Contraseña**: `4609a848bce08ccbbc29367dd5be8f36c8709b1adea059e3`
- **Base**: `samuelcorrea`

## 📝 Conclusiones

El Tutorial 05 se ha completado exitosamente con todos los objetivos cumplidos:

1. ✅ **Despliegue en AWS EC2** con Amazon Linux 2023
2. ✅ **Imagen Docker personalizada** para Laravel
3. ✅ **Infraestructura separada** (MySQL + phpMyAdmin)  
4. ✅ **Aplicación independiente** con su propia red
5. ✅ **Persistencia de datos** verificada
6. ✅ **URLs públicas** funcionando correctamente
7. ✅ **Coexistencia** con otros estudiantes en la misma instancia

El despliegue demuestra el uso correcto de Docker Compose para aplicaciones multi-contenedor, separación de responsabilidades, manejo de redes Docker y persistencia de datos en entornos de producción.

---

**Repositorio**: https://github.com/SamuelCV12/scorreav5-Topicos-Software  
**Tutorial**: 05 - Docker Deployment  
**Estado**: ✅ Completado