# **Atividade Prática de Docker**  
**Gerenciamento de Contêineres com Docker**  

---
## 📌 **Descrição do Projeto**  
Este repositório contém os resultados da atividade prática de **Computação em Nuvem**, onde exploramos os conceitos básicos de containers Docker, incluindo:  
✅ Execução de containers (`hello-world`, `ubuntu`)  
✅ Criação de servidores web com **Nginx**  
✅ Gerenciamento de imagens e containers  
✅ Uso de portas e acesso remoto  
---
## 🛠 **Tecnologias Utilizadas**  
- **Docker** (versão 24.0.7)  
- **Imagens Oficiais**:  
  - `hello-world`  
  - `ubuntu`  
  - `nginx` (servidor web)  
  - `mysql` (imagem adicional testada)  
---
## 📂 **Estrutura do Repositório**  
```
atividade-docker/  
├── relatorio.md          # Relatório detalhado da atividade  
├── screenshots/          # Prints dos resultados (opcional)  
│   ├── nginx-8081.png  
│   └── docker-ls.png  
└── README.md             # Este arquivo  
```
---
## 🚀 **Como Reproduzir a Atividade**  

### **1. Pré-requisitos**  
- Docker instalado ([Download Docker Desktop](https://www.docker.com/products/docker-desktop/))  
- Terminal (PowerShell, Bash ou Command Prompt)  

### **2. Comandos Executados**  
```bash
# Verificar versão do Docker
docker --version

# Executar container hello-world
docker run hello-world

# Criar servidor Nginx na porta 8081
docker run -d -p 8081:80 --name ws1 nginx
```
*(Lista completa no [relatorio.md](relatorio.md))*  

### **3. Testando os Servidores Web**  
- Acesse no navegador:  
  - `http://localhost:8081` (servidor `ws1`)  
  - `http://localhost:8082` (servidor `ws2`)  

---

## 🔍 **Principais Observações**  
✔️ **Containers são efêmeros**: Os containers `hello-world` e `ubuntu` encerram após a execução.  
✔️ **Nginx em segundo plano**: O servidor web permanece ativo até ser interrompido manualmente.  
✔️ **Isolamento de portas**: Cada instância do Nginx requer uma porta diferente (ex: 8081, 8082).  

*(Dificuldades e soluções detalhadas no [relatório completo](relatorio.md).)*  

---
## 📊 **Tamanho das Imagens**  
| Imagem       | Tamanho  |  
|--------------|----------|  
| `hello-world`| 13.3kB   |  
| `ubuntu`     | 77.8MB   |  
| `nginx`      | 142MB    |  

---

## 📜 **Licença**  
Este projeto é parte de uma atividade acadêmica da **Faculdade Anhanguera**.  

--- 

🔗 **Links Úteis**:  
- [Documentação Docker](https://docs.docker.com/)  
- [Docker Hub](https://hub.docker.com/)  

---  

## ⚠️ **Dificuldades e Soluções Encontradas**  

Durante a execução da atividade, enfrentei alguns desafios técnicos. Abaixo estão os principais problemas e como foram resolvidos:  

---

### **1. Docker não reconhecido no terminal**  
**Erro:**  
```bash
docker: command not found
```  
**Causa:**  
- Docker Desktop não estava instalado ou o PATH do sistema não estava configurado corretamente.  

**Solução:**  
✔️ Reinstalei o Docker Desktop ([download oficial](https://www.docker.com/products/docker-desktop/))  
✔️ Verifiquei se o serviço Docker estava rodando (ícone na bandeja do sistema).  

---

### **2. Erro ao acessar `http://localhost:8081`**  
**Erro:**  
```
This site can’t be reached
```  
**Causas possíveis:**  
- Container não estava em execução.  
- Porta 8081 já em uso por outro aplicativo.  
- Firewall bloqueando o acesso.  

**Solução:**  
✔️ Verifiquei os containers ativos:  
```bash
docker container ls
```  
✔️ Reiniciei o container `ws1`:  
```bash
docker start ws1
```  
✔️ Testei outra porta (ex: `8082`) e desativei temporariamente o firewall.  

---

### **3. Falha ao executar container Ubuntu interativo**  
**Erro:**  
```bash
Unable to find image 'ubuntu:latest' locally
docker: Error response from daemon: pull access denied.
```  
**Causa:**  
- Problemas de conexão com o Docker Hub ou falta de permissões.  

**Solução:**  
✔️ Executei o Docker como administrador.  
✔️ Verifiquei a conexão com a internet e tentei novamente:  
```bash
docker run -it ubuntu bash
```  

---

### **4. Container MySQL não iniciava**  
**Erro:**  
```bash
[ERROR] [FATAL] InnoDB: Cannot allocate memory for the buffer pool
```  
**Causa:**  
- Limite de memória insuficiente no Docker.  

**Solução:**  
✔️ Aumentei os recursos no Docker Desktop:  
`Settings > Resources > Memory` (aumentei para 4GB).  

---

### **5. Acesso remoto não funcionava**  
**Erro:**  
- Navegador externo não conseguia acessar `http://[IP]:8081`.  

**Causa:**  
- Firewall do Windows ou roteador bloqueando a porta.  

**Solução:**  
✔️ Liberei a porta `8081` no firewall:  
```powershell
New-NetFirewallRule -DisplayName "Allow Docker Port 8081" -Direction Inbound -LocalPort 8081 -Protocol TCP -Action Allow
```  

---

## 📌 **Lições Aprendidas**  
- **Sempre verificar se o Docker está rodando** antes de executar comandos.  
- **Testar portas alternativas** se a padrão estiver ocupada.  
- **Containers consomem recursos**, ajustar configurações conforme necessário.  

*(Detalhes completos no [relatório](relatorio.md).*  

--- 
## 🐳 **Imagem Adicional do Docker Hub Utilizada**  

Para complementar a atividade, explorei a imagem oficial do **MySQL** disponível no Docker Hub.  

---

### 🔍 **Por que escolhi o MySQL?**  
- É um dos bancos de dados mais populares, amplamente usado em aplicações web.  
- Permite testar a integração entre containers (ex: Nginx + MySQL).  
- A imagem é bem documentada e mantida pela comunidade.  

---

### 🛠 **Como Utilizei a Imagem**  

#### **1. Baixei a imagem oficial**  
```bash
docker pull mysql
```

#### **2. Executei um container MySQL**  
```bash
docker run --name meu-mysql -e MYSQL_ROOT_PASSWORD=senha123 -d mysql
```  
**Explicação dos parâmetros:**  
- `--name meu-mysql`: Nomeou o container como "meu-mysql".  
- `-e MYSQL_ROOT_PASSWORD=senha123`: Definir a senha do root (obrigatório).  
- `-d`: Executou em segundo plano.  

#### **3. Verifiquei se o MySQL estava rodando**  
```bash
docker ps
```  
**Saída esperada:**  
```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                 NAMES
a1b2c3d4e5f6   mysql     "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   3306/tcp, 33060/tcp   meu-mysql
```

#### **4. Acessei o banco de dados dentro do container**  
```bash
docker exec -it meu-mysql mysql -uroot -p
```  
- Inseri a senha (`senha123`) e consegui interagir com o MySQL via CLI.  

#### **5. Criei um banco de dados teste**  
```sql
CREATE DATABASE atividade_docker;
USE atividade_docker;
CREATE TABLE usuarios (id INT, nome VARCHAR(50));
```  

---

### 📊 **Dados Técnicos da Imagem**  
| Item               | Detalhe                          |  
|--------------------|----------------------------------|  
| **Repositório**    | [hub.docker.com/_/mysql](https://hub.docker.com/_/mysql) |  
| **Tamanho**        | ~519MB (versão `latest`)         |  
| **Porta padrão**   | 3306                             |  

---

### 🔗 **Integração com Outros Containers**  
Para simular um ambiente real, conectei o MySQL a um container com **PHPMyAdmin**:  
```bash
docker run --name phpmyadmin -d --link meu-mysql:db -p 8080:80 phpmyadmin/phpmyadmin
```  
- Acessei a interface pelo navegador: `http://localhost:8080`.  

---

### 📌 **Aprendizados**  
✔️ **Persistência de dados**: Volumes Docker são necessários para manter os dados do MySQL após a remoção do container.  
✔️ **Segurança**: É crucial usar senhas fortes e variáveis de ambiente (`-e`).  
✔️ **Networking**: Containers podem se comunicar via rede bridge padrão do Docker.  
--- 
Desenvolvido por: Pedro Vinicius Sousa Lima
Curso: Ciência da Computação
Disciplina: Computação em Nuvem
