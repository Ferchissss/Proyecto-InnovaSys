# Proyecto InnovaSys - Automatización con Ansible

## Descripción
Este proyecto automatiza la configuración de un servidor Ubuntu 24.04 para la startup InnovaSys, implementando:
- Un portal de bienvenida interno con Apache
- Un repositorio de archivos centralizado con Samba

## Requisitos
- Nodo de control: Linux Lite con Ansible instalado
- Nodo gestionado: Ubuntu Server 24.04 accesible por SSH
- Acceso SSH configurado entre nodos
    - Generar clave SSH (si no existe)
    ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -N ""
    - Copiar clave al servidor gestionado
    ssh-copy-id -i ~/.ssh/id_ed25519.pub operador@192.168.10.100
    - Probar conexión
    ssh operador@192.168.10.100
    exit
- Puerto 80 libre en Ubuntu

## Estructura del Proyecto

ProyectoInnovaSys/

├── ansible.cfg

├── inventories/

│ └── production

├── group_vars/

│ └── all/

│ └── vars.yml

├── roles/

│ ├── apache/

│ └── samba/

├── site.yml

└── README.md

## Variables Configurables
- `nombre_empresa`: Nombre de la empresa para la página web
- `samba_share_name`: Nombre del recurso compartido Samba
- `samba_share_path`: Ruta del directorio compartido
- `samba_group`: Grupo de usuarios Samba
- `samba_user`: Usuario Samba
- `samba_password`: Contraseña del usuario Samba

## Ejecución
```bash
cd ProyectoInnovaSys

ansible-playbook -i inventories/production site.ym
```  
## Verificación

Servidor Web: http://192.168.10.100

Recurso Samba: smb://192.168.10.100/Proyectos

Usuario: devuser1

Contraseña: Innova.2025

## 🔍 SOLUCIÓN DE PROBLEMAS COMUNES

```bash
### Si falla la instalación de paquetes:

# Actualizar cache de paquetes

sudo apt update

# Verificar acceso a internet

ping 8.8.8.8

Si Samba no funciona:

# Verificar servicio Samba en el servidor

ssh operador@192.168.10.100

sudo systemctl status smbd
```  
