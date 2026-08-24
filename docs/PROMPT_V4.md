# Prompt Avançado — Sistema de Conciliação Financeira Omie × Modelagem

Crie um **sistema avançado de conciliação de fluxo de caixa** para comparar o **Omie** com uma **Modelagem financeira interna**, com foco em identificar divergências de caixa de forma rápida, auditável e visual.

O sistema deve trabalhar em **duas camadas**:

1. **Comparação consolidada mensal**
2. **Investigação detalhada da divergência**

A lógica principal é:

> Primeiro identificar **em qual mês existe diferença**.
> Depois descobrir **quais dias e quais lançamentos explicam essa diferença**.

O sistema NÃO deve começar comparando diretamente todos os lançamentos brutos sem antes validar o consolidado mensal.

---

# 1. Objetivo principal

O sistema deve responder automaticamente:

- O saldo inicial do Omie bate com a Modelagem?
- Quanto entrou no Omie em cada mês?
- Quanto entrou na Modelagem em cada mês?
- Quanto saiu no Omie em cada mês?
- Quanto saiu na Modelagem em cada mês?
- Qual foi o saldo final de cada base?
- Qual é a diferença mensal?
- Em quais meses existem divergências?
- Em quais dias essas divergências surgiram?
- Quais lançamentos específicos explicam a diferença?
- Existe lançamento somente no Omie?
- Existe lançamento somente na Modelagem?
- Existe o mesmo lançamento com valor diferente?
- Existe o mesmo lançamento com data diferente?
- Existe lançamento agrupado em uma base e desmembrado na outra?

O sistema deve transformar uma diferença de saldo em uma explicação objetiva.

Exemplo:

> Janeiro/2026 possui R$ 8.403,21 de divergência.
>
> 92% da diferença está concentrada em 4 dias:
>
> 05/01 — R$ 2.500,00
> 18/01 — R$ 1.903,21
> 27/01 — R$ 3.000,00
> 31/01 — R$ 1.000,00

Depois o usuário deve conseguir clicar no dia e visualizar os lançamentos envolvidos.

---

# 2. Conceito central

A análise deve seguir obrigatoriamente esta hierarquia:

## Nível 1 — MÊS

Comparar:

**Omie × Modelagem**

por mês.

## Nível 2 — DIA

Se existir divergência no mês, decompor por dia.

## Nível 3 — LANÇAMENTO

Se existir divergência no dia, procurar os lançamentos responsáveis.

Nunca começar diretamente pelo nível 3.

---

# 3. Saldo inicial

O sistema deve permitir informar manualmente o saldo inicial consolidado.

Saldo inicial atual:

**R$ 3.350.160,91**

O saldo é consolidado.

Não é necessário separar inicialmente por banco.

O usuário deve conseguir alterar o saldo inicial de cada período.

---

# 4. Fórmula principal do caixa

Para Omie:

**Saldo Inicial + Receitas - Despesas + Ajustes = Saldo Final**

Para Modelagem:

**Saldo Inicial + Entradas - Saídas + Ajustes = Saldo Final**

A estrutura deve aceitar que Omie e Modelagem usem nomenclaturas diferentes.

---

# 5. Não confundir caixa com competência

O sistema deve trabalhar prioritariamente com:

- data de pagamento;
- data de recebimento;
- data efetiva da movimentação financeira.

Não usar como regra principal:

- data de emissão;
- competência;
- data de execução;
- data de vencimento.

Esses campos podem ser mostrados como informação adicional.

A pergunta principal é:

> Quando o dinheiro entrou ou saiu?

---

# 6. Importação de dados

Criar uma página chamada:

# Importar Dados

Permitir adicionar arquivos sempre que o usuário quiser.

Aceitar:

- XLSX
- XLS
- CSV

Não substituir automaticamente arquivos anteriormente importados.

Permitir:

- adicionar arquivo;
- remover arquivo individual;
- limpar base;
- visualizar arquivos carregados;
- visualizar número de linhas;
- visualizar período identificado.

---

