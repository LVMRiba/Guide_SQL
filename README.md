Guia de comandos para SQL

fore_name: Nome Próprio
last_name: Sobrenome
state: Unidade Federativa

## SELECIONAR COLUNAS
SELECT fore_name, last_name FROM pessoas;

## SELECIONAR TODAS AS COLUNAS
SELECT * FROM pessoas;

## SELECIONAR COLUNAS COM CONDIÇÕES (WHERE, AND, OR, WHERE NOT)
SELECT fore_name, last_name FROM pessoas WHERE state = 'RJ';
SELECT fore_name, last_name FROM pessoas WHERE state = 'RJ' AND city='Rio de Janeiro';
SELECT fore_name, last_name FROM pessoas WHERE state = 'RJ' AND city='Rio de Janeiro' AND color='blue';
SELECT fore_name, last_name FROM pessoas WHERE state = 'RJ' OR state = 'SP'
SELECT fore_name, last_name, state  FROM pessoas WHERE state = 'SP' OR state = 'MG'
SELECT fore_name, last_name, nome_time, state FROM pessoas WHERE NOT (state = 'SP')
SELECT fore_name, last_name, nome_time, state FROM pessoas WHERE state <> 'SP'
SELECT fore_name, last_name, state, nome_time FROM pessoas WHERE nome_time = 'vermelho' AND state = 'SP' OR state = 'MG'
SELECT fore_name, last_name, state, nome_time FROM pessoas WHERE nome_time = 'vermelho' AND (state = 'SP' OR state = 'MG' )

## SELECIONAR COLUNAS COM CONDIÇÕES (LIKE)
SELECT fore_name, last_name, state from Pessoas WHERE state LIKE 'S%'
SELECT fore_name, last_name, state from Pessoas WHERE state LIKE '%O'
SELECT fore_name, last_name, state FROM pessoas WHERE fore_name LIKE '%DANI%';
SELECT fore_name, last_name, state FROM pessoas WHERE fore_name LIKE '%DANI%' LIMIT 2
SELECT fore_name, last_name, state FROM pessoas WHERE fore_name LIKE '%DANI%' LIMIT 2 OFFSET 2

## ORDENAÇÃO (BY) POR (ASC, DESC)
SELECT fore_name, last_name FROM pessoas ORDER BY fore_name
SELECT fore_name, last_name FROM pessoas ORDER BY fore_name ASC
SELECT fore_name, last_name FROM pessoas ORDER BY fore_name DESC
SELECT fore_name, last_name FROM pessoas ORDER BY fore_name DESC, last_name ASC
SELECT fore_name, last_name , qte_pontos FROM pessoas ORDER BY qte_pontos
SELECT fore_name, last_name , qte_pontos FROM pessoas ORDER BY qte_pontos DESC

## TAMANHO (LENGTH)
SELECT fore_name, LENGTH(fore_name) FROM pessoas
SELECT DISTINCT(fore_name) FROM pessoas
SELECT DISTINCT(fore_name) FROM pessoas ORDER BY fore_name
SELECT COUNT(*) FROM pessoas WHERE state = 'SP'

## JUNTAR (JOIN)
SELECT fore_name, pessoas.state FROM pessoas JOIN estados;
SELECT pessoas.fore_name, pessoas.state, estados.nome_capital FROM pessoas JOIN estados ON pessoas.state = estados.state
SELECT * FROM pessoas JOIN estados ON pessoas.state = estados.state;
SELECT * FROM pessoas JOIN estados ON pessoas.state = estados.state WHERE pessoas.fore_name LIKE 'a%' AND estados.state like '%P%'

