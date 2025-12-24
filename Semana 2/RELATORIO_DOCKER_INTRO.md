# 🐳 Docker para iniciantes
Este é um relatório que resume os ensinamentos da playlist "Docker Crash Course for Absolute Beginners" da TechWorld with Nana.
- **Nome:** Eduardo Fraga Pereira
- **Data:** 01/12/2025


---
## 1. O que é Docker e por que usar?
### O problema ("Na minha máquina funciona")
Antes, o desenvolvimento sofria com diferenças de ambiente (versão do OS, bibliotecas, dependências). O Docker resolve isso empacotando a aplicação e tudo o que ela precisa para rodar em um **Container**.

### Container vs máquina virtual (VM)
* **VM**: Tem um sistema operacional completo rodando sobre o Host. É pesado e lento para iniciar.
* **Container**: Compartilha o kernel do sistema operacional do Host. É leve, rápido (segundos para iniciar) e isolado.



---
## 2. Conceitos chave
### 🖼️ Imagem (image)
* É o "molde" ou a "planta" da sua aplicação.
* Contém o código, bibliotecas, variáveis de ambiente e arquivos de configuração
* É **imutável** (não muda depois de criada).

### 📦 Container
* É a instância de uma Imagem rodando.
* Pode ter vários containers rodando a partir da mesma imagem.
* É o ambiente onde a aplicação roda.

### 🗄️ Docker registry (Docker Hub)
* É onde as imagens são armazenadas (tipo um GitHub para imagens Docker)
* O **Docker Hub** é o registro público padrão.



---
## 3. Comandos essenciais
### Baixar e rodar
* `docker pull nginx`: Baixa a imagem do Nginx do Docker Hub.
* `docker run nginx`: Baixa (se não tiver) e sobe um container.
* `docker run -d nginx`: Roda em segundo plano (**Detached** mode).

### Listar e parar
* `docker ps`: Lista containers rodando.
* `docker ps -a`: Lista todos os containers (inclusive os parados).
* `docker stop <id_container>`: Mata um container
* `docker start <id_container>`: Inicia um container parado.

### Port binding
Para acessar a aplicação dentro do container, você precisa conectar a porta do container com a porta da sua máquina.
```bash
docker run -p 8080:80 nginx
```
* `8080`: Porta na sua máquina (Host).
* `80`: Porta dentro do container.
* Acesse em: `localhost:8080`.



---
## 4. Criação de imagens e Dockerfile
`Dockerfile` é um arquivo de texto com instruções para criar uma imagem.

Exemplo para uma aplicação Node.js:

```dockerfile
FROM node:14 #1. Imagem base
WORKDIR /app #2. Diretório de trabalho dentro do container
COPY package.json . #3. Copiar arquivos de dependências
RUN npm install #4. Instalar dependências
COPY . . #5. Copiar o resto do código
EXPOSE 3000 #6. Expor a porta
CMD ["node", "app.js"] #7. Comando para iniciar a aplicação
```

### Construindo a imagem
```bash
docker build -t meu-app-node:1.0 .
```
* `-t`: Tag (nome:versão)
* `.`: Contexto (pasta atual).



---
## 5. Ciclo de vida completo
1.  **Code**: Você escreve o código e o `Dockerfile`.
2.  **Build**: `docker build` cria a Imagem.
3.  **Push**: `docker push` envia a imagem para o Docker Registry (opcional, serve para compartilhar).
4.  **Run**: `docker run` baixa a imagem e cria o Container em qualquer servidor.



---
> **Dica:** usar **Docker Desktop** para uma interface visual que facilita o gerenciamento dos containers sem linha de comando.