# 7. Dados do Omie

O sistema deve aceitar inicialmente:

### Pagamentos realizados

### Recebimentos realizados

Opcionalmente:

### Movimentação financeira

Se futuramente for possível importar o próprio relatório consolidado de fluxo de caixa, deixar a arquitetura preparada.

---

# 8. Dados da Modelagem

Permitir importar:

### CP — Contas a Pagar

### CR — Contas a Receber

Também permitir importar futuramente uma base consolidada do Fluxo de Caixa.

Porém o sistema não deve simplesmente somar todas as linhas existentes.

Ele deve identificar somente os campos que representam movimentação efetiva de caixa.

---

# 9. Camada 1 — Comparação consolidada

Criar uma tela principal:

# Conciliação de Caixa

Mostrar uma tabela mensal:

| MêsSaldo Inicial OmieSaldo Inicial ModelagemEntradas OmieEntradas ModelagemSaídas OmieSaídas ModelagemSaldo Final OmieSaldo Final ModelagemDivergência |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ |

Exemplo:

\| Janeiro/2026 | R$ 3.350.160,91 | R$ 3.350.160,91 | R$ 1.704.949,03 | R$ 1.700.149,00 | R$ 3.787.204,15 | R$ 3.765.000,00 | R$ 1.276.905,79 | R$ 1.285.309,00 | -R$ 8.403,21 |

Destacar os meses:

- verde = conciliado;
- vermelho = divergência;
- amarelo = divergência pequena configurável.

---

# 10. Dashboard

Criar cards:

### SALDO INICIAL

### ENTRADAS OMIE

### ENTRADAS MODELAGEM

### DIFERENÇA DE ENTRADAS

### SAÍDAS OMIE

### SAÍDAS MODELAGEM

### DIFERENÇA DE SAÍDAS

### SALDO FINAL OMIE

### SALDO FINAL MODELAGEM

### DIVERGÊNCIA FINAL

Criar também:

**Percentual de conciliação**

Exemplo:

> 99,72% do fluxo conciliado

---

# 11. Ponte da divergência

Criar seção:

# O que explica a diferença?

Exemplo:

Saldo inicial:

**R$ 3.350.160,91**

Diferença de entradas:

**+ R$ 4.800,03**

Diferença de saídas:

**- R$ 22.204,15**

Diferença de ajustes:

**+ R$ 9.000,00**

Diferença final:

**- R$ 8.403,21**

A ponte deve sempre fechar matematicamente.

Nunca mostrar uma diferença final que não possa ser explicada pelos componentes.

---

# 12. Camada 2 — Análise diária

Quando o usuário clicar em um mês com divergência, abrir:

# Divergência por Dia

Mostrar:

| DataEntradas OmieEntradas ModelagemDif. EntradasSaídas OmieSaídas ModelagemDif. SaídasImpacto Líquido |
| ----------------------------------------------------------------------------------------------------- |

Exemplo:

\| 05/01/2026 | 120.000 | 120.000 | 0 | 42.500 | 40.000 | -2.500 | -2.500 |
\| 06/01/2026 | 50.000 | 50.000 | 0 | 18.000 | 18.000 | 0 | 0 |
\| 18/01/2026 | 80.000 | 78.096,79 | 1.903,21 | 30.000 | 30.000 | 0 | 1.903,21 |

Ordenar automaticamente por:

**maior impacto financeiro primeiro.**

---

# 13. Mostrar somente os dias problemáticos

Criar filtro:

### Mostrar:

- Todos os dias
- Somente dias conciliados
- Somente dias com divergência

Padrão:

**Somente dias com divergência**

Mostrar mensagem:

> 31 dias analisados
> 26 dias conciliados
> 5 dias possuem divergência

---

# 14. Camada 3 — Investigação por lançamento

Ao clicar em um dia com divergência, abrir:

# Detalhamento do Dia

Separar em duas colunas.

## OMIE

Mostrar todos os pagamentos e recebimentos daquele dia.

## MODELAGEM