## ESTATÍSTICA (COUNT, AVG, MIN, MAX, SUM)
SELECT fore_name, COUNT(*) FROM pessoas
SELECT fore_name, COUNT(*) FROM pessoas GROUP BY fore_name
SELECT fore_name, COUNT(*), state FROM pessoas GROUP BY fore_name, state
SELECT fore_name, AVG(qte_pontos) FROM pessoas GROUP BY fore_name, state
SELECT fore_name, AVG(qte_pontos) FROM pessoas GROUP BY fore_name
SELECT fore_name, MIN(qte_pontos) FROM pessoas GROUP BY fore_name
SELECT fore_name, MAX(qte_pontos) FROM pessoas GROUP BY fore_name
SELECT fore_name, SUM(qte_pontos) FROM pessoas GROUP BY fore_name

## OPERADORES MATEMÁTICOS
SELECT 3+2;
SELECT 3/2;
SELECT 3/2.0;
SELECT fore_name, qte_pontos FROM pessoas WHERE qte_pontos > 70;
SELECT qte_pontos + 10 FROM pessoas WHERE qte_pontos < 70;

## (wip)
SELECT fore_name, last_name, qte_pontos FROM pessoas WHERE qte_pontos >= max (qte_pontos)
SELECT fore_name, last_name, qte_pontos FROM pessoas WHERE qte_pontos >= (select MAX(qte_pontos) from Pessoas)

## MANIPULAÇÃO DE STRINGS
SELECT fore_name, last_name FROM pessoas;
SELECT LOWER(fore_name), UPPER(last_name) FROM pessoas;
SELECT LOWER(fore_name), SUBSTR(last_name, 1, 5) FROM pessoas;
SELECT LOWER(fore_name), SUBSTR(last_name, 2) FROM pessoas;
SELECT LOWER(fore_name), SUBSTR(last_name, -2) FROM pessoas;
SELECT LOWER(fore_name), SUBSTR(last_name, -4) FROM pessoas;
SELECT LOWER(fore_name), REPLACE(last_name, 'a', '@@') FROM pessoas;
SELECT LOWER(fore_name), REPLACE(last_name, 'A', '@@') FROM pessoas;
SELECT LOWER(fore_name), REPLACE(last_name, 'e', '') FROM pessoas;

## (wip)
SELECT MAX(qte_pontos) FROM pessoas
SELECT CAST(qte_pontos AS CHAR) FROM pessoas
SELECT MAX(CAST(qte_pontos AS CHAR)) FROM pessoas
SELECT MAX(CAST(qte_pontos AS INT)) FROM pessoas

# (wip)
SELECT fore_name, last_name FROM pessoas;
SELECT fore_name, UPPER(last_name) FROM pessoas;
SELECT fore_name, UPPER(last_name) AS sobrenome FROM pessoas;
SELECT pessoas.fore_name, pessoas.state, estados.nome_capital FROM pessoas JOIN estados ON pessoas.state = estados.state
SELECT P.fore_name, P.state, E.nome_capital FROM pessoas AS P JOIN estados AS E ON P.state = E.state

## INSERIR DADOS
INSERT INTO pessoas (fore_name) VALUES ('Dani')
INSERT INTO pessoas (fore_name, last_name) VALUES ('Dani', 'Monteiro')
SELECT fore_name, last_name FROM pessoas WHERE fore_name = 'Dani'
INSERT INTO pessoas (fore_name, last_name, state, camiseta_ou_chapeu, nome_time) VALUES
('Danielle', 'Monteiro', 'SP', 'chapéu', 'lilás')
SELECT * FROM pessoas
INSERT INTO pessoas (fore_name, last_name, state, camiseta_ou_chapeu, nome_time) VALUES
('DaniMonteiroDBA', 'Apelido', 'SP', 'camiseta', 'vermelho'),
('Teresa', 'Costa', 'MG', 'chapéu', 'azul')
SELECT * FROM pessoas

## SET
UPDATE pessoas SET fore_name = 'Pedro' WHERE fore_name = 'DaniMonteiroDBA'

## DELETAR LINHA (DELETE)
DELETE FROM pessoas WHERE fore_name = 'Pedro'
