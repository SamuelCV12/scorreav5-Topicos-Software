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
APP_URL=http://3.91.71.33:8081
DB_DATABASE=samuelcorrea
DB_USERNAME=samuelcorrea
```

## 🌐 URLs de Acceso

- **Laravel**: http://3.91.71.33:8081
- **phpMyAdmin**: http://3.91.71.33:9081

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
![Base de Datos](https://github.com/user-attachments/assets/40b73667-65f7-4a9e-bf78-d45037f6a5cd
)


*Base de datos `samuelcorrea` creada correctamente*

#### Tablas Generadas por Migraciones
![Tablas MySQL](https://github.com/user-attachments/assets/79c44993-0009-4243-a9cb-e9453fd98a83
)
*6 tablas creadas automáticamente por Laravel*

#### Usuario MySQL Configurado
![Usuario MySQL](https://github.com/user-attachments/assets/01e72f32-a789-4279-a2b8-66d1ff0d9750
)
*Usuario `samuelcorrea` con permisos correctos*

#### Datos Almacenados
![Datos Productos](https://github.com/user-attachments/assets/10f4d808-4d45-4ac1-b434-77b2d12cea4c
)
*Datos guardados correctamente en la base*

### 3. 🔄 Persistencia de Datos

#### Comandos de Reinicio
![Terminal Down](https://github.com/user-attachments/assets/c1afcf89-6616-4698-b176-10940ab59968
)
*Deteniendo contenedores para probar persistencia*

![Terminal Up](https://github.com/user-attachments/assets/6a59732d-c055-44b6-915b-d406908c6be8
)
*Reiniciando contenedores*

#### Verificación Post-Reinicio
![Laravel Post-Restart](https://github.com/user-attachments/assets/4756e13b-2c4f-464d-8831-aa3f89c68bd5
)
*Laravel funcionando después del reinicio*

![Datos Persistentes](https://github.com/user-attachments/assets/308f6089-92b1-46ea-b4f5-70dea381ebff
)
*Los datos siguen existiendo en MySQL*

