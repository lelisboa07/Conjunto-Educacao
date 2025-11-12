# Conjunto-Educação

# Projeto Profissional - Planejamento

Aluno: Letícia da Rosa Lisboa

Título do Projeto: Conjunto Educação: Plataforma digital interativa com orientação para pais/responsáveis e profissionais da área da Pedagogia

Repositório: https://github.com/lelisboa07/Conjunto-Educacao

Professor Orientador: Rafaella Egues da Rosa e Iuri Nascimento Santos

Período: Maio a Novembro de 2025

## Objetivo da Aplicação

Fortalecer a educação inclusiva nos anos iniciais, por meio de uma plataforma que promove o diálogo entre famílias e profissionais da pedagogia, além de conscientizar sobre a importância de práticas educativas inclusivas para o desenvolvimento integral das crianças.

## Tecnologias usadas

- HTML
- CSS
- JavaScript

## Configuração e Instalação

Para que a aplicação funcione corretamente, siga os passos abaixo.

### Pré-requisitos:
- Node.js
- Servidor MySQL

### 1. Clonagem do Repositório

```bash
git clone https://github.com/seu-usuario/nome-do-repositorio.git
cd nome-do-repositorio
```

### 2. Instalação das Dependências

```bash
npm install express mysql2 cors dotenv
```

### 3. Configuração do Ambiente

Dentro do arquivo `db_config.js` preencha com suas credenciais do banco de dados:

```env
DB_HOST=localhost
DB_USER=seu_usuario_mysql
DB_PASSWORD=sua_senha_mysql
DB_NAME=projeto_pp
```

### 4. Setup do Banco de Dados

```sql
create database projeto_pp;
use projeto_pp;

create table usuario(
    id int auto_increment primary key,
    name varchar(255) not null,
    email varchar(255) not null,
    password varchar(255) not null,
    criado_em timestamp default current_timestamp
);

CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES usuario(id) ON DELETE CASCADE
);

CREATE TABLE comments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    post_id INT NOT NULL,
    user_id INT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES usuario(id) ON DELETE CASCADE
);

CREATE TABLE likes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    post_id INT NOT NULL,
    user_id INT NOT NULL,
    FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES usuario(id) ON DELETE CASCADE,
    UNIQUE KEY unique_like (post_id, user_id) 
);

CREATE TABLE private_messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sender_id INT NOT NULL,
    recipient_id INT NOT NULL,
    message TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (sender_id) REFERENCES usuario(id) ON DELETE CASCADE,
    FOREIGN KEY (recipient_id) REFERENCES usuario(id) ON DELETE CASCADE
);
```

### 5. Execução

Inicie o servidor backend:

```bash
cd backend
npm start
```
