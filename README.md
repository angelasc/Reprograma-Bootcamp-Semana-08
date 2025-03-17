<h1 align="center">
  <img src="assets/reprograma-fundos-claros.png" alt="logo reprograma" width="500">
</h1>

# Reprograma | Bootcamp de Análise de Dados
## 🚀 Exercícios para Casa 
Turma Online on29 | Semana 08 | 2024 | Professora Daviny Letícia

Este repositório contém os exercícios desenvolvidos durante a **Semana 08** do curso de Análise de Dados da turma Online On29 da Reprograma. Os desafios foram realizados para consolidar os conhecimentos adquiridos em aula.  

## 📌 Descrição
Nesta semana, exploramos a continuidade do trabalho com bancos de dados relacionais, avançando para o uso de operações mais complexas, como joins, subconsultas e views. O objetivo foi aprofundar o uso de SQL e Python para realizar consultas mais robustas e eficazes.

## 🎯 Objetivos do projeto
- Implementar joins entre múltiplas tabelas para combinar dados de diferentes fontes.
- Utilizar subconsultas para realizar consultas complexas.
- Criar views para facilitar a reutilização de consultas SQL.
- Integrar essas operações com Python utilizando a biblioteca sqlite3.

## 📝 Conteúdo do Repositório  
O repositório está organizado da seguinte maneira:
- banco_de_dados.db: Arquivo do banco de dados gerado e manipulado pelo código Python.
- main.py: Código principal onde as operações do banco de dados são realizadas.
- requirements.txt: Dependências do projeto (caso existam).  

## 🖥️ Tecnologias utilizadas
- Python: Linguagem de programação utilizada para interagir com o banco de dados.
- SQLite: Sistema de banco de dados relacional leve e fácil de usar.
- SQL: Linguagem para manipulação dos dados no banco de dados.


---


### Instruções
Antes de começar, vamos organizar nosso setup.
* Fork esse repositório 
* Clone o fork na sua máquina (Para isso basta abrir o seu terminal e digitar `git clone url-do-seu-repositorio-forkado`)
* Entre na pasta do seu repositório (Para isso basta abrir o seu terminal e digitar `cd nome-do-seu-repositorio-forkado`)
* [Add outras intrucoes caso necessario]

### Conteúdo Extra

* [Conteúdo Extra: Uso de Funções Agregadas e Joins em SQLite ](./extra/readme.md)


## Introdução ao SQLite

SQLite é um sistema de gerenciamento de banco de dados relacional (SGBD) leve, autocontido e embutido. Ele é amplamente utilizado em aplicativos que requerem um banco de dados eficiente, sem a necessidade de um servidor separado.

#### Instalando e Importando o Módulo `sqlite3`

O módulo `sqlite3` é incluído na biblioteca padrão do Python, então não é necessário instalar pacotes adicionais. Para usá-lo, basta importá-lo no seu script Python:

```python
import sqlite3
```

#### Criando e Conectando ao Banco de Dados

Para conectar a um banco de dados SQLite, usamos a função `sqlite3.connect()`. Se o banco de dados não existir, ele será criado automaticamente.

```python
# Conectando ao banco de dados (ou criando, se não existir)
conn = sqlite3.connect('meu_banco_de_dados.db')

# Criando um cursor para executar comandos SQL
cursor = conn.cursor()
```

#### Executando Comandos SQL

A seguir, vamos aprender a executar comandos SQL básicos: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, e `JOIN`.

##### 1. Comando `SELECT`

O comando `SELECT` é usado para buscar dados no banco de dados.

```python
# Selecionando todos os registros de uma tabela
cursor.execute("SELECT * FROM minha_tabela")
resultados = cursor.fetchall()

# Exibindo os resultados
for linha in resultados:
    print(linha)
```

##### 2. Comando `INSERT`

O comando `INSERT` é usado para adicionar novos registros a uma tabela.

```python
# Inserindo um novo registro na tabela
cursor.execute("INSERT INTO minha_tabela (coluna1, coluna2) VALUES (?, ?)", (valor1, valor2))

# Salvando (commit) as mudanças
conn.commit()
```

##### 3. Comando `UPDATE`

O comando `UPDATE` é usado para modificar registros existentes.

