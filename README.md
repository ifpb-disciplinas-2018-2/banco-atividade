## Consultas


Em grupos de (até) três alunos realizem as seguintes atividades:

### Primeira atividade

A primeira etapa da atividade consiste em realizar o processo de engenharia reversa. Ou seja, tendo acesso as tabelas vamos desenvolver o mapeamento relacional e lógico. É preciso criar o diagrama entidade relacionamento! 

```sql
CREATE TABLE departamento(
  id integer NOT NULL,
  abreviacao character varying(255),
  PRIMARY KEY (id)
);


CREATE TABLE endereco(
  id integer NOT NULL,
  bairro character varying(255),
  cidade character varying(255),
  rua character varying(255),
  PRIMARY KEY (id)
);

CREATE TABLE funcionario(
  id integer NOT NULL,
  cpf character varying(255),
  nome character varying(255),
  departamento_id integer,
  end_cod integer,
  salario double precision,
  PRIMARY KEY (id),
  FOREIGN KEY (departamento_id) REFERENCES departamento (id) 
  FOREIGN KEY (end_cod) REFERENCES endereco (id) 
);


CREATE TABLE dependente(
  codigo integer NOT NULL,
  nome character varying(255),
  funcionario_id integer,
  PRIMARY KEY (codigo),
  FOREIGN KEY (funcionario_id) REFERENCES funcionario (id)
);

CREATE TABLE gerente(
  id integer NOT NULL,
  cpf character varying(255),
  fim date,
  inicio date,
  nome character varying(255),
  dep_id integer,
  PRIMARY KEY (id),
  FOREIGN KEY (dep_id) REFERENCES departamento (id)     
);

CREATE TABLE projeto(
  id integer NOT NULL,
  descricao character varying(255),
  gerente_id integer,
  PRIMARY KEY (id),
  FOREIGN KEY (gerente_id) REFERENCES gerente (id) 
);

CREATE TABLE alocacao(
  funcionarios_id integer NOT NULL,
  projetos_id integer NOT NULL,
  PRIMARY KEY (funcionarios_id, projetos_id),
  FOREIGN KEY (funcionarios_id) REFERENCES funcionario (id),
  FOREIGN KEY (projetos_id) REFERENCES projeto (id) 
);
```

### Segunda atividade

A segunda etapa da atividade consiste em realizar um conjunto de consultas na base de dados criada. Para tal, vamos utilizar os seguintes dados:

```sql
INSERT INTO departamento VALUES (7, 'UNINFO');
INSERT INTO departamento VALUES (14, 'UNIND');
INSERT INTO endereco VALUES (1, 'Meu bairro', 'Minha cidade', 'Minha rua');
INSERT INTO endereco VALUES (11, 'bairro', 'cidade', 'rua 1');
INSERT INTO endereco VALUES (10, 'bairro', 'cidade', 'rua');
INSERT INTO funcionario VALUES (12, '1354', 'Kiko', NULL, 11, 1200);
INSERT INTO funcionario VALUES (9, '124', 'Florinda', 7, 1, 980);
INSERT INTO funcionario VALUES (8, '123', 'Madruga', 7, 1, 980);
INSERT INTO funcionario VALUES (4, '134', 'Chaves', NULL, 10, 1500);
INSERT INTO gerente VALUES (15, '123', '2019-04-05', '2019-03-19', 'Job', 7);
INSERT INTO projeto VALUES (13, 'SD', 15);
INSERT INTO projeto VALUES (5, 'Banco de Dados', 15);
INSERT INTO projeto VALUES (6, 'POO', NULL);
INSERT INTO alocacao VALUES (4, 5);
INSERT INTO alocacao VALUES (12, 5);
INSERT INTO alocacao VALUES (4, 13);
INSERT INTO dependente VALUES (18, 'Tulio', NULL);
INSERT INTO dependente VALUES (17, 'jose', NULL);
INSERT INTO dependente VALUES (16, 'Godiles', 8);
INSERT INTO dependente VALUES (2, 'Chiquinha', 8);
INSERT INTO dependente VALUES (3, 'Mariana', 4);
```

Segue lista de consultas:

* Selecionar todos os Funcionarios;
* Selecionar o Departamento com id igual 6;
* Selecionar a abreviação do Departamento e o seu Gerente;
* Selecionar o nomes dos Funcionarios que possuem Dependentes;
* Selecionar o nomes dos Funcionarios e dos seus respectivos Dependentes;
* Selecionar o nomes dos Funcionarios e quantidade de seus Dependentes;
* Selecionar o nome em maiusculo dos Dependentes que possuem id entre 15 e 17;
* Selecionar os Departamentos que não possuem Gerente; 
* Selecionar o nome dos Funcionarios que possuem Dependentes e o nome do Dependente começa com a letra `M`;
* Selecionar o nome do funcionario que recebe o maior salario entre todos os funcionarios;
 