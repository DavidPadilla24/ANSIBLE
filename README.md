# ANSIBLE

![PORTADA](https://www.strsistemas.com/sites/default/files/imagen_ansible.jpg)
# Estudio del Módulo `assemble` en Ansible

## 1.- Nombre del módulo: `assemble`

### Descripción
El módulo `assemble` de Ansible se utiliza para combinar múltiples archivos en uno solo. Es útil cuando tienes fragmentos de archivos de configuración dispersos y necesitas ensamblarlos en un solo archivo en el nodo remoto. Este módulo es comúnmente utilizado para la gestión de configuraciones complejas y para juntar archivos de forma dinámica.

## 2.- Ejemplos de funcionamiento

### Ejemplo 1: Unir archivos de configuración

Para este playbook necesitaremos archivos de configuracion separados y lo vamos a juntar en uno solo. Por ejemplo de apache. 

![Captura del playbook](imagenes/ejemploplaybook.png)


```yaml
- name: Unir fragmentos de configuración de Apache en un servidor Debian
  hosts: debian1  # Reemplazar con el nombre de tu host o grupo de hosts
  become: true  # Permite ejecutar el playbook con permisos de superusuario
  tasks:
    - name: Unir fragmentos de la configuración de Apache
      ansible.builtin.assemble:
        src: /home/usuario/apache_fragments/  # Ruta local donde están los fragmentos
        dest: /etc/apache2/apache2.conf  # Ruta de destino donde se combinarán los archivos
```
Comando para lanzar playbook ``` ansible-playbook nombre_playbook```

![Captura del playbook](imagenes/playbook2.png)

Observamos que nos aparece changed , vamos a comprobarlo

![Captura del playbook](imagenes/playbook3.png)


Como vemos se han juntado los tres fragmentos que teniamos en un solo archivo de configuracion.


### Ejemplo 2: Unir scripts

Para este playbook necesitaremos pequeños scripts separados , en este caso de instalacion y configuracion de mysql.

![Captura del playbook](imagenes/playbook4.png)



```yaml

- name: Unir fragmentos de un script de instalación en un solo archivo
  hosts: debian1  # Reemplazar con tu host o grupo de hosts
  become: true  # Permite ejecutar el playbook con privilegios de superusuario
  tasks:
    - name: Unir fragmentos del script de instalación de MySQL
      ansible.builtin.assemble:
        src: /home/usuario/mysql_install/  # Ruta local donde están los fragmentos
        dest: /usr/local/bin/mysql_install.sh  # Ruta de destino para el script combinado
        mode: '0755'  # Establecer permisos para que el archivo sea ejecutable
```
Comando para lanzar playbook ``` ansible-playbook nombre_playbook```

![Captura del playbook](imagenes/playbook5.png)

Observamos que nos aparece changed , vamos a comprobarlo

![Captura del playbook](imagenes/playbook6.png)


Vemos que ya nos han unido los pequeños scripts de instalacion en uno solo. Es muy util porque habiendo unido los pequeños scripts podemos instalar y configurar mysql en uno solo.



## 3.- Referencias

- https://docs.ansible.com/ansible/latest/collections/ansible/builtin/assemble_module.html
- [Manuel Domínguez](https://github.com/mftienda)

# Autor
[David Alvarez Padilla](https://github.com/DavidPadilla24)





