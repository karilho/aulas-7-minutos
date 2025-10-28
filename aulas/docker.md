# 🐳 Docker em 7 Minutos

## 🚀 1. O que é Docker

Docker é uma plataforma de desenvolvimento de software baseada em **virtualização**, que permite empacotar e executar aplicações em **containers** — ambientes isolados e consistentes.  
Com isso, é possível rodar a **mesma aplicação** em Linux, Windows ou macOS da mesma forma, geralmente gerenciada pelo **Docker Compose**.

---

## ⚙️ 2. Virtualização x Docker

Na **virtualização clássica**, cada máquina virtual (VM) possui um sistema operacional completo, suas próprias bibliotecas e kernel. Isso consome mais CPU e memória.  

O **Docker**, por outro lado, também usa virtualização — mas **muito mais leve**.  
Por meio da **Docker Engine**, os containers compartilham o kernel do host, mantendo isolamento entre si, sem precisar de um sistema operacional completo por instância.

---

## 📘 3. Conceitos Fundamentais

**Kernel:**  
Coração do sistema operacional. Gerencia CPU, memória, disco e rede. No Docker, os containers compartilham o kernel do host, o que os torna mais leves.  

**Imagem:**  
Uma **imagem** é um pacote leve e autossuficiente que contém tudo o que um software precisa para rodar: código, bibliotecas e configurações.  É um **molde** para criar containers.  

**Hypervisor:**  
Software que cria e gerencia máquinas virtuais (VMs). Ele intermedeia o hardware do host e o sistema operacional convidado.  
*Exemplos:* VirtualBox, VMware, Hyper-V.  

**Docker Engine:**  
Camada responsável por criar e executar containers. Funciona como o “motor” do Docker, usando o kernel do host para isolar processos.  

**Virtual Machine (VM):**  
Simulação completa de um computador, com sistema operacional, kernel e bibliotecas próprios. Mais pesado, mas totalmente isolado.  

**Container:**  
Ambiente isolado que roda uma aplicação com todas as suas dependências, compartilhando o kernel do host. Muito mais leve e rápido que uma VM.  

---

<img width="1025" height="570" alt="image" src="https://github.com/user-attachments/assets/25906a17-bc46-49a7-80d6-f7b9caf0ac0f" />


---

## 🌍 4. Benefícios e Usos do Docker Hoje

- **Escalabilidade e Flexibilidade:** Suba ou remova containers rapidamente conforme a demanda.  
- **Padronização:** Mesma aplicação funciona em qualquer sistema.  
- **Isolamento:** Cada container roda de forma independente.  
- **Integração Contínua (CI/CD):** Facilita pipelines automatizados.  
- **Ambientes Reproduzíveis:** Ideal para desenvolvimento e testes.  

**Usos Comuns:**  
- Hospedagem de microserviços.  
- Criação de ambientes de desenvolvimento idênticos.  
- Execução de pipelines CI/CD.  
- Infraestrutura de Data Science e Machine Learning.  

---

## 🧱 5. Dockerizando Aplicações

“Dockerizar” uma aplicação significa empacotá-la em um container.  
Para isso, cria-se um arquivo **Dockerfile**, que define o passo a passo de como gerar a imagem.  

**Exemplo de Dockerfile:**

```dockerfile

# Use a base image oficial do Go (contém a toolchain Go e o ambiente necessário)
FROM golang:1.22

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Copia todos os arquivos do diretório local para o diretório de trabalho do container
COPY . .

# Executa o build do binário Go dentro do container e gera o executável chamado "main"
RUN go build -o main .

# Define o comando padrão que será executado quando o container iniciar:
# aqui rodamos o executável que foi gerado na etapa anterior
CMD ["./main"]

````
Em seguida, gera-se a imagem e roda-se o container:

````bash
docker build -t minha-app .

docker run -p 8080:8080 minha-app
````

---

## 🧩 6. Docker Compose com Imagem
O Docker Compose permite orquestrar múltiplos containers (como app + banco).

Exemplo:

````yaml

version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:8080"
  db:
    image: postgres:16
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb

````

## ☁️ 7. Docker Hub
O Docker Hub é o repositório oficial de imagens Docker.
Lá é possível baixar imagens prontas (como postgres, redis, nginx) ou enviar suas próprias.

Comandos úteis:


Sempre exibir os detalhes

Copiar código

````bash
# Baixar imagem
docker pull nginx

````

# Enviar imagem

````bash
docker login
docker tag minha-app usuario/minha-app:v1
docker push usuario/minha-app:v1

````
