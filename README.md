# Projeto-SSIS

Aula 1 - Introdução ao Git e Github

Aula 2 - Criando conectores ( CSV e SQL Server )

Aula 3 - Criando Tabelas no SQL Server e Importando dados de arquivos CSV

Aula 4 -Loop de Truncate Table

- USE Curso_SSIS;


-- Criar variável "@Tabelas", Onde traz uma nova tabela com dois campos: IDX (índice) e uma coluna (Tb1Name) com os nomes das tabelas existentes--
DECLARE
	@Tabelas TABLE (IDX INT IDENTITY (1,1), Tb1Name VARCHAR (100))
INSERT INTO 
	@Tabelas (Tb1Name)

-- Pegar Nome de todas as Tabelas --
SELECT
	Table_Name
FROM
	INFORMATION_SCHEMA.TABLES
WHERE
	TABLE_TYPE = 'Base Table'
AND TABLE_NAME <> 'sysssislog'    --Tabelas que não precisam sofrer o TRUNCATE



DECLARE @Start INT
DECLARE @End INT
DECLARE @Command VARCHAR (100)

SELECT 
	@Start = 1, @End = MAX(IDX)
FROM
	@Tabelas

WHILE 
	@Start <= @End
BEGIN
	SELECT 
		@Command = 'TRUNCATE TABLE ' + Tb1Name + ''
	FROM
		@Tabelas
	WHERE
		IDX = @Start

	EXEC (@Command)
	PRINT (@Command)

	SET @Start = @Start + 1

END


Aula 5 -Dividindo Fluxo de ETL