```python
# Atualizando um registro existente
cursor.execute("UPDATE minha_tabela SET coluna1 = ? WHERE coluna2 = ?", (novo_valor1, valor2))

# Salvando as mudanças
conn.commit()
```

##### 4. Comando `DELETE`

O comando `DELETE` é usado para remover registros de uma tabela.

```python
# Removendo um registro da tabela
cursor.execute("DELETE FROM minha_tabela WHERE coluna1 = ?", (valor1,))

# Salvando as mudanças
conn.commit()
```

#### Usando `JOIN` e `LEFT JOIN`

O comando `JOIN` é utilizado para combinar registros de duas ou mais tabelas com base em uma coluna relacionada.

##### 1. Comando `JOIN`

```python
# Selecionando dados de duas tabelas relacionadas
cursor.execute("""
SELECT a.coluna1, b.coluna2
FROM tabela1 a
JOIN tabela2 b ON a.chave_estrangeira = b.id
""")
resultados = cursor.fetchall()

for linha in resultados:
    print(linha)
```

##### 2. Comando `LEFT JOIN`

O comando `LEFT JOIN` retorna todos os registros da tabela à esquerda e os registros correspondentes da tabela à direita. Se não houver correspondência, os resultados conterão `NULL`.

```python
# Selecionando dados com LEFT JOIN
cursor.execute("""
SELECT a.coluna1, b.coluna2
FROM tabela1 a
LEFT JOIN tabela2 b ON a.chave_estrangeira = b.id
""")
resultados = cursor.fetchall()

for linha in resultados:
    print(linha)
```

#### Fechando a Conexão

Após executar todos os comandos necessários, é importante fechar a conexão com o banco de dados.

```python
# Fechando o cursor e a conexão
cursor.close()
conn.close()
```

#### Exemplo Completo

Aqui está um exemplo completo que demonstra a criação de uma tabela, inserção, atualização, seleção, remoção de dados e uso de `JOIN`.

```python
import sqlite3

# Conectando ao banco de dados
conn = sqlite3.connect('exemplo.db')
cursor = conn.cursor()

# Criando uma tabela
cursor.execute("""
CREATE TABLE IF NOT EXISTS usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    idade INTEGER NOT NULL
)
""")

# Inserindo dados
cursor.execute("INSERT INTO usuarios (nome, idade) VALUES (?, ?)", ("Alice", 30))
cursor.execute("INSERT INTO usuarios (nome, idade) VALUES (?, ?)", ("Bob", 25))

# Atualizando dados
cursor.execute("UPDATE usuarios SET idade = ? WHERE nome = ?", (26, "Bob"))

# Selecionando dados
cursor.execute("SELECT * FROM usuarios")
for linha in cursor.fetchall():
    print(linha)

# Removendo dados
cursor.execute("DELETE FROM usuarios WHERE nome = ?", ("Alice",))

# Commit das mudanças
conn.commit()

# Fechando a conexão
cursor.close()
conn.close()
```

## Integração de CSV com SQLite usando Python

#### Introdução

Nesta seção, vamos aprender como integrar arquivos CSV com um banco de dados SQLite usando Python. Isso inclui ler dados de um arquivo CSV e inseri-los em um banco de dados SQLite, além de exportar dados do banco de dados para um arquivo CSV.

#### Bibliotecas Necessárias

Para este tutorial, vamos usar as bibliotecas `sqlite3` e `csv`, ambas inclusas na biblioteca padrão do Python. Certifique-se de que você tenha o Python instalado.

#### Instalando e Importando as Bibliotecas

Como `sqlite3` e `csv` são bibliotecas padrão do Python, não é necessário instalar pacotes adicionais. Para usá-las, basta importá-las no seu script Python:

```python
import sqlite3
import csv
```

#### Lendo Dados de um Arquivo CSV e Inserindo no SQLite

Vamos começar lendo dados de um arquivo CSV e inserindo-os em uma tabela do banco de dados SQLite.

##### 1. Criando a Tabela no SQLite

Primeiro, vamos criar uma tabela no banco de dados SQLite onde os dados do CSV serão armazenados. Suponha que temos um arquivo CSV chamado `dados.csv` com as colunas `nome` e `idade`.

