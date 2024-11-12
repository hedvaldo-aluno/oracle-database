### 1. **CREATE TABLE**
   O `CREATE TABLE` cria uma nova tabela no banco de dados com colunas e tipos de dados definidos.

   ```sql
   -- Cria a tabela 'funcionarios' com colunas para id, nome, idade e salário
   CREATE TABLE funcionarios (
       id INT PRIMARY KEY,            -- 'id' é a chave primária (única e não nula)
       nome VARCHAR(50),               -- 'nome' é um texto com até 50 caracteres
       idade INT,                      -- 'idade' é um número inteiro
       salario DECIMAL(10, 2)          -- 'salario' é um valor decimal com 10 dígitos, sendo 2 após a vírgula
   );
   ```

### 2. **CONSTRAINT**
   `CONSTRAINT` é usado para definir regras sobre os dados, como valores únicos ou obrigatórios.

   ```sql
   -- Cria a tabela 'departamentos' e aplica uma restrição de unicidade na coluna 'nome'
   CREATE TABLE departamentos (
       id INT PRIMARY KEY,                          -- 'id' é a chave primária
       nome VARCHAR(50) CONSTRAINT nome_unico UNIQUE -- 'nome' deve ser único em cada linha
   );
   ```

### 3. **FOREIGN KEY**
   Define uma chave estrangeira que estabelece um vínculo entre tabelas.

   ```sql
   -- Cria a tabela 'empregados' com uma chave estrangeira ligada a 'departamentos'
   CREATE TABLE empregados (
       id INT PRIMARY KEY,
       nome VARCHAR(50),
       departamento_id INT,
       CONSTRAINT fk_departamento FOREIGN KEY (departamento_id) REFERENCES departamentos(id)
       -- 'departamento_id' deve ter um valor existente na coluna 'id' da tabela 'departamentos'
   );
   ```

### 4. **PRIMARY KEY**
   Define a coluna (ou colunas) como uma chave primária, que deve ser única e não nula.

   ```sql
   -- Cria a tabela 'clientes' com 'cliente_id' como chave primária
   CREATE TABLE clientes (
       cliente_id INT PRIMARY KEY,
       nome VARCHAR(50)
   );
   ```

### 5. **SELECT**
   Recupera dados de uma ou mais tabelas.

   ```sql
   -- Seleciona as colunas 'nome' e 'idade' da tabela 'funcionarios'
   SELECT nome, idade FROM funcionarios;
   ```

### 6. **INSERT INTO**
   Insere novos dados em uma tabela.

   ```sql
   -- Insere uma nova linha na tabela 'funcionarios'
   INSERT INTO funcionarios (id, nome, idade, salario) VALUES (1, 'Maria', 30, 4000.00);
   ```

### 7. **UPDATE**
   Atualiza dados existentes em uma tabela.

   ```sql
   -- Atualiza o salário de 'Maria' para 4500.00
   UPDATE funcionarios SET salario = 4500.00 WHERE nome = 'Maria';
   ```

### 8. **SET**
   Usado junto com `UPDATE` para definir novos valores.

   ```sql
   -- Atualiza a idade de 'Maria' para 31
   UPDATE funcionarios SET idade = 31 WHERE nome = 'Maria';
   ```

### 9. **ALTER TABLE**
   Modifica a estrutura de uma tabela existente.

   ```sql
   -- Adiciona uma nova coluna 'endereco' na tabela 'funcionarios'
   ALTER TABLE funcionarios ADD endereco VARCHAR(100);
   ```

### 10. **WHERE**
   Especifica condições para filtrar os dados retornados ou atualizados.

   ```sql
   -- Seleciona funcionários com idade acima de 30 anos
   SELECT * FROM funcionarios WHERE idade > 30;
   ```

### 11. **AS**
   Renomeia temporariamente colunas ou tabelas.

   ```sql
   -- Seleciona o nome dos funcionários e o renomeia temporariamente para 'funcionario_nome'
   SELECT nome AS funcionario_nome FROM funcionarios;
   ```

### 12. **LIKE**
   Usa padrões com caracteres coringa (`%` e `_`) para comparar texto.

   ```sql
   -- Seleciona funcionários cujo nome começa com a letra 'M'
   SELECT * FROM funcionarios WHERE nome LIKE 'M%';
   ```

### 13. **BETWEEN**
   Filtra valores dentro de um intervalo, inclusive dos limites.

   ```sql
   -- Seleciona funcionários com salário entre 3000 e 5000
   SELECT * FROM funcionarios WHERE salario BETWEEN 3000 AND 5000;
   ```

