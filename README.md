# tallerjulio2023
Obligatorio - Repositorio del Taller de Linux, julio de 2023. Este Repositorio contiene los Playbooks de Ansible necesarios para el Despliegue de:
- Una Aplicación Web Java en ambiente de Contenedor Podman
- Un Servidor Apache para cumplir la funcionalidad de Proxy Reverso
- Un Servidor de Base de Datos MariaDB

Se incluye además la habilitación necesaria de cada uno de los Servicios en el Firewall.

Ambos Playbooks pueden ser ejecutados tanto en Servidores RedHat/Rocky como Ubuntu, y se incluyen los archivos necesarios para todos los despliegues.

## Playbook webserver
Los pasos del despliegue se detallan a continuación:
- Determinar distribución e inicializar la variable “pkg_mgr” para el caso que corresponda.
- Instalación de Podman.
- Instalación del Servidor Web Apache.
- Inicio y habilitación de Servicio Apache.
- Creación de Directorios: VirtualHosts, Webapp.
- Copia de Archivo de Configuración de Proxy Reverso.
- Modificación de Archivo de Configuración del Servidor Apache para incluir los módulos de Proxy y la ruta al Directorio donde se almacena el VirtualHost.
- Copia de “todo.war” y Dockerfile al Directorio correspondiente.
- Build de la Aplicación utilizando Podman.
- Despliegue de la Aplicación utilizando Podman.
- Habilitación de Servicio a través de Firewall.
- Reinicio de Servidor Web Apache.

## Playbook dbserver
Los pasos del despliegue se detallan a continuación:
- Determinar distribución e inicializar la variable “pkg_mgr” para el caso que corresponda.
- Instalación de Servidor MariaDB.
- Instalación de Complemento “PyMySQL” para la ejecución de tareas iniciales desde el Servidor Bastión.
- Habilitación e Inicio del Servicio de Base de Datos.
- Configuración del Servidor para que escuche en todas las interfaces de Red.
- Publicación en el Firewall del puerto del Servicio.
- Servicios de Gestión Inicial:
- Actualización de root password.
- Borrado de login anónimo.
- Borrado de Base de Datos “Test”.

## Requisitos
* Se requieren al menos 2 servidores para realizar el Despliegue: un servidor Bastión para ejecutar los Playbooks y uno para instalar y habilitar los Servicios.
* Se recomiendan tres equipos desplegados de la siguiente forma: Servidor Rocky (Bastión), Servidor Rocky (Web + Reverse Proxy), Servidor Ubuntu (Base de Datos).
* Se requiere la creación de un usuario ansible con permisos de sudo en los servidores donde se realizará el despliegue, idealmente sin contraseña con clave ssh.
* Archivo dbpassword.yml generado mediante el comando ad-hoc ansible-vault.

## Ejecución
Para ejecutar el Playbook Webserver, basta con ejecutar el siguiente comando
```
ansible-playbook webserver.yml --ask-become-pass
```
Para ejecutar el Playbook DBserver, basta con ejecutar el siguiente comando
```
ansible-playbook dbserver.yml --ask-become-pass --ask-vault-pass
```
Una vez que comienza, se muestran en pantalla los pasos mencionados anteriormente y su correspondiente resultado de ejecución. El Playbook finaliza su ejecución con un resumen de las tareas realizadas.

## Distribuciones soportadas actualmente
Estos Playbooks fueron ejecutados y probados en las siguientes distribuciones:
* RedHat/CentOS
* Ubuntu

Utiliza a tu riesgo si no ves tu distribución incluida aquí.