Mostrar todos os pagamentos e recebimentos daquele dia.

Tabela:

| StatusCliente/FornecedorDocumentoValor OmieValor ModelagemDiferença |
| ------------------------------------------------------------------- |

---

# 15. Regra de conciliação dos lançamentos

Utilizar nesta ordem:

### 1. Tipo

Entrada com entrada.

Saída com saída.

Nunca cruzar entrada com saída.

### 2. Data efetiva

Mesma data = maior prioridade.

### 3. Valor

Valor idêntico = forte evidência.

### 4. Documento / NF

Se disponível.

### 5. Cliente ou fornecedor

Usar como apoio.

### 6. Descrição

Usar como apoio complementar.

---

# 16. Normalização de nomes

Antes de comparar nomes:

- remover acentos;
- converter para maiúsculas;
- remover espaços duplicados;
- remover caracteres especiais;
- ignorar LTDA;
- ignorar ME;
- ignorar EIRELI;
- ignorar SA;
- ignorar S/A.

Exemplo:

**ABC EVENTOS LTDA**

e:

**ABC Eventos**

devem ser considerados altamente semelhantes.

---

# 17. Campos que NÃO podem impedir conciliação

Não utilizar como exigência:

- projeto;
- centro de custo;
- categoria;
- classificação gerencial.

Omie e Modelagem possuem nomenclaturas diferentes.

Se:

- data bate;
- valor bate;
- tipo bate;

o lançamento pode ser conciliado mesmo que projeto ou categoria sejam diferentes.

Mostrar apenas:

**Classificação gerencial diferente**

como alerta informativo.

---

# 18. Status dos lançamentos

Criar:

### CONCILIADO

Mesmo tipo + mesma data + mesmo valor.

### SOMENTE OMIE

Existe somente no Omie.

### SOMENTE MODELAGEM

Existe somente na Modelagem.

### DATA DIFERENTE

Mesmo valor e forte semelhança, mas data diferente.

### VALOR DIFERENTE

Mesmo documento/fornecedor/data, mas valor divergente.

### POSSÍVEL CORRESPONDÊNCIA

Sistema encontrou indícios, mas não consegue confirmar.

### CONCILIADO POR COMPOSIÇÃO

Um lançamento de uma base corresponde a vários da outra.

---

# 19. Conciliação por composição

Essa função é essencial.

Exemplo:

Omie:

**10/01 — R$ 15.000**

Modelagem:

**10/01 — R$ 5.000**
**10/01 — R$ 4.000**
**10/01 — R$ 6.000**

Como:

**R$ 5.000 + R$ 4.000 + R$ 6.000 = R$ 15.000**

marcar:

**CONCILIADO POR COMPOSIÇÃO**

Também fazer o inverso.

Limitar inicialmente busca automática para combinações de até 3 ou 4 lançamentos, evitando lentidão excessiva.

---

# 20. Análise inteligente da diferença

O sistema deve gerar explicações automáticas.

Exemplo:

> Divergência em 15/01/2026: R$ 12.500,00.
>
> Identificamos:
>
> - R$ 10.000,00 presente somente no Omie.
> - R$ 2.500,00 com provável diferença de data.
>
> Esses dois itens explicam 100% da divergência do dia.

Outro exemplo:

> Divergência do mês: R$ 8.403,21.
>
> 4 dias explicam 94% da diferença.
>
> Recomenda-se iniciar a análise por 31/01 e 18/01.

---

# 21. Indicador de diferença explicada

Criar KPI:

### DIVERGÊNCIA EXPLICADA

Exemplo:

**R$ 7.982,40 de R$ 8.403,21**

**95% explicado**

Restante:

**R$ 420,81 ainda não explicado**

O objetivo do sistema deve ser chegar a:

**100% da divergência explicada.**

---

# 22. Ranking de divergências

Criar página:

# Maiores Divergências

Mostrar:

1. 31/01 — R$ 4.500
2. 18/01 — R$ 1.903
3. 05/01 — R$ 1.500
4. 27/01 — R$ 500

