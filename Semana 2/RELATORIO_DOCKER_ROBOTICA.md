# 🤖 Docker para Robótica
Este é um relatório que resume os ensinamentos da playlist "Docker for Robotics" da The Construct, focando especificamente no uso de Docker para ambientes de robótica (ROS, Gazebo).
- **Nome:** Eduardo Fraga Pereira
- **Data:** 03/12/2025


---
## 1. Por que Docker na robótica?
Robótica envolve dependências complexas (versões específicas do ROS, drivers, bibliotecas de simulação).
* **Reprodutibilidade**: Garante que o código rode igual no seu laptop e no robô.
* **Isolamento**: Permite testar diferentes versões do ROS (ex: Noetic vs Humble) na mesma máquina sem conflitos
* **Deploy**: Facilita atualizar o software no robô físico.



---
## 2. Docker 101 para robótica
Os comandos básicos (`run`, `build`, `ps`) são os mesmos, mas o fluxo de trabalho muda.
Em vez de apenas rodar um servidor web, você geralmente precisa de:
* **Terminal Interativo**: `docker run -it ubuntu bash` para entrar no container e rodar comandos ROS.
* **Persistência**: Usar **Volumes** para editar código na sua máquina e ver o resultado no container instantaneamente



---
## 3. O Dockerfile de robótica
Um Dockerfile típico de ROS começa assim:

```dockerfile
FROM osrf/ros:humble-desktop

# Instalar dependências extras
RUN apt-get update && apt-get install -y \
    ros-humble-navigation2 \
    ros-humble-nav2-bringup

# Configurar o ambiente (source do ROS)
RUN echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc

# Diretório de trabalho
WORKDIR /root/ros2_ws
```



---
## 4. Acesso a hardware e GPU (O pulo do gato)
O maior desafio em robótica é acessar sensores (câmeras, LiDAR) e a GPU (para simulação Gazebo/Rviz) de dentro do container.

### Acesso a dispositivos (USB/serial)
Para acessar um sensor conectado via USB:
```bash
docker run -it --device=/dev/ttyUSB0 ubuntu bash
```
Ou, modo "privilegiado" (menos seguro, mas fácil para dev):
```bash
docker run -it --privileged -v /dev:/dev ubuntu bash
```

### Acesso a GPU (NVIDIA)
Para rodar simulações pesadas, você precisa do **NVIDIA Container Toolkit**.
```bash
docker run -it --gpus all osrf/ros:humble-desktop
```

### Interface gráfica (GUI)
Para abrir o **Rviz** ou **Gazebo** de dentro do container e ver na sua tela:
1.  Permitir conexões X11 no host: `xhost +`
2.  Rodar com variáveis de ambiente de display:
```bash
docker run -it \
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    osrf/ros:humble-desktop
```



---
## 5. Workflow de desenvolvimento
> "Se você não está desenvolvendo com isso, está perdendo tempo."

A recomendação é usar o **VS Code Remote - Containers (Dev Containers)**.
1.  Crie uma pasta `.devcontainer`.
2.  Configure o `devcontainer.json`.
3.  O VS Code abre *dentro* do container. Você edita, compila e roda tudo lá dentro, com autocompletar e debug funcionando perfeitamente para as bibliotecas instaladas no container.



---
## Resumo
* Use Docker para não quebrar seu sistema instalando 10 versões de ROS.
* Use `--net=host` para facilitar a comunicação de rede ROS entre container e host
* Use Dev Containers para uma experiência de desenvolvimento fluida.
