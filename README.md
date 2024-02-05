⭐️para criar um banco de dados no my sql precisamos do seguinte comando
criação do banco: create database banco;
create table if not exists bancoteste(
id int not null auto_increment,                 # isso é para criar a chave primaria
nome varchar(15) not null,
nascimento data,
profissao varchar(30),
sexo enum('M', 'F'),
primary key (id);                               # isso é para definir a chave primaria
) default charset= utf8;



⭐️Para inserir valores dentro da tabela precimos usar o insert into

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






⭐️Comando relacionados ao alter table(serve para mudar a tabela e modificar os dados da coluna)


Mudar nome: 
alter table bancoteste
raname nome to usuario;

Adicionar colunas:
alter table bancoteste
add column comidafavorita varchar(50);              voce tambem pode adicionar tanto o after ou first depois pra organizar melhor onde botar

Para modificar os dados da coluna use:
alter table bancoteste
modify column comidafavorita varchar(35);

Para mudar o nome da tabela em especifico use:
alter table
change column profissao prof varchar(30);

Alterar o nome da tabela:
alter table bancoteste
rename to amigos;

Para apagar a coluna use:
drop column profissao;


⭐️Agora vamos aprender sobre Update, DELETE e Truncate
o update serve para setar um valor especifico na tabela

um exemplo claro é esse:

update bancoteste
set nome = 'matheus'                                       #  set é pra setar oque voce vai querer mudar
where id = '1'                                           #  where é pra dizer de onde? onde vou mudar
limit 1;                                                 #  limit é pra dizer quantos é pra mudar(serve para a segurança)

Caso deseje alterar mais de uma coisa na coluna é simples faça isso:
update bancoteste
set nome = 'matheus', nascimento = '1978-09-18', profissão = 'medico contrabandista'
where id = '1';

Agora vamos a exemplos para usar o delete

Delete from bancoteste
where id = '1';

Delete from bancoteste
where ano = '2018'                                 #aqui ele vai excluir os bancos de dados que tem como parametro o ano de 2018
limit 3;


O uso agora o truncate é bem simples ele vai só APAGAR KKKKKKK TUDO.....
exemplo de uso
truncate table bancoteste


⭐️Agora vou falar sobre o select, tu vai usar da seguinte forma

select nome, nascimento, carga from bancoteste                            # aqui tu vai selecionar só nome, nascimento e carga do bancoteste
where ano = 2016                                                          # só vai filtrar do ano 2016
order by nome, profissao                                                  # ordendando por nome e profissao


tambem temos esse:

select nome, ano from bancoteste
where ano between 2014 and 2016;                                               #  vai selecionar os anos de 2014 entre 2016


select * from bancoteste
where ano in (2016,2017)                             #  vai selecinar tudo relacionado a 2016 e 2017 e foda-se o resto
order by nome


Vamos ver agora as filtragens de valores

select * from cursos
where nome like '%p'                                           # se for %p vai ter qualquer coisa e p no final, se for p% vai ter p no inicio, se for %p% vai ter p em qualquer parte e tbm pode se usar o _ 


select distinct nacionalidade from gafanhotos                  #serve para filtrar os paises que foram cadastrados

                                            
select count(*) from cursos                               # serve para contar tudo de cursos, quantas linhas foram cadastradas

select max(nome) from curso                              # serve para ver o total de nomes, ou o minimo usando min, ou a media usando avg



⭐️Ultima aula de select vamos fazer o seguinte:

OBS:Distinct serve exclusivamente para distinguir certas linhas como uma pessoa de 32 anos, se eu n quiser mais ver ela use o distinct.
OBS: Caso voce queira agrupar esses grupos faça o seguinte:

select carga from cursos
group by carga;                                                  isso vai fazer com que voce agrupe tudo que se relaciona a cargas.


Agora para melhorarmos ainda mais vamos usar a agrupamento & agregação
da seguinte forma

select from carga count(nome) from cursos


select nome, altura,peso from gafanhotos where peso > 100 and altura > 1.93        aqui eu agrupei geral com mais de 100 kilos e com media da altura da galera e peguei os acima da media



⚿⭐️ Modelo relacional

group by carga;

aqui esta uma das atividades que fiz no curso

