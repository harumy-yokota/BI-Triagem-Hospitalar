/*
13/09 -> Ajustes do nome das colunas para deixar mais didático o entendimento
17/09 -> Substituição de valores: 1 = Feminino, 2 = Masculino
      -> Substituição de valores: 1 = Não, 2 = Sim


Próximas etapas:
- Criar hierarquias das idades
- Tratar valores "??" na coluna Pressão arterial sistólica

*/

-- Banco de dados: `projeto_aplicado`

CREATE DATABASE IF NOT EXISTS `projeto_aplicado` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE `projeto_aplicado`;



-- Estrutura do dataset original Emergency_Service_Triage.csv `triage`

CREATE TABLE projeto_aplicado.`triage` (
      `id_paciente` int auto_increment PRIMARY KEY,
      `grupo` int, -- 1: Pronto-socorro Local / 2: Pronto-socorro Regional
      `genero` int, -- 1: Feminino / 2: Masculino
      `idade` int, -- Idade (anos)
      `numero_pacientes_hora` int,
      `id_transporte` int, -- 1: A pé/ 2: Ambulância pública/ 3: Veículo próprio/ 4: Ambulância privada/ 5: Veículo público/ 6: Cadeira de rodas/ 7: Outro
      `ferimento` int, -- 1: Sem ferimento / 2: Com ferimento
      `queixa_paciente` varchar(45),
      `id_estado_mental` int, -- 1: Consciente / 2: Resposta verbal / 3: Resposta a dor / 4: Incosciente
      `dor` int, -- 1: Com dor / 2: Sem dor
      `escala_dor` varchar(45), -- Escala de dor 0 a 10
      `pressao_sistolica` varchar(45),
      `pressao_diastolica` varchar(45),
      `batimentos_cardiacos` decimal,
      `frequencia_respiratoria` varchar(45),
      `temperatura` varchar(45),
      `saturacao_oximetro` int,
      `KTAS_enfermeiro` int, -- Classificação de risco pelo enfermeiro
      `diagnostico` varchar(100),
      `id_atendimento` int, -- 1: Liberado / 2: Admissão enfermaria / 3: Admissão UTI / 4: Autoliberação / 5: Transferência / 6: Morte / 7: Cirurgia
      `KTAS_expert`int, -- Classificação de risco pelo enfermeiro experiente
      `erro` int, -- Motivo do erro entre a triagem da enfermagem e do expert
      `tempo_PS_min` decimal,
      `duracao_triagem_min` varchar(45),
      `erro_triagem` int -- 0: Correto / 1: Erro de risco maior / 2: Erro de risco menor
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;



-- Data import wizard
-- Importar dados para tabela 'triage'



-- Estrutura do dataset `risco`

CREATE TABLE projeto_aplicado.`risco` (
      `id_risco` int PRIMARY KEY,
      `risco` varchar(20)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO projeto_aplicado.`risco` (`id_risco`, `risco`) VALUES
(1, 'Ressuscitação'),
(2, 'Emergencial'),
(3, 'Urgente'),
(4, 'Menos urgente'),
(5, 'Não urgente');



-- Estrutura do dataset `transporte`

CREATE TABLE projeto_aplicado.`transporte` (
      `id_transporte` int PRIMARY KEY,
      `transporte` varchar(30)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO projeto_aplicado.`transporte` (`id_transporte`, `transporte`) VALUES
(1, 'A pé'),
(2, 'Ambulância pública'),
(3, 'Veículo próprio'),
(4, 'Ambulância privada'),
(5, 'Veículo público'),
(6, 'Cadeira de rodas'),
(7, 'Outro');



-- Estrutura do dataset `estado_mental`

CREATE TABLE projeto_aplicado.`estado_mental` (
      `id_estado_mental` int PRIMARY KEY,
      `estado_mental` varchar(20)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO projeto_aplicado.`estado_mental` (`id_estado_mental`, `estado_mental`) VALUES
(1, 'Consciente'),
(2, 'Resposta verbal'),
(3, 'Resposta a dor'),
(4, 'Incosciente');



-- Estrutura do dataset `atendimento`

CREATE TABLE projeto_aplicado.`atendimento` (
      `id_atendimento` int PRIMARY KEY,
      `atendimento` varchar(30)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO projeto_aplicado.`atendimento` (`id_atendimento`, `atendimento`) VALUES
(1, 'Liberado'),
(2, 'Admissão enfermaria'),
(3, 'Admissão UTI'),
(4, 'Autoliberação'),
(5, 'Transferência'),
(6, 'Morte'),
(7, 'Cirurgia');



-- Deletar colunas da tabela 'triage' que não serão utilizadas no projeto

ALTER TABLE projeto_aplicado.`triage`
      DROP COLUMN `grupo`, 
      DROP COLUMN `numero_pacientes_hora`, 
      DROP COLUMN `erro`, 
      DROP COLUMN `erro_triagem`;



-- Investigação de valores ausentes e outliers em cada coluna

-- Encontrados 556 valores ausentes na coluna 'escala_dor'

SELECT DISTINCT escala_dor, COUNT(escala_dor)
FROM projeto_aplicado.`triage`
GROUP BY escala_dor;

SELECT dor, escala_dor, COUNT(escala_dor)
FROM projeto_aplicado.`triage`
GROUP BY dor, escala_dor;

SET SQL_SAFE_UPDATES = 0;  -- Substituir 553 valores ausentes, atribuindo 'escala_dor' = 0 onde 'dor' = 0, sem alterar na fonte de dados
UPDATE projeto_aplicado.`triage`
SET `escala_dor` = 0
WHERE `dor` = 0;
SET SQL_SAFE_UPDATES = 1;

SELECT * FROM projeto_aplicado.`triage`  -- Verificar as 3 observações restantes, onde 'dor' = 1
WHERE escala_dor = '';

SET SQL_SAFE_UPDATES = 0;  -- Optou-se por deletar as 3 observações
DELETE FROM projeto_aplicado.`triage`
WHERE escala_dor = '';
SET SQL_SAFE_UPDATES = 1;



-- Encontrados 25 valores ausentes na coluna pressao_sistolica 

SELECT DISTINCT pressao_sistolica, COUNT(pressao_sistolica)
FROM projeto_aplicado.`triage`
GROUP BY pressao_sistolica
ORDER BY pressao_sistolica;

SET SQL_SAFE_UPDATES = 0;
UPDATE projeto_aplicado.`triage`
SET `pressao_sistolica` = NULL
WHERE `pressao_sistolica` = 0;
SET SQL_SAFE_UPDATES = 1;



-- Encontrados 29 valores ausentes na coluna pressao_diastolica 

SELECT DISTINCT pressao_diastolica, COUNT(pressao_diastolica)
FROM projeto_aplicado.`triage`
GROUP BY pressao_diastolica
ORDER BY pressao_diastolica;

SET SQL_SAFE_UPDATES = 0;
UPDATE projeto_aplicado.`triage`
SET `pressao_diastolica` = NULL
WHERE `pressao_diastolica` = 0;
SET SQL_SAFE_UPDATES = 1;



-- Encontrados 20 valores ausentes na coluna batimentos_cardiacos 

SELECT DISTINCT batimentos_cardiacos, COUNT(batimentos_cardiacos)
FROM projeto_aplicado.`triage`
GROUP BY batimentos_cardiacos
ORDER BY batimentos_cardiacos;

SET SQL_SAFE_UPDATES = 0;
UPDATE projeto_aplicado.`triage`
SET `batimentos_cardiacos` = NULL
WHERE `batimentos_cardiacos` = 0;
SET SQL_SAFE_UPDATES = 1;



-- Encontrados 22 valores ausentes na coluna frequencia_respiratoria 

SELECT DISTINCT frequencia_respiratoria, COUNT(frequencia_respiratoria)
FROM projeto_aplicado.`triage`
GROUP BY frequencia_respiratoria
ORDER BY frequencia_respiratoria;

SET SQL_SAFE_UPDATES = 0;
UPDATE projeto_aplicado.`triage`
SET `frequencia_respiratoria` = NULL
WHERE `frequencia_respiratoria` = 0;
SET SQL_SAFE_UPDATES = 1;



-- Encontrados 18 valores ausentes na coluna temperatura 

SELECT DISTINCT temperatura, COUNT(temperatura)
FROM projeto_aplicado.`triage`
GROUP BY temperatura
ORDER BY temperatura;

SET SQL_SAFE_UPDATES = 0;
UPDATE projeto_aplicado.`triage`
SET `temperatura` = NULL
WHERE `temperatura` = 0;
SET SQL_SAFE_UPDATES = 1;



-- Encontrados 18 valores = 0 na coluna 'temperatura'

SELECT MIN(temperatura) AS minimo, 
      MAX(temperatura) AS maximo, 
      ROUND(AVG(temperatura)) AS media, 
      COUNT(temperatura) AS contagem_nao_nulo
FROM projeto_aplicado.`triage`
WHERE temperatura > 0;

SELECT COUNT(temperatura) AS contagem_nulo
FROM projeto_aplicado.`triage`
WHERE temperatura <= 0;



-- Encontrados 694 valores = 0 na coluna 'saturacao_oximetro'

SELECT MIN(saturacao_oximetro) AS minimo, 
      MAX(saturacao_oximetro) AS maximo, 
      ROUND(AVG(saturacao_oximetro)) AS media, 
      COUNT(saturacao_oximetro) AS contagem_nao_nulo
FROM projeto_aplicado.`triage`
WHERE saturacao_oximetro > 0;

SELECT COUNT(saturacao_oximetro) AS contagem_nulo
FROM projeto_aplicado.`triage`
WHERE saturacao_oximetro <= 0;

SET SQL_SAFE_UPDATES = 0;  -- Substituir 694 valores = 0, atribuindo 'saturacao_oximetro' = NULL
UPDATE projeto_aplicado.`triage`
SET `saturacao_oximetro` = NULL
WHERE `saturacao_oximetro` = 0;
SET SQL_SAFE_UPDATES = 1;



-- Adicionar coluna 'KTAS_check' para comparar 'KTAS_enfermeiro' e 'KTAS_expert'

ALTER TABLE projeto_aplicado ADD KTAS_check varchar(20);