Mostrar também:

**Impacto acumulado**

Exemplo:

> As 3 maiores divergências representam 93% do problema.

---

# 23. DRE de Caixa comparativa

Criar página:

# DRE de Caixa

Não tratar como DRE contábil tradicional.

Mostrar:

| GrupoOmieModelagemDiferença |
| --------------------------- |

Estrutura inicial:

### SALDO INICIAL

### ENTRADAS

Receitas diretas

Receitas indiretas

Entradas não operacionais

Outras entradas

### TOTAL ENTRADAS

### SAÍDAS

Impostos

Custos / CSP / CMV

Administrativas

Pessoal

Comerciais

Financeiras

Não operacionais

Investimentos

Outras

### TOTAL SAÍDAS

### GERAÇÃO / CONSUMO DE CAIXA

### AJUSTES

### SALDO FINAL

---

# 24. DE-PARA gerencial

Como Omie e Modelagem possuem nomenclaturas diferentes, criar:

# DE-PARA

Exemplo:

| OrigemCategoria originalGrupo padrão |                                     |                 |
| ------------------------------------ | ----------------------------------- | --------------- |
| Omie                                 | Custos de Prestação de Serviços/CMV | CSP             |
| Modelagem                            | CSP                                 | CSP             |
| Omie                                 | Despesas com Pessoal                | Pessoal         |
| Modelagem                            | Pessoal                             | Pessoal         |
| Omie                                 | Despesas Administrativas            | Administrativas |
| Modelagem                            | Administrativas                     | Administrativas |

Esse DE-PARA serve somente para apresentação da DRE de Caixa.

Nunca permitir que o DE-PARA altere a conciliação financeira.

---

# 25. Transferências internas

Esse ponto deve receber tratamento separado.

No Omie aparecem:

- Entrada de Transferência
- Saída de Transferência
- Transferência
- Ajustes de saldo

Como o caixa está sendo analisado de forma consolidada, transferências entre contas próprias não representam geração ou consumo real de caixa.

Criar seção:

# Transferências e Ajustes

Mostrar:

Entradas de transferência:

R$ X

Saídas de transferência:

R$ X

Resultado líquido:

R$ X

Se entrada e saída se anularem:

**Transferências conciliadas**

Se não se anularem:

**Investigar diferença de transferência**

Ajustes de saldo devem aparecer separadamente.

---

# 26. Não esconder ajustes

Se houver um ajuste de saldo de R$ 9.000,00, por exemplo, não simplesmente excluir.

Mostrar claramente:

> Ajuste de saldo identificado: R$ 9.000,00.

E indicar se ele afeta ou não o saldo final.

---

# 27. Períodos

Permitir analisar:

- um mês;
- vários meses;
- ano inteiro.

Criar seletor:

**Janeiro/2026**

ou:

**Janeiro/2026 até Julho/2026**

---

# 28. Continuidade mensal

O saldo final de um mês deve poder ser confrontado com o saldo inicial do mês seguinte.

Criar teste:

### CONTINUIDADE DO CAIXA

Exemplo:

Saldo final Jan:

R$ 1.276.905,79

Saldo inicial Fev:

R$ 1.276.905,79

Resultado:

**OK**

Se não bater:

**Diferença entre fechamento de janeiro e abertura de fevereiro: R$ X**

Isso pode revelar erros de abertura, ajustes ou lançamentos retroativos.

---

# 29. Auditoria

Cada conciliação manual deve guardar:

- data;
- usuário;
- ação;
- lançamento Omie;
- lançamento Modelagem;
- status anterior;
- status novo.

Exemplo:

> 21/08/2026 15:30
>
> Lançamento confirmado manualmente como conciliado.

---

# 30. Confirmação manual

No detalhamento permitir:

### Confirmar conciliação

### Não são o mesmo lançamento

### Ignorar neste fechamento

### Adicionar observação

### Marcar para revisar

---

# 31. Histórico

Criar uma página:

# Fechamentos

Exemplo:

