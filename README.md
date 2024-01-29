para criar um banco de dados no my sql precisamos do seguinte comando
criação do banco: create database banco;
create table if not exists bancoteste(
id int not null auto_increment,                  isso é para criar a chave primaria
nome varchar(15) not null,
nascimento data,
profissao varchar(30),
sexo enum('M', 'F'),
primary key (id);                                isso é para definir a chave primaria
) default charset= utf8;



Para inserir valores dentro da tabela precimos usar o insert into

tipo:
insert into bancoteste values 
('default', 'josé', '1998-04-15', 'corno', 'M')


ou tambem caso deseje voce tbm pode fazer assim:


insert into bancoteste
(id,nome,nascimento,profissao,sexo)
values
('default', 'josé', '1998-04-15', 'corno', 'M')

---------------------------
Dois comandos muito importante para ver a database, abrir tabelas e ver colunas
use bancoteste,   desc/describe bancoteste, select * from bancoteste
---------------------------






Comando relacionados ao alter table(serve para mudar a tabela e modificar os dados da coluna)


Mudar nome: 
alter table bancoteste
raname nome to usuario;

Adicionar colunas:
alter table bancoteste
add column comidafavorita varchar(50);

Para modificar os dados da coluna use:
alter table bancoteste
modify column comidafavorita varchar(35);

Alterar o nome da tabela:
alter table bancoteste
rename to amigos;

Para apagar a coluna use:
drop column profissao;


