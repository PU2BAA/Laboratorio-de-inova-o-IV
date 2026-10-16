# FASE 2: COMPREENSÃO DOS DADOS

Laboratório de Inovação IV — Prof. Edilberto Silva — 2026
---------------------------------------------------------

**Projeto:** Gestão de educação corporativa

**Data:** 13/08/2026 

**Última Atualização:** 12/10/2026

**Status:** EM DESENVOLVIMENTO

**Localização dos Arquivos:** Moodle

**Link PÚBLICO do GitHub** (obrigatório)

* `GitHub - PU2BAA/Laboratorio-de-inova-o-IV: trabalho final · GitHub](https://github.com/PU2BAA/Laboratorio-de-inova-o-IV)

----------------------------------

| ID    | Fonte             | Tipo | Volume          | Frequência | Status     |
| ----- | ----------------- | ---- | --------------- | ---------- | ---------- |
| DS-01 | Curso             | CSV  | 50 registros    | Mensal     | Disponível |
| DS-02 | Funcionario       | CSV  | 140 registros   | Mensal     | Disponível |
| DS-03 | ParticipacaoCurso | CSV  | 2.500 registros | Mensal     | Disponível |

----------------------

### Tabela: CURSO

| Campo                     | Tipo    | Tamanho | Chave | Nulo? | Descrição                                      |
| ------------------------- | ------- | ------- | ----- | ----- | ---------------------------------------------- |
| curso                     | VARCHAR | -       | PK    | Não   | Identificador do curso (ex: "10001/2024")      |
| EVENTO                    | VARCHAR | -       | -     | Não   | Nome do curso/treinamento                      |
| PROGRAMA                  | VARCHAR | -       | -     | Sim   | Programa (PDS ou PDL)                          |
| CATEGORIA                 | VARCHAR | -       | -     | Não   | Categoria do curso (ex: Técnica)               |
| FORMATO                   | VARCHAR | -       | -     | Não   | Formato (INTERNO ou EXTERNO)                   |
| Data de Inclusão do Curso | DATE    | -       | -     | Não   | Data de inclusão (DD/MM/AAAA)                  |
| CARGA-HORÁRIA             | INT     | -       | -     | Não   | Carga horária do curso em horas                |
| MODALIDADE                | VARCHAR | -       | -     | Sim   | Modalidade (EAD ou PRESENCIAL)                 |
| SITUAÇÃO                  | VARCHAR | -       | -     | Sim   | Situação (Realizado ou Não-Executado)          |
| VALOR CONTRATADO          | VARCHAR | -       | -     | Não   | Valor do contrato (formato BR, ex: "2.150,75") |

### Tabela: FUNCIONARIO

| Campo           | Tipo    | Tamanho | Chave | Nulo? | Descrição                                        |
| --------------- | ------- | ------- | ----- | ----- | ------------------------------------------------ |
| Matricula       | INT     | -       | PK    | Não   | Identificador único do servidor                  |
| Nome            | VARCHAR | 100     | -     | Sim   | Nome do servidor                                 |
| Situacao        | VARCHAR | -       | -     | Não   | Situação funcional (Ativa/Inativa/Ativo/Inativo) |
| Cargo           | VARCHAR | -       | -     | Sim   | Cargo ocupado                                    |
| Area            | VARCHAR | -       | -     | Não   | Área de lotação (ex: Acadêmica)                  |
| Chefe           | VARCHAR | -       | -     | Não   | Indica se é chefia (Sim/Não)                     |
| Lotacao         | VARCHAR | -       | -     | Não   | Setor/coordenação de lotação                     |
| Sexo            | VARCHAR | 1       | -     | Não   | Sexo (F/M)                                       |
| Grau_Instrucao  | VARCHAR | -       | -     | Não   | Grau de instrução                                |
| Data_Nascimento | DATE    | -       | -     | Sim   | Data de nascimento (DD/MM/AAAA)                  |

### Tabela: PARTICIPACAOCURSO

| Campo                      | Tipo    | Tamanho | Chave            | Nulo? | Descrição                                   |
| -------------------------- | ------- | ------- | ---------------- | ----- | ------------------------------------------- |
| PROCESSO                   | VARCHAR | -       | FK (Curso)       | Não   | Identificador do processo/curso vinculado   |
| MATRÍCULA                  | INT     | -       | FK (Funcionario) | Não   | Matrícula do servidor participante          |
| SERVIDOR                   | VARCHAR | -       | -                | Sim   | Nome do servidor participante               |
| É GESTOR?                  | VARCHAR | -       | -                | Sim   | Indica se o participante é gestor (Sim/Não) |
| LOTAÇÃO                    | VARCHAR | -       | -                | Sim   | Setor de lotação do participante            |
| UNIDADE                    | VARCHAR | -       | -                | Não   | Unidade organizacional                      |
| EVENTO                     | VARCHAR | -       | FK (Curso)       | Sim   | Nome do curso cursado                       |
| PROGRAMA                   | VARCHAR | -       | -                | Não   | Programa (PDS ou PDL)                       |
| FORMATO                    | VARCHAR | -       | -                | Não   | Formato (INTERNO ou EXTERNO)                |
| MODALIDADE                 | VARCHAR | -       | -                | Sim   | Modalidade (EAD ou PRESENCIAL)              |
| DATA DE INÍCIO DO CURSO    | DATE    | -       | -                | Não   | Data de início (DD/MM/AAAA)                 |
| DATA DE CONCLUSÃO DO CURSO | DATE    | -       | -                | Sim   | Data de conclusão (DD/MM/AAAA)              |

---------------------------------------

### Estatísticas Básicas

**Tabela CURSO:**

* Total de registros: 50
* Período coberto: 04/01/2024 a 04/02/2026
* Registros duplicados: 0
* Valores NULL: PROGRAMA (1), MODALIDADE (1), SITUAÇÃO (2)

**Tabela FUNCIONARIO:**

* Total de registros: 140
* Período coberto (nascimento): datas de 1452 a 2008 (parte inválida — ver seção 4)
* Registros duplicados: 0
* Valores NULL: Nome (2), Cargo (1), Data_Nascimento (1)

**Tabela PARTICIPACAOCURSO:**

* Total de registros: 2.500
* Período coberto: início 03/01/2024 a 23/12/2026; conclusão 07/01/2024 a 28/12/2026
* Registros duplicados: 0
* Valores NULL: SERVIDOR (2), É GESTOR? (1), LOTAÇÃO (2), EVENTO (1), MODALIDADE (1), DATA DE CONCLUSÃO DO CURSO (1)

* * *

4. PROBLEMAS DE QUALIDADE IDENTIFICADOS

---------------------------------------

| ID    | Campo/Tabela                                          | Problema                                                                                  | Severidade | Exemplo                                             |
| ----- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------- | ---------- | --------------------------------------------------- |
| PQ-01 | FORMATO / Curso                                       | Valor fora do domínio esperado (INTERNO/EXTERNO)                                          | BAIXA      | Valor "y"                                           |
| PQ-02 | Data de Inclusão do Curso / Curso                     | Valor não corresponde a uma data válida                                                   | BAIXA      | Valor "67"                                          |
| PQ-03 | Situacao / Funcionario                                | Valor fora do domínio esperado (Ativa/Inativa)                                            | BAIXA      | Valor "0"                                           |
| PQ-04 | Data_Nascimento / Funcionario                         | Datas implausíveis geram idade acima de 100 anos ou valores não numéricos                 | MÉDIA      | Datas "15/04/1452", "06/03/1475", valores "x" e "8" |
| PQ-05 | É GESTOR? / ParticipacaoCurso                         | Valor fora do domínio esperado (Sim/Não)                                                  | BAIXA      | Valor "v"                                           |
| PQ-06 | DATA DE CONCLUSÃO DO CURSO / ParticipacaoCurso        | Valor não corresponde a uma data válida                                                   | BAIXA      | Valores "56" e "34"                                 |
| PQ-07 | VALOR CONTRATADO / Curso                              | Formato numérico brasileiro armazenado como texto, exige conversão antes de uso analítico | BAIXA      | "2.150,75" em vez de 2150.75                        |
| PQ-08 | Vários campos / Curso, Funcionario, ParticipacaoCurso | Valores NULL em múltiplas colunas                                                         | BAIXA      | Ver seção 3 (EDA) para contagem por campo           |

----------------------

| Problema                                                       | Ação                                                                                                                                   | Responsável | Prazo  |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------ |
| PQ-01 (FORMATO / Curso)                                        | Remover (linha excluída se valor inválido)                                                                                             | [Pessoa]    | [Data] |
| PQ-02 (Data de Inclusão / Curso)                               | Remover (linha excluída se data inválida)                                                                                              | [Pessoa]    | [Data] |
| PQ-03 (Situacao / Funcionario)                                 | Remover (linha excluída se valor fora de Ativa/Inativa)                                                                                | [Pessoa]    | [Data] |
| PQ-04 (Data_Nascimento / Funcionario)                          | Substituir por "Não informado" (linha mantida)                                                                                         | [Pessoa]    | [Data] |
| PQ-05 (É GESTOR? / ParticipacaoCurso)                          | Remover (linha excluída se valor inválido)                                                                                             | [Pessoa]    | [Data] |
| PQ-06 (Data de Conclusão / ParticipacaoCurso)                  | Remover (linha excluída se data inválida)                                                                                              | [Pessoa]    | [Data] |
| PQ-07 (VALOR CONTRATADO / Curso)                               | Substituir — conversão de texto BR para número (float)                                                                                 | [Pessoa]    | [Data] |
| PQ-08 (Nulos diversos / Curso, Funcionario, ParticipacaoCurso) | Substituir por "Não informado" (PROGRAMA, MODALIDADE, SITUAÇÃO em Curso) ou Remover (demais campos em Funcionario e ParticipacaoCurso) | [Pessoa]    | [Data] |

---------------------------

**Diagrama de Relacionamento:**
    [FUNCIONARIO] ──Matricula──> [PARTICIPACAOCURSO]
                                        ↓
                                       n:1
                                        ↓
                                  [CURSO] (via EVENTO/PROCESSO)

**Integridade Referencial:**

* [ ] Todas as chaves estrangeiras apontam para registros válidos
* [ ] Não há órfãos (registros sem pai)
* [ ] Cardinalidades confirmadas

-----------------------

**Crescimento de Dados (últimos 12 meses):**

| Mês    | Registros | Taxa Crescimento |
| ------ | --------- | ---------------- |
| Mês 1  | [X.XXX]   | -                |
| Mês 6  | [X.XXX]   | [+Y%]            |
| Mês 12 | [X.XXX]   | [+Z%]            |

**Tempo de Acesso:**

* Consulta simples (1M registros): [X ms]
* Consulta com JOIN: [X ms]
* Agregações: [X ms]

Como o volume atual (50, 140 e 2.500 registros) é pequeno, não há necessidade prática de medir performance de consulta neste momento.

* * *

**Revisado por:** [Nome] **Data de Revisão:** [DD/MM/AAAA]