```python
import sqlite3

# Conectando ao banco de dados SQLite (ou criando se não existir)
conn = sqlite3.connect('exemplo.db')
cursor = conn.cursor()

# Criando a tabela
cursor.execute("""
CREATE TABLE IF NOT EXISTS usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    idade INTEGER NOT NULL
)
""")

# Salvando as mudanças
conn.commit()
```

##### 2. Lendo o Arquivo CSV e Inserindo Dados na Tabela

Agora, vamos ler o arquivo CSV e inserir os dados na tabela `usuarios`.

```python
import csv
import sqlite3

# Conectando ao banco de dados
conn = sqlite3.connect('exemplo.db')
cursor = conn.cursor()

# Abrindo o arquivo CSV
with open('dados.csv', 'r') as arquivo_csv:
    leitor_csv = csv.reader(arquivo_csv)
    
    # Pulando o cabeçalho
    next(leitor_csv)
    
    # Inserindo cada linha do CSV na tabela
    for linha in leitor_csv:
        cursor.execute("INSERT INTO usuarios (nome, idade) VALUES (?, ?)", (linha[0], int(linha[1])))

# Salvando as mudanças
conn.commit()

# Fechando a conexão
cursor.close()
conn.close()
```

#### Exportando Dados do SQLite para um Arquivo CSV

Vamos exportar dados da tabela `usuarios` para um arquivo CSV.

```python
import csv
import sqlite3

# Conectando ao banco de dados
conn = sqlite3.connect('exemplo.db')
cursor = conn.cursor()

# Selecionando todos os dados da tabela
cursor.execute("SELECT nome, idade FROM usuarios")
dados = cursor.fetchall()

# Escrevendo os dados para um arquivo CSV
with open('exportados.csv', 'w', newline='') as arquivo_csv:
    escritor_csv = csv.writer(arquivo_csv)
    
    # Escrevendo o cabeçalho
    escritor_csv.writerow(['nome', 'idade'])
    
    # Escrevendo os dados
    escritor_csv.writerows(dados)

# Fechando a conexão
cursor.close()
conn.close()
```

#### Exemplo Completo

Aqui está um exemplo completo que demonstra como ler dados de um arquivo CSV e inseri-los no SQLite, e como exportar dados do SQLite para um arquivo CSV.

```python
import sqlite3
import csv

# Função para criar a tabela no SQLite
def criar_tabela(conn):
    cursor = conn.cursor()
    cursor.execute("""
    CREATE TABLE IF NOT EXISTS usuarios (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        nome TEXT NOT NULL,
        idade INTEGER NOT NULL
    )
    """)
    conn.commit()

# Função para inserir dados do CSV no SQLite
def importar_csv_para_sqlite(arquivo_csv, conn):
    cursor = conn.cursor()
    with open(arquivo_csv, 'r') as csv_file:
        leitor_csv = csv.reader(csv_file)
        next(leitor_csv)  # Pular o cabeçalho
        for linha in leitor_csv:
            cursor.execute("INSERT INTO usuarios (nome, idade) VALUES (?, ?)", (linha[0], int(linha[1])))
    conn.commit()

# Função para exportar dados do SQLite para CSV
def exportar_sqlite_para_csv(arquivo_csv, conn):
    cursor = conn.cursor()
    cursor.execute("SELECT nome, idade FROM usuarios")
    dados = cursor.fetchall()
    with open(arquivo_csv, 'w', newline='') as csv_file:
        escritor_csv = csv.writer(csv_file)
        escritor_csv.writerow(['nome', 'idade'])  # Cabeçalho
        escritor_csv.writerows(dados)

# Conectando ao banco de dados SQLite
conn = sqlite3.connect('exemplo.db')

# Criando a tabela
criar_tabela(conn)

# Importando dados do CSV para o SQLite
importar_csv_para_sqlite('dados.csv', conn)

# Exportando dados do SQLite para CSV
exportar_sqlite_para_csv('exportados.csv', conn)

# Fechando a conexão
conn.close()
```


***
### Exercícios 
* [Exercicio para sala](https://github.com/reprograma/on29-python-s08-banco-de-dados-II/tree/main/exercicios/para-sala)
* [Exercicio para casa](https://github.com/reprograma/on29-python-s08-banco-de-dados-II/tree/main/exercicios/para-casa)


<p align="center">
Desenvolvido com :purple_heart:  
</p>