### 14. **NOT IN**
   Exclui valores de uma lista específica.

   ```sql
   -- Seleciona funcionários cujo 'departamento_id' não está nas opções 1, 2 ou 3
   SELECT * FROM funcionarios WHERE departamento_id NOT IN (1, 2, 3);
   ```

### 15. **count()**
   Conta o número de linhas no resultado.

   ```sql
   -- Conta o número de funcionários
   SELECT COUNT(*) FROM funcionarios;
   ```

### 16. **max()**
   Retorna o valor máximo de uma coluna.

   ```sql
   -- Obtém o maior salário entre os funcionários
   SELECT MAX(salario) FROM funcionarios;
   ```

### 17. **min()**
   Retorna o valor mínimo de uma coluna.

   ```sql
   -- Obtém o menor salário entre os funcionários
   SELECT MIN(salario) FROM funcionarios;
   ```

### 18. **avg()**
   Calcula a média dos valores de uma coluna.

   ```sql
   -- Calcula o salário médio dos funcionários
   SELECT AVG(salario) FROM funcionarios;
   ```

### 19. **ORDER BY**
   Ordena os resultados com base em uma ou mais colunas.

   ```sql
   -- Ordena funcionários por salário em ordem decrescente
   SELECT * FROM funcionarios ORDER BY salario DESC;
   ```

### 20. **GROUP BY**
   Agrupa linhas com valores comuns em uma coluna e permite a aplicação de funções de agregação.

   ```sql
   -- Agrupa os funcionários por 'departamento_id' e calcula a média salarial de cada departamento
   SELECT departamento_id, AVG(salario) FROM funcionarios GROUP BY departamento_id;
   ```

### 21. **HAVING**
   Aplica condições em grupos após uma agregação.

   ```sql
   -- Filtra departamentos onde a média salarial é superior a 4000
   SELECT departamento_id, AVG(salario) FROM funcionarios GROUP BY departamento_id HAVING AVG(salario) > 4000;
   ```

### 22. **CONSULTAS ANINHADAS (SUBQUERIES)**
   Uma consulta dentro de outra consulta para fornecer resultados específicos.

   ```sql
   -- Seleciona funcionários com salário acima da média de todos os funcionários
   SELECT * FROM funcionarios WHERE salario > (SELECT AVG(salario) FROM funcionarios);
   ```

### 23. **exists**
   Verifica a existência de resultados em uma subconsulta.

   ```sql
   -- Seleciona departamentos que têm funcionários associados
   SELECT * FROM departamentos WHERE EXISTS (SELECT * FROM funcionarios WHERE departamento_id = departamentos.id);
   ```

### 24. **not exists**
   Verifica a ausência de resultados em uma subconsulta.

   ```sql
   -- Seleciona departamentos que não têm funcionários associados
   SELECT * FROM departamentos WHERE NOT EXISTS (SELECT * FROM funcionarios WHERE departamento_id = departamentos.id);
   ```

### 25. **Tipos de JOIN**
   Combina registros de tabelas relacionadas.

   - **INNER JOIN**: Retorna registros que têm correspondência nas duas tabelas.

     ```sql
     -- INNER JOIN: Retorna somente os registros que têm correspondência nas duas tabelas ('funcionarios' e 'departamentos')
     SELECT funcionarios.nome, departamentos.nome AS departamento
     FROM funcionarios
     INNER JOIN departamentos ON funcionarios.departamento_id = departamentos.id;
     ```

   - **LEFT JOIN**: Retorna todos os registros da tabela à esquerda e correspondências da tabela à direita.

      ```sql
      -- incluindo os registros que não têm correspondência na tabela à direita ('departamentos').
      SELECT funcionarios.nome, departamentos.nome AS departamento
      FROM funcionarios
      LEFT JOIN departamentos ON funcionarios.departamento_id = departamentos.id;
      ```

   - **RIGHT JOIN**: Retorna todos os registros da tabela à direita e correspondências da tabela à esquerda.

     ```sql
       -- incluindo os registros que não têm correspondência na tabela à esquerda ('funcionarios').
      SELECT funcionarios.nome, departamentos.nome AS departamento
      FROM funcionarios
      RIGHT JOIN departamentos ON funcionarios.departamento_id = departamentos.id;
     ```

   - **FULL JOIN**: Retorna todos os registros quando há correspondência em qualquer tabela.

     ```sql
       -- Inclui registros não correspondentes de ambas as tabelas ('funcionarios' e 'departamentos').
      SELECT funcionarios.nome, departamentos.nome AS departamento
      FROM funcionarios
      FULL JOIN departamentos ON funcionarios.departamento_id = departamentos.id;
     ```