| PeríodoSaldo OmieSaldo ModelagemDivergênciaStatus |   |   |        |            |
| ------------------------------------------------- | - | - | ------ | ---------- |
| Jan/26                                            |   |   | R$ 0   | Conciliado |
| Fev/26                                            |   |   | R$ 420 | Em análise |
| Mar/26                                            |   |   | R$ 0   | Conciliado |

Permitir reabrir períodos anteriores.

---

# 32. Validação final

Criar botão:

# Validar Fechamento

Antes de fechar verificar:

- saldo inicial;
- entradas;
- saídas;
- ajustes;
- saldo final;
- dias divergentes;
- lançamentos sem correspondência;
- divergência não explicada.

Se tudo estiver conciliado:

> **Fluxo de Caixa Conciliado**
>
> Divergência: R$ 0,00
>
> 100% dos valores explicados.

Se ainda houver problema:

> **Fechamento ainda possui R$ 8.403,21 de divergência**
>
> 95% já explicado.
>
> R$ 420,81 ainda precisam ser investigados.

---

# 33. Exportação

Permitir gerar Excel contendo:

### Resumo mensal

### Comparativo Omie × Modelagem

### Divergência por dia

### Divergências por lançamento

### DRE de Caixa

### Itens somente Omie

### Itens somente Modelagem

### Conciliações manuais

### Auditoria

---

# 34. Design

Criar aparência de sistema financeiro profissional.

Referências visuais:

- ERP;
- FP&A;
- BPO financeiro;
- conciliação bancária.

Usar:

- fundo claro;
- menu lateral;
- cards discretos;
- tabelas compactas;
- boa hierarquia visual;
- números destacados;
- poucas cores.

Cores:

**Verde:** conciliado.

**Vermelho:** divergência.

**Amarelo/Laranja:** precisa analisar.

**Azul:** informação ou possível correspondência.

Não exagerar em gradientes.

Não criar aparência genérica de dashboard de IA.

---

# 35. Menu lateral

Criar:

**Dashboard**

**Consolidado Mensal**

**Divergência por Dia**

**Conciliação de Lançamentos**

**DRE de Caixa**

**Transferências e Ajustes**

**Maiores Divergências**

**Importar Dados**

**DE-PARA**

**Fechamentos**

**Auditoria**

**Configurações**

---

# 36. Regra fundamental

A lógica do sistema deve ser:

## PRIMEIRO

> O consolidado do Omie bate com a Modelagem?

Se sim:

**período conciliado.**

Se não:

## SEGUNDO

> Em quais dias surgiu a diferença?

Depois:

## TERCEIRO

> Quais lançamentos daqueles dias explicam a diferença?

Nunca apresentar milhares de lançamentos para o usuário analisar sem antes reduzir o universo da investigação.

---

# 37. Exemplo de experiência ideal

Ao entrar:

> **Janeiro/2026**
>
> Saldo inicial:
> R$ 3.350.160,91
>
> Saldo Final Omie:
> R$ 1.276.905,79
>
> Saldo Final Modelagem:
> R$ 1.285.309,00
>
> **Divergência: R$ 8.403,21**
>
> 🔴 Fluxo ainda não conciliado

Logo abaixo:

> **Encontramos divergência em 5 dos 31 dias.**
>
> 26 dias estão 100% conciliados.

Depois:

> **3 dias explicam 91% da diferença.**

Botão:

### Investigar divergência

Ao clicar:

> 31/01/2026
>
> Omie:
> Saídas R$ 85.500
>
> Modelagem:
> Saídas R$ 81.000
>
> Divergência:
> R$ 4.500

Depois listar:

> Fornecedor ABC — R$ 3.000 — SOMENTE OMIE
>
> Fornecedor XYZ — R$ 1.500 — POSSÍVEL DATA DIFERENTE

Assim o usuário consegue sair de:

> "Meu saldo não bate."

para:

> "Meu saldo não bate R$ 8.403,21 e estes 4 lançamentos são responsáveis pela diferença."

Esse é o resultado principal esperado do sistema.