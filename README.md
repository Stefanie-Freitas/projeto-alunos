# projeto-alunos

import sqlite3

# Conectar ao banco de dados
conn = sqlite3.connect('Banco');
cursor = conn.cursor();

# Criar tabela se não existir
cursor.execute('''
    CREATE TABLE IF NOT EXISTS alunos (
        id INTEGER PRIMARY KEY,
        nome TEXT,
        idade INTEGER,
        curso TEXT )''');

# Inserir registros na tabela de alunos (sem especificar IDs)
cursor.execute('''INSERT INTO alunos (nome, idade, curso) VALUES 
                  ('Camila', 20, 'Dados'),
                  ('Maria', 22, 'Dados'),
                  ('Joana', 24, 'Engenharia'),
                  ('Clara', 25, 'Dados'),
                  ('Simone', 30, 'Engenharia')''')

# Criar tabela se não existir

cursor.execute('''CREATE TABLE IF NOT EXISTS clientes (id INTEGER primary key, nome VARCHAR(250), idade INTEGER, saldo FLOAT)''')

# Inserir registros na tabela de clientes ver ID
cursor.execute('''insert into clientes (nome, idade, saldo) values ("Camila", 20, 1000), ("Maria", 33, 200), ("Joana", 24, 500), ("Clara", 40, 1200), ("Simone", 30, 300)''')

conn.commit()

cursor.execute('''select * from alunos''')

cursor.execute('''select nome, idade from alunos where idade > 20''')

cursor.execute('''select * from alunos where curso = "Engenharia" order by nome''')

cursor.execute('''select count(*) from alunos''')

cursor.execute('''update alunos set idade = 28 where id = 1''')

cursor.execute('''delete from alunos where id = 1''')


# Conectar ao banco de dados

import sqlite3

conn = sqlite3.connect('Banco');
cursor = conn.cursor();

## Calcule o saldo médio dos clientes.
cursor.execute('''select AVG(saldo) from clientes''')

#c) Encontre o cliente com o saldo máximo.
cursor.execute('''select nome from clientes where saldo = (select max(saldo) from clientes)''')

#d) Conte quantos clientes têm saldo acima de 1000.
cursor.execute('''select count(*) from clientes where saldo >=1000''')

#7. Atualização e Remoção com Condições
#a) Atualize o saldo de um cliente específico.
cursor.execute('''update clientes set saldo = 2000 where id =1''')

#b) Remova um cliente pelo seu ID.
cursor.execute('''delete from clientes where id = 1''')

#8. Junção de Tabelas
#Crie uma segunda tabela chamada "compras" com os campos: id (chave primária), cliente_id (chave estrangeira referenciando o id da tabela "clientes"), produto (texto) e valor (real).
cursor.execute('''create table compras (id INTEGER primary key, cliente_id INTEGER, produto VARCHAR(250), valor FLOAT, CONSTRAINT fk_clientes FOREIGN KEY (cliente_id) REFERENCES clientes (id))''')
cursor.execute('''insert into compras (id, cliente_id, produto, valor) values (1,1, 'caderno', 20.0), (2,1,"caneta", 1.10), (3, 2, "caderno", 2.0)''')

# Insira algumas compras associadas a clientes existentes na tabela "clientes". Escreva uma consulta para exibir o nome do cliente, o produto e o valor de cada compra.
cursor.execute('''select c.nome, co.produto, co.valor from compras as co inner join clientes as c on c.id = co.cliente_id''')
for item in result:
    print(item)


# as informações só são enviadas quando chegar nesse comando
conexao.commit()

# encerra o processo
conexao.close

# Fechar a conexão com o banco de dados
# conn.close()

