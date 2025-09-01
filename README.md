# Proyecto InnovaSys - Automatización con Ansible

## Descripción
Este proyecto automatiza la configuración de un servidor Ubuntu 24.04 para la startup InnovaSys, implementando:
- Un portal de bienvenida interno con Apache
- Un repositorio de archivos centralizado con Samba

## Requisitos
- Nodo de control: Linux Lite con Ansible instalado
- Nodo gestionado: Ubuntu Server 24.04
- Acceso SSH configurado entre nodos

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

ansible-playbook site.yml

## Verificación

Servidor Web: http://192.168.10.100

Recurso Samba: smb://192.168.10.100/Proyectos

Usuario: devuser1

Contraseña: Innova.2025

Configuración exitosa:

✅ Servidor web Apache en http://192.168.10.100

✅ Recurso Samba en //192.168.10.100/Proyectos

✅ Usuario: devuser1, Contraseña: Innova.2025

## 🔍 SOLUCIÓN DE PROBLEMAS COMUNES

### Si falla la conexión SSH:

# Verificar conexión

ssh -v operador@192.168.10.100

# Regenerar claves si es necesario
ssh-keygen -R 192.168.10.100

Si falla la instalación de paquetes:

bash
# Actualizar cache de paquetes

sudo apt update

# Verificar acceso a internet

ping 8.8.8.8

Si Samba no funciona:

bash
# Verificar servicio Samba en el servidor

ssh operador@192.168.10.100

sudo systemctl status smbd
