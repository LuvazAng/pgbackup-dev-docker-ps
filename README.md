# pgbackup-dev
**pgbackup-dev** es una utilidad interactiva para generar **backups de PostgreSQL desde contenedores Docker** de forma simple, rápida y visual desde **PowerShell**.

Está pensada para **entornos de desarrollo**, donde PostgreSQL corre dentro de Docker y los desarrolladores necesitan generar respaldos sin recordar comandos largos de `pg_dump`.

La herramienta ofrece una **interfaz de terminal mejorada**, un **selector interactivo de bases de datos** y generación automática de backups organizados por base de datos.

---
# Características

- Ejecuta backups directamente desde **contenedores Docker**
- **Selector interactivo de bases de datos**
- Soporte para múltiples formatos de backup:
    - `.sql` (plain text)
    - `.dump` (formato custom comprimido)
- **Interfaz CLI**
    - colores
    - animaciones
    - spinner de progreso
- Organización automática de **backups**
- Archivos con **timestamp**
- Basado en `pg_dump`

---

# Experiencia en terminal

```
pgbackup-dev  PostgreSQL Backup Utility · Docker  

Bases disponibles  
↑↓ navegar · Enter seleccionar · ESC cancelar  
  
▶ my_database  
  postgres  
  analytics
```

Durante el backup:
```
⠋ Generando .sql (plain)...  
✔ backups/my_database/backup_my_database_2026-03-11_1540.sql  
  
⠋ Generando .dump (custom, comprimido)...  
✔ backups/my_database/backup_my_database_2026-03-11_1540.dump
```

---

# Instalación

Clona el repositorio:
git clone https://github.com/tu-usuario/pgbackup-dev.git

Importa o copia la función en tu perfil de **PowerShell**.

Ejemplo:
```powershell
notepad $PROFILE
```


Pega la función `pgbackup-dev` y guarda.

Reinicia PowerShell.
```powershell
. $PROFILE
```

---

# Uso

## Abrir selector interactivo

```powershell
pgbackup-dev
```

Esto mostrará todas las bases disponibles dentro del contenedor.

---
## Backup directo

```powershell
pgbackup-dev -db my_database
```

---
## Generar solo SQL

```powershell
pgbackup-dev -db my_database -sql
```

---
## Generar solo dump comprimido

```powershell
pgbackup-dev -db my_database -dump
```


---
# Parámetros

|Parámetro|Descripción|Default|
|---|---|---|
|`-db`|Base de datos objetivo|—|
|`-u`|Usuario de PostgreSQL|`postgres`|
|`-p`|Contraseña|`root`|
|`-container`|Contenedor Docker|`postgres17`|
|`-sql`|Genera backup `.sql`||
|`-dump`|Genera backup `.dump`||
|`-help`|Muestra ayuda||

Si no se especifica formato, se generan **ambos**.

---

# Estructura de backups

Los archivos se organizan automáticamente:
```
backups/  
 └── database_name/  
      ├── backup_database_name_YYYY-MM-DD_HHMM.sql  
      └── backup_database_name_YYYY-MM-DD_HHMM.dump
```

Ejemplo:
```
backups/  
 └── app_db/  
      ├── backup_app_db_2026-03-11_1540.sql  
      └── backup_app_db_2026-03-11_1540.dump
```

---

# Requisitos

- Docker
- PostgreSQL ejecutándose dentro de un contenedor
- PowerShell
- `pg_dump` disponible dentro del contenedor

---

# Cómo funciona

Internamente la herramienta ejecuta:

```powershell
docker exec <container> pg_dump
```


Utilizando:

- `-F p` para `.sql`
- `-F c -Z 9` para `.dump` comprimido

---

# Objetivo del proyecto

`pgbackup-dev` nace para **simplificar los backups de PostgreSQL en entornos de desarrollo**, evitando comandos largos y proporcionando una **experiencia CLI clara, interactiva y amigable**.

---

# Licencia

MIT License
