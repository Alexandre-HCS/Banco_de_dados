# Passo a passo : Criação de um banco de dados
Tutorial de como criar um banco de dados SQL que organiza as informações de 'livros', 'editora', 'autores e 'assuntos'.Este guia será dividido em etapas para demonstrar desde a criação de tabelas, chaves e até manipulação/consulta de dados

## Resumo de uma estrutura SQL

*_CREATE_ para criar 'Banco de dados' ou 'Tabelas'
*_ALTER_ para adicionar ou modificar colunas
*_DROP_ para remover 'Banco de dados' ou 'Tabelas'
*_INSERT_ para adicionar registros na tabela
*_UPDATE_ para atualizar os registros
*_DELETE_ para remover os registros
*_SELECT_ para consultar e visualizar dado

## Passo 1: criação do Banco de dados e das Tabelas
### 1.1 Criação o DB

```
CREATE DATABASE biblioteca;
USE biblioteca;
```
### 1.2 Criação a Tabela 'editora'
```
CREATE TABLE editora (
    id_editora INT PRIMARY KEY AUTO_INCREMENT,
    nome_editora VARCHAR(100) NOT NULL,
    pais VARCHAR(50)
);
```
### 1.3 Criação a Tabela 'autor'
```
CREATE TABLE autor (
    id_autor INT PRIMARY KEY AUTO_INCREMENT,
    nome_autor VARCHAR(200),
    data_nacimento DATA
);
```

### 1.4 Criação a Tabela 'assunto'
```
CREATE TABLE assunto (
    id_assunto INT PRIMARY KEY AUTO_INCREMENT,
    descricao_assunto VARCHAR(300)
);
```
### 1.5 Criação a Tabela 'livro'
```
CREATE TABLE livro (
    id_livro INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(150) NOT NULL,
    ano_publicaçao YEAR,
    editora INT,
    autor INT,
    assunto INT,
    FOREIGN KEY (editora) REFERENCES editora(id_editora),
    FOREIGN KEY (autor) REFERENCES autor(id_autor),
    FOREIGN KEY (assunto) REFERENCES assunto(id_assunto)
);
```
### 1.6 Criação a Tabela 'Extra'
a tabela EXTRA vai servir para exemplificar a exclusão
```
CREATE TABLE extra (
    id_livro INT PRIMARY KEY AUTO_INCREMENT,
    produtos VARCHAR(50) NOT FULL,
    quantidade INT(20) NOT FULL,
    preco DOUBLE NOT FULL
);
```
## Passo 2: editar tabelas usando 'ALTER'
Após a criação da tabela, podemos adicionar novos campos. Vamos adicionar uma coluna 'email' na tabela 'autor'

```
SQL
ALTER TABLE autor
ADD COLUMN email VARCHAR(100);
```
