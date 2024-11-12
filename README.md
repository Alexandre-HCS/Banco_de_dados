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

```SQL
CREATE DATABASE biblioteca;
USE biblioteca;
```

### 1.2 Criação a Tabela 'editora'

```SQL
CREATE TABLE editora (
    id_editora INT PRIMARY KEY AUTO_INCREMENT,
    nome_editora VARCHAR(100) NOT NULL,
    pais VARCHAR(50)
);
```
### 1.3 Criação a Tabela 'autor'

```SQL
CREATE TABLE autor (
    id_autor INT PRIMARY KEY AUTO_INCREMENT,
    nome_autor VARCHAR(200),
    data_nacimento DATA
);
```

### 1.4 Criação a Tabela 'assunto'

```SQL
CREATE TABLE assunto (
    id_assunto INT PRIMARY KEY AUTO_INCREMENT,
    descricao_assunto VARCHAR(300)
);
```
### 1.5 Criação a Tabela 'livro'

```SQL
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

```SQL
CREATE TABLE extra (
    id_livro INT PRIMARY KEY AUTO_INCREMENT,
    produtos VARCHAR(50) NOT FULL,
    quantidade INT(20) NOT FULL,
    preco DOUBLE NOT FULL
);
```
## Passo 2: editar tabelas usando 'ALTER'
Após a criação da tabela, podemos adicionar novos campos. Vamos adicionar uma coluna 'email' na tabela 'autor'

```SQL
ALTER TABLE autor
ADD COLUMN email VARCHAR(100);
```
## Passo 3: Remover tabrla usando 'DROP'

```SQL
DROP TABLE extra;
```

## Passo 4: Inserindo dados usando 'INSERT'
Agora que as tabelas já estão prontas, vamos inserir dados nelas

## Passo 4.1 Inserindo dados na tabela 'editora'

```SQL
INSERT INTO editora(nome_editora, pais)
VALUES
('New England', 'Inglaterra'),
('Editora Visão', 'Brasil'),
('Kentucky Books', 'Estados Unidos');
```

## Passo 4.2 Inserindo dados na tabela 'autor'

```SQL
INSERT INTO autor(nome_autor, data_nascimento, email)
VALUES
('Tom Fox', '1934-09-04', 'fox.t@gmail.com'),
('Joaquim Silveira', '2000-07-11', 'joa.sa@gmail.com'),
('Michael Woods', '1975-06-03', 'michael.florest@gmail.com');
```

## Passo 4.3 Inserindo dados na tabela 'assunto'

```SQL
INSERT INTO assunto(descricao_assunto)
VALUES
('Ficção'),
('Romance'),
('Mistério'),
('Aventura'),
('Terror'),
('Ação');
```

## Passo 4.4 Inserindo dados na tabela 'livro'

```SQL
INSERT INTO livro(titulo, ano_publicaçao, editora, autor, assunto)
VALUES
('Noite de Verão', '1942', 1, 1, 2),
('Juizado à Sorrow', '1990', 3, 3, 6),
('Assinado: Priscila', '2021', 2, 2, 2),
('Tal Muro', '1980', 3, 3, 2),
('Te Vejo Em Breve', '2011', 2, 2, 2);
```

## Passo 5: Atualizando nos dados usando 'UPDATE'

## Passo 6: Excluindo dados usando 'DELETE'
Para removermos registros de uma tabela utilizamos o comando 'DELETE'
Vamos usar de exemplo um dos livros já existentes

```SQL
DELETE FROM livro
WHERE id_livro = 4;
```

## Passo 7: Selecionando dados usando 'SELECT'
Para selecionar os dados para visualizar da forma como quiser
PAra isso usamos o comando 'SELECT'

## Passo 7: Selecionar todos os livros com suas editoras e autores
Vamos usar os dados das tabelas 'livros', 'editora', 'autor' e 'assunto' usando o comando 'JOIN'

```SQL
SELECT livro.titulo AS titulo,
        editora.nome_editora AS editora,
        autor.nome_autor AS autor,
        assunto.descricao_assunto AS tema,
        livro.ano_publicacao AS ano
FROM livro
JOIN editora ON livro.editora = editora.id_editora
JOIN autor ON livro.autor = autor.id_autor
JOIN assunto ON livro.assunto = assunto.id_assunto
```

## Passo 7: Selecionar todos os livros do mesmo tipo
Vamos usar os dados das tabelas 'livros', 'editora', 'autor' e 'assunto' usando o comando 'JOIN'

```SQL
SELECT FROM livro
WHERE assunto = 2
```

-- Consulta com filtro WHERE

```SQL
SELECT livro.titulo AS título,
        assunto.descricao_assunto AS tema
FROM livro
JOIN assunto ON livro.assunto = assunto.id_assunto
WHERE assunto.descricao_assunto = 'Romance'
```