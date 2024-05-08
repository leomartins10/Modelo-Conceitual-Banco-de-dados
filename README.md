# Modelo Conceitual Banco de dados
<img src="Modelo Conceitual do Banco de Dados.png">
### Documentação do Script SQL

Aqui está uma documentação detalhada do script SQL que você forneceu, explicando cada comando e sua função dentro do contexto de criação de um banco de dados para um sistema educacional ou similar:

---

#### Comandos Iniciais

```sql
-- Drop tables if they exist to start fresh
DROP TABLE IF EXISTS feedbacks, habilidades, aluno, professor, time, usuario;
```

**Descrição:**
Este comando é usado para garantir que o ambiente de banco de dados esteja limpo antes de criar novas tabelas. Ele remove as tabelas especificadas se já existirem, evitando erros de criação devido à presença de tabelas com o mesmo nome.

---

#### Criação da Tabela `usuario`

```sql
CREATE TABLE usuario (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(255),
  idade INT,
  nacionalidade VARCHAR(255),
  universidade VARCHAR(255),
  email VARCHAR(255) UNIQUE,
  senha VARCHAR(255)
);
```

**Descrição:**
Esta tabela armazena informações básicas dos usuários do sistema. 

- `id`: Um identificador único para cada usuário, que se autoincrementa automaticamente.
- `nome`: Nome do usuário.
- `idade`: Idade do usuário.
- `nacionalidade`: Nacionalidade do usuário.
- `universidade`: Nome da universidade à qual o usuário está associado, se aplicável.
- `email`: Endereço de email do usuário, que deve ser único no sistema.
- `senha`: Senha do usuário para acesso ao sistema.

---

#### Criação da Tabela `habilidades`

```sql
CREATE TABLE habilidades (
  id INT AUTO_INCREMENT PRIMARY KEY,
  habilidade1 VARCHAR(255),
  habilidade2 VARCHAR(255),
  habilidade3 VARCHAR(255)
);
```

**Descrição:**
Esta tabela é destinada a armazenar diferentes habilidades que podem ser associadas aos usuários.

- `id`: Um identificador único para cada conjunto de habilidades.
- `habilidade1`, `habilidade2`, `habilidade3`: Descrições textuais de habilidades individuais.

---

#### Criação da Tabela `time`

```sql
CREATE TABLE time (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(255),
  descricao VARCHAR(255)
);
```

**Descrição:**
Esta tabela guarda informações sobre diferentes equipes ou grupos dentro do sistema.

- `id`: Um identificador único para cada time.
- `nome`: Nome do time.
- `descricao`: Uma breve descrição do time.

---

#### Criação da Tabela `aluno`

```sql
CREATE TABLE aluno (
  id INT AUTO_INCREMENT PRIMARY KEY,
  usuario_id INT,
  habilidades_id INT,
  time_id INT,
  FOREIGN KEY (usuario_id) REFERENCES usuario(id),
  FOREIGN KEY (habilidades_id) REFERENCES habilidades(id),
  FOREIGN KEY (time_id) REFERENCES time(id)
);
```

**Descrição:**
Esta tabela conecta os alunos às tabelas `usuario`, `habilidades`, e `time`.

- `id`: Identificador único para cada aluno.
- `usuario_id`: Chave estrangeira que conecta o aluno ao seu registro na tabela `usuario`.
- `habilidades_id`: Chave estrangeira que associa o aluno a um conjunto específico de habilidades na tabela `habilidades`.
- `time_id`: Chave estrangeira que associa o aluno a um time específico.

---

#### Criação da Tabela `professor`

```sql
CREATE TABLE professor (
  id INT AUTO_INCREMENT PRIMARY KEY,
  usuario_id INT,
  time_id INT,
  FOREIGN KEY (usuario_id) REFERENCES usuario(id),
  FOREIGN KEY (time_id) REFERENCES time(id)
);
```

**Descrição:**
Armazena informações dos professores e os conecta a usuários e times.

- `id`: Identificador único para cada professor.
- `usuario_id`: Conecta o professor ao seu perfil de usuário.
- `time_id`: Associa o professor a um time específico.

---

#### Criação da Tabela `feedbacks`

```sql
CREATE TABLE feedbacks (
  id INT AUTO_INCREMENT PRIMARY KEY,
  autor_id INT,
  destinatario_id INT,
  conteudo TEXT,
  FOREIGN KEY (autor_id) REFERENCES usuario(id),
  FOREIGN KEY (destinatario_id) REFERENCES usuario(id)
);
```

**Descrição:**
Esta tabela é usada para armazenar feedbacks entre usuários.

- `id`: Identificador único para cada feedback.
- `autor_id`: Identifica o usuário que escreveu o feedback.
- `destinatario_id`: Identifica o usuário que recebeu o feedback.


- `conteudo`: O texto do feedback.

---

### Considerações Finais

Este script SQL cria uma estrutura básica de banco de dados para um sistema que envolve usuários, suas habilidades, e suas interações em times e feedbacks. A estrutura está projetada para ser extensível e adaptável às necessidades de diferentes aplicações que possam requerer gerenciamento de usuários, habilidades, e grupos.
