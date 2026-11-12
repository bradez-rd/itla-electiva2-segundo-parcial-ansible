# Laboratorio Ansible con dos servidores Docker

Objetivo: administrar dos contenedores Ubuntu 24.04 con Ansible y verificar la creación de archivos y directorios en ambos.

## Preparación

Se necesitan Docker Compose, Ansible y la colección `community.docker` en el equipo de control.

```bash
docker compose up -d
docker ps
docker exec server1 bash -lc 'apt update && apt install -y python3'
docker exec server2 bash -lc 'apt update && apt install -y python3'
ansible-galaxy collection install community.docker
ansible docker -i inventory.ini -m ping
ansible-playbook -i inventory.ini playbook.yml
```

El inventario usa `ansible_connection=docker`. Cada servidor recibe `/tmp/ansible-demo/info.txt` y los subdirectorios `logs`, `backup` y `config`.

## Evidencia de ejecución

La ejecución completa del laboratorio en GitHub Actions terminó correctamente: [ver ejecución y registro](https://github.com/bradez-rd/itla-electiva2-segundo-parcial-ansible/actions/runs/43133446360). El entorno local no dispone de Docker, por lo que la prueba se realizó en el runner Ubuntu de GitHub. El enlace permite verificar los comandos y la salida real del playbook. No se adjunta una captura de pantalla local.
