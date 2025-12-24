# Relatório de Andamento das Atividades – Trainee
- **Nome:** Eduardo Fraga Pereira
- **Data:** 24/10/2025



---
## Card 1 - Criar o container do ROS 2
**Resultados obtidos**
Todo o conteúdo foi instalado satisfatoriamente, e testado com os nodes talker e listener.

**Problemas encontrados e como foram resolvidos**
Não estava conseguindo executar os comandos com docker, mas resolvi usando "sudo" no começo.

**Comentários e dificuldades de cada tarefa**
Fácil.



---
## Card 2 - Conceitos básicos do ROS
**Resultados obtidos**
Conteúdo aprendido, resumo feito e testes realizados.

**Problemas encontrados e como foram resolvidos**
Nenhum problema encontrado.

**Comentários e dificuldades de cada tarefa**
Fácil de entender, com exceção dos services que demandaram pesquisa adicional.



---
## Card 3 - ROS e Turtlesim
**Resultados obtidos**
Todos os testes foram realizados com sucesso.

**Problemas encontrados e como foram resolvidos**
- Os tutoriais utilizavam a versão iron, mas a atual é a humble, então alguns comandos eu tive que fazer uma pequena alteração.
- O turtlesim não abria, erros relacionados ao X11 e a parte gráfica (could not connect to display)(MESA: error: Failed to query drm device)(libGL error: failed to create dri3 screen). Todos os erros foram corrigidos recriando os containers com comandos específicos com o auxilio do chatGPT.
- Tive que baixar o gedit, pois não tinha baixado ainda.

**Comentários e dificuldades de cada tarefa**
Difícil, devido a enorme quantidade de erros encontrados.

**OBSERVAÇÃO**
O tutorial 1 e o tutorial 2 são o mesmo vídeo.



---
## Card 4 - ROS e Gazebo
**Resultados obtidos**
Todos os testes foram realizados.

**Problemas encontrados e como foram resolvidos**
Problemas novamente com o display gráfico, resolvi isso executando comandos de configuração que o chatGPT recomendou.

**Comentários e dificuldades de cada tarefa**
Fácil.



---
## Card 5 - Turtlebot

**Resultados obtidos**
Tudo rodando conforme esperado.

**Problemas encontrados e como foram resolvidos**
Problemas novamente com o display gráfico, resolvi novamente com o auxilio do chatgpt, porém irei resolver definitivamente sem "gambiarras" pra evitar futuros problemas.

**Comentários e dificuldades de cada tarefa**
Difícil, devido à quantidade de problemas pra rodar tudo junto.
<br>
<br>
<br>



---
## Resumo dos tópicos
### Primeiro card: Criar o container do ROS 2
Nenhum resumo necessário.

### Segundo card: Conceitos básicos do ROS
**Topic**
- Forma de comunicação entre nodes.
- Exemplo: o talker publica no chatter topic e o listener se inscreve no chatter topic.
- Os nodes não se comunicam diretamente entre si; eles apenas publicam ou se inscrevem em topics.
- É possível ter múltiplos nodes publicando em um mesmo topic, ou múltiplos nodes se inscrevendo em um topic.
- Cada topic tem um nome, que funciona como o "endereço" para os nodes saberem com quem se comunicar.
- Cada topic também tem um tipo de dado, que define o formato das mensagens enviadas e recebidas.
- O mecanismo de topics é anônimo — quem recebe não sabe quem enviou, e vice-versa.

**ROS Service**
- É uma comunicação de clientes, funcionando como uma "função" comum em linguagens de programação.
- Só pode haver um server, mas vários clients.
- Os clients fazem os pedidos enviando parâmetros de entrada, e o server processa esses dados e devolve uma resposta.
    ```
    int64 a //pedido
    int64 b //pedido
    ---
    int64 sum //resposta
    ```
- Nesse exemplo, os clients pedem a soma de dois inteiros (a e b), e o server responde com o resultado (sum).
- Usamos services em dois casos principais: processar dados (como o exemplo da soma de dois inteiros, esperando uma resposta) ou fazer mudança de configurações do robô.
- O rqt_graph não mostra services.

### Terceiro card: ROS e Turtlesim
**Criação do workspace**
- `mkdir -p ~/workspace/src`
- `cd ~/workspace/src`

**Build do workspace**
- `colcon build`
- `ls -l`
- `builder` -> arquivos intermediários, cada pacote com sua pasta para cmake
- `install` -> pacotes instalados, cada um com sua pasta separada
- `log` -> logs do build

**Criação do pacote python**
- `ros2 pkg create --build-type ament_python first_package`
- `cd first_package` (2x)

**Edição do publisher**
- `gedit publisher.py`

**Depois do build, carregar ambiente**
- `source ~/workspace/install/setup.b`

### Quarto card: ROS e Gazebo
**Baixando gazebo**
- `sudo apt install ros-humble-gazebo-ros-pkgs`
- `sudo apt install ros-humble-ros-core ros-humble-geometry2`
- `gazebo`

**Comandos e Caminhos**
- `/opt/ros/humble/share/gazebo_plugins/worlds/`
- `cd /opt/ros/share/gazebo_plugins/worlds/`
- `ls -l`
- `gazebo --verbose`
- `/opt/ros/humble/share/gazebo_plugins/worlds/gazebo_ros_diff_drive_demo.world`

### Quinto card: Turtlebot
Resumo não necessário.