🔑chave primaria é o formato id ou idcurso ou cpf, algo unico

🗝️A chave estrangeira é quando vamos relacionar tabelas, é quanto uma chave primaria de uma tabela vai fazer parte de outra tabela, fazendo assim que ela
deixe de ser uma chave primaria e venha a existir como uma chave estrangeira

Agora vamos aprender a dividir as chaves, entre 1 pra n(n é muitos), tipo um gerente para um funcionario, o 1 seria o gerente pois ele é quem vai comandar e o n os funcionarios
se for por exemplo 1 para 1, marido e mulher
se for por exemplo tambem n para n cliente e produto


Para isso vamos pegar visao assim, se liga:
1 para 1= id primarios de um vai pra um e do outro vai pra outro como chave estranheira.
1 para n= o id primario do 1 vai para o n como chave estranheira.
n para n = vai botar o id tanto do n tanto do outro n no meio deles, tipo cliente compra e produto o id do cliente e do produto vão para a compra.

⭐️Agora vamos ver como se usa o join, cuida pai.
OBS: Os exemplos que utilizarei aqui em baixo é referente a uma aula do curso em video do professor guanabara.

primeiramente vamos adicionar uma coluna que sera a chave estranheira
usaremos:
alter table gafanhotos add column cursopreferido int;       se liga que o cursopreferido é a chave estranheira

Agora para setar que ela é uma chave estrangeira usaremos

alter table gafanhotos
add foreing key(cursopreferido)
references cursos(idcursos);

Beleza, depois desse comando a gente setou a chave primaria, para conferir ela deve ter um MUL na tabela

obs: Join significa em sql junção

Agora para fazer-mos a ligação dessa tabela vamos fazer o seguinte:

select gafanhotos.nome, gafanhotos.cursopreferido,cursos.nome, cursos.ano 
from gafanhotos an g join cursos an c                                                     agora caso queira vc pode simplesmente trocar o gafanhotos por g na linha de cima
on cursos.idcurso = gafanhotos.cursopreferido                                             isso é para filtrar que será apenas os que tem ligação e não mostrar tudo(on)





⭐️Agora assim, caso voce queira ver todos que estão em ligação de tabelas e os que tbm não estão faz o seguinte

select gafanhotos.nome, gafanhotos.cursopreferido, cursos.nome, cursos.ano
from gafanhotos left outer join cursos                                              a partir dessa linha vc vai ver os que tem um curso favorito e os que não tem um curso favorito
on cursos.idcursos = gafanhotos.cursopreferido


⭐️⭐️⭐️Final

Aqui vamos fazer uma ligação de n para n vamos fazer o seguinte

create table ganahotos_assiste_curso(
id int not null auto_increment,
data date,
idgafanhotos int,                               essa é a criação da chave estranheira
idcurso int,                                    essa é a outra, vamos setar as duas agora com:
primary key(id),
foreing key(idgafanhotos) references gafanhotos(id)
foreing key(idcurso) references cursos(idcurso)
) default charset= utf8;

agora voce vai insesrir na tabela ganahotos_assiste_curso alguns dados

logo após vamos lincar as 3 tabelas em suas respectivas tabelas da seguinte forma

select * from gafanhotos g                   aqui selecionei tudo mais vc pode selecionar por nome, id, etc tipo g.nome, c.nome
join ganahotos_assiste_curso a
on g.id = a.idgafanhotos
join cursos c                               aqui vamos ligar com quais cursos o meliante anda fazendo
on a.idcurso = c.idecurso                   aqui lincamos os id das duas colunas

e logo mais é isso galerinha, um beijo e um queijo hihi.

*  #######  #######  ##   ##  ######   ###  ##  #######           #######  #######           #######  #######  #######  #######  ####### *
*                ##  ##   ##    ##     #### ##                         ##                         ##       ## *
*  ##       #######  #######    ##     ## ####  ##   ##           ##   ##  ####              #######  ##   ##  #######  ####     ####### *
*  ##       ##  ##        ##    ##     ##  ###  ##    #           ##   ##  ##                ##  ##   ##   ##       ##  ##            ## *
*  #######  ##   ##  #######  ######   ##   ##  #######           #######  ##                ##   ##  #######  #######  #######  ####### *



.
