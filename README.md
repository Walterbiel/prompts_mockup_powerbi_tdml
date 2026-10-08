# Prompts para Claude: Dashboard COVID-19 no Brasil

Projeto de referência: base histórica de COVID-19 do Brasil.IO, com dados provenientes das Secretarias Estaduais de Saúde.

Fonte: https://brasil.io/dataset/covid19/caso/
Arquivos: https://brasil.io/dataset/covid19/files/

> Envie ao Claude o CSV efetivamente baixado. A base é histórica, com cobertura até março de 2022. Não interpretar o resultado como monitoramento atual. A estrutura e os campos devem ser confirmados no arquivo, sem pressupor que todas as colunas existam.

---

## PROMPT 1: Análise da base e planejamento do dashboard

```text
Você é um especialista sênior em Engenharia de Dados, Análise de Dados, Epidemiologia Descritiva, Business Intelligence e Power BI.

PROJETO
Nome: Panorama Histórico da COVID-19 no Brasil
Fonte: Brasil.IO, dataset covid19/caso, compilado a partir de Secretarias Estaduais de Saúde.
Contexto: dashboard histórico para estudo e portfólio, não um painel de situação epidemiológica atual.
Público-alvo: gestores, analistas de dados, estudantes e público geral.
Ferramenta de implementação final: Power BI Desktop.
Objetivo: apresentar a evolução histórica dos casos e óbitos registrados, a distribuição por estado e município e comparações geográficas, respeitando a granularidade e a qualidade da base.
Arquivo: CSV da base covid19/caso que anexei nesta conversa.

REGRAS INEGOCIÁVEIS
1. Examine o arquivo real antes de recomendar qualquer indicador. Não assuma que as colunas de exemplo existem.
2. Não construa o mockup nesta etapa.
3. Não invente valores, resultados, campos, taxas ou relacionamentos.
4. Diferencie fatos observados, hipóteses e problemas de qualidade.
5. Identifique se cada registro é um retrato acumulado por data/localidade, uma observação diária ou outra granularidade.
6. Nunca some valores acumulados de datas diferentes para obter totais. Para cartões de total, defina a regra de última observação válida por localidade, respeitando filtros de período e cobertura.
7. Verifique duplicidade ou sobreposição de registros estaduais e municipais antes de qualquer agregação; não some os dois níveis indiscriminadamente.
8. Para calcular variações, incidência ou mortalidade por população, confirme se os campos e denominadores estão disponíveis e comparáveis. Diferencie letalidade aparente (óbitos/casos notificados) de taxa de mortalidade populacional.
9. Identifique datas sem registros, mudanças de cobertura e eventuais revisões de acumulados.

ETAPA A: PERFIL DOS DADOS
- Quantidade de linhas e colunas, tamanho e intervalo temporal.
- Dicionário completo: coluna, tipo inferido, significado, exemplos e uso analítico.
- Valores ausentes, duplicados, chaves candidatas e inconsistências.
- Granularidade e nível geográfico de cada registro.
- Disponibilidade de data, UF, município, casos, óbitos, população e indicadores diários ou acumulados.
- Cobertura e limitações da fonte.

ETAPA B: PERGUNTAS DE NEGÓCIO
Avalie quais destas perguntas podem ser respondidas com segurança:
- Como evoluíram os casos e os óbitos ao longo do período disponível?
- Quais estados tiveram mais casos e óbitos registrados?
- Quais localidades apresentaram maior volume ou taxa, se houver denominador válido?
- Em quais períodos ocorreram maiores aumentos?
- Como os padrões mudam conforme a região e o período?

ETAPA C: INDICADORES E VISUAIS
Proponha, apenas se suportados pelos dados:
- Total de casos acumulados na data de referência.
- Total de óbitos acumulados na data de referência.
- Letalidade aparente (%), claramente rotulada.
- Novos casos e novos óbitos por dia ou semana, quando calculáveis com segurança.
- Evolução temporal, ranking por UF, comparação geográfica e tabela detalhada.
- Filtros por data, estado e município, se disponíveis.

Para cada medida, entregue: nome, pergunta respondida, tabela/colunas necessárias, definição matemática, regra de agregação, comportamento com filtros, restrições e visual recomendado.

ETAPA D: MODELAGEM POWER BI
- Proponha o modelo mais simples e confiável para a base.
- Indique tabela fato, dimensões e calendário apenas quando fizer sentido.
- Defina chaves, relacionamentos e direção dos filtros.
- Diferencie medidas de colunas calculadas.
- Explique como evitar dupla contagem de snapshots e níveis geográficos.

ENTREGA
1. Resumo executivo do dataset.
2. Dicionário de dados.
3. Diagnóstico de qualidade.
4. Granularidade e regras de agregação.
5. Perguntas analíticas respondíveis.
6. Catálogo de KPIs com fórmulas conceituais.
7. Gráficos e filtros recomendados.
8. Modelo semântico sugerido.
9. Wireframe textual do dashboard.
10. Limitações, decisões pendentes e pontos de validação.

Ao final, apresente uma proposta enxuta de uma página de dashboard e pergunte se está aprovada. Não inicie a etapa 2 antes da minha aprovação.
```

---

## PROMPT 2: Mockup interativo e medidas em massa no Power BI

```text
Você é um especialista sênior em UX/UI para dashboards, Power BI, DAX, TMDL (Tabular Model Definition Language), React e visualização de dados.

PROJETO
Nome: Panorama Histórico da COVID-19 no Brasil.
Público-alvo: gestores, analistas, estudantes e público geral.
Fonte: CSV histórico do Brasil.IO covid19/caso, analisado na etapa 1.
Ferramenta final: Power BI Desktop.
Mockup: protótipo web interativo em React, Tailwind CSS e Recharts, se o ambiente permitir.
Formato prioritário: desktop 1920x1080, com adaptação responsiva.
Identidade visual: tema claro, fundo cinza muito suave, cards brancos, azul como cor principal e verde como cor secundária; visual moderno, limpo e profissional.

PRÉ-REQUISITO
Use a análise e o catálogo de medidas APROVADOS na etapa 1. Se eles não estiverem no contexto, solicite-os. Confirme os nomes reais das tabelas e colunas antes de gerar DAX ou TMDL. Não invente dados ou medidas.

PARTE A: CONSTRUIR O MOCKUP
Crie um dashboard de uma página, com:
- Cabeçalho: título, subtítulo, fonte, cobertura temporal e aviso de que são dados históricos.
- Linha superior de KPIs aprovados: casos, óbitos, letalidade aparente e um quarto indicador somente se suportado.
- Filtros de período e geografia realmente disponíveis na base, com opção de limpar.
- Evolução temporal em linha ou área, quando válida.
- Ranking de estados em barras horizontais.
- Comparação entre casos e óbitos com escalas e rótulos adequados.
- Tabela de localidades, se fizer sentido.
- Legendas, tooltips, estados sem dados e informações de cobertura.

Use dados reais do arquivo. Se o protótipo precisar de amostras para funcionar, identifique-as visivelmente como SIMULADAS e mantenha-as isoladas do dataset real.

Os filtros devem atualizar todos os componentes compatíveis. Respeite as regras de agregação aprovadas: snapshots acumulados não podem ser somados entre datas, e registros estaduais e municipais não devem ser somados juntos se houver sobreposição.

Organize o código em componentes reutilizáveis e separe ingestão, cálculos, filtros, visualizações e tema. Entregue o protótipo executável e instruções curtas para rodar.

PARTE B: MAPEAR O MOCKUP PARA POWER BI
Para cada cartão, gráfico, tabela e tooltip, informe:
- Qual medida DAX será utilizada.
- Quais colunas são dimensões ou eixos.
- Qual filtro afeta o componente.
- Qual regra de agregação evita resultados incorretos.

PARTE C: GERAR TODAS AS MEDIDAS DAX EM TMDL
Produza um script TMDL consolidado para criar EM MASSA todas as medidas aprovadas no Power BI Desktop.

Requisitos:
1. Use TMDL, não 'TDML'.
2. Use nomes REAIS de tabelas e colunas conforme a etapa 1 e o modelo semântico definido.
3. Gere medidas DAX corretas, com dependências explícitas e nomes consistentes.
4. Use DIVIDE em divisões e VAR/RETURN quando ajudarem.
5. Defina displayFolder, formatString e description quando suportados pela sintaxe aplicável.
6. Diferencie valores acumulados, diários e agregações por localidade. Nunca use SUM indiscriminado sobre snapshots acumulados.
7. Não crie métricas dependentes de população, calendário ou relacionamentos que não estejam disponíveis; liste os pré-requisitos separadamente.
8. Agrupe medidas em pastas: Visão Geral, Evolução Temporal, Geografia e Qualidade/Cobertura, quando aplicável.
9. Não recrie, renomeie nem substitua tabelas e colunas existentes sem necessidade.
10. Valide a sintaxe TMDL e a semântica DAX tanto quanto o ambiente permitir; se não puder executar a validação, informe isso claramente.

PARTE D: COMPATIBILIDADE COM MEDIDAS JÁ EXISTENTES (OBRIGATÓRIA)
O modelo Power BI de destino pode conter dezenas ou centenas de medidas e outros objetos. O script NÃO pode apagar, renomear ou sobrescrever medidas preexistentes.

Antes de declarar o script pronto:
1. Solicite o TMDL atual da tabela de destino ou um inventário do modelo (nomes de tabelas, medidas, colunas e relacionamentos). Se não houver acesso a essas informações, NÃO garanta execução sem conflitos.
2. Compare os nomes propostos com TODAS as medidas existentes, inclusive as armazenadas em outras tabelas. Nomes de medidas precisam ser únicos no modelo.
3. Em caso de conflito, proponha um nome novo e consistente, por exemplo com prefixo COVID_, e atualize todas as referências entre medidas. Não substitua medidas antigas automaticamente.
4. Gere um script incremental para a TMDL View, usando a sintaxe e o modo de aplicação suportados pela versão do Power BI Desktop. Prefira `createOrAlter` somente quando adequado; esse comando NÃO é uma garantia contra sobrescrita de objetos homônimos.
5. Inclua apenas as novas medidas e os comandos mínimos necessários. Não entregue a definição integral de uma tabela existente para substituição; não use `createOrReplace` nem operações destrutivas.
6. Respeite os nomes e os tipos reais de tabelas, colunas e relacionamentos. Se for necessária uma tabela de medidas, confirme primeiro se já existe uma adequada; explique separadamente qualquer criação nova.
7. Verifique sintaxe, dependências, ordem de referências, nomes de medidas, expressões DAX, pastas e formatos. Não afirme que houve execução ou testes reais sem acesso ao modelo e ao Power BI.
8. Forneça um procedimento de segurança: salvar cópia PBIX/PBIP, abrir a TMDL View, revisar a prévia/diff das alterações, aplicar em cópia de teste e validar as medidas antes de publicar.
9. Entregue um relatório de impacto contendo: medidas novas, nomes alterados para evitar conflito, dependências, objetos existentes que serão preservados e pendências que impedem aplicação segura.
10. Se faltar inventário do modelo, entregue o script como PROVISÓRIO, explique as validações pendentes e solicite os metadados necessários. Nunca prometa compatibilidade universal.

CRITÉRIO DE ACEITE: adicionar todas as novas medidas do dashboard sem alterar ou remover qualquer medida já existente. A garantia só pode ser dada após inspeção do modelo e teste da aplicação no ambiente real.

ENTREGA TMDL
- Uma tabela de mapeamento: elemento do mockup -> medida -> dependências -> formato.
- Um ÚNICO bloco consolidado de TMDL para copiar e aplicar na TMDL View do Power BI Desktop.
- Se for útil, forneça também o conteúdo de um arquivo .tmdl separado.
- Explique onde abrir a TMDL View, como aplicar o script ao modelo, salvar e verificar as medidas.
- Alerte sobre pré-requisitos de versão/recurso, permissões e possíveis conflitos com medidas já existentes.
- Se a estrutura do modelo ainda não estiver confirmada, não finja que o script é pronto para aplicação: apresente primeiro as dependências e solicite confirmação.

ENTREGÁVEIS FINAIS
1. Mockup interativo e responsivo.
2. Componentes e filtros funcionais.
3. Correspondência entre mockup e visuais do Power BI.
4. Catálogo completo de medidas DAX.
5. Script TMDL único para criação em massa.
6. Instruções de aplicação e checklist de validação no Power BI.
7. Instruções simples para substituir dataset, métricas e paleta em um projeto futuro.

Priorize precisão dos números, legibilidade e reutilização. Não entregue apenas uma imagem estática ou uma descrição do que faria: construa o protótipo no ambiente disponível.
```

---

## Partes a trocar para reutilizar em outro projeto

| Elemento | Neste projeto | O que substituir |
|---|---|---|
| Nome do projeto | Panorama Histórico da COVID-19 no Brasil | Nome do novo dashboard |
| Fonte | Brasil.IO `covid19/caso` | Link e origem do novo dataset |
| Arquivo | CSV histórico de COVID-19 | Arquivo CSV, Excel ou outra fonte anexada |
| Contexto | Epidemiologia descritiva histórica | Problema de negócio ou domínio |
| Público-alvo | Gestores, analistas, estudantes e público geral | Usuários do novo dashboard |
| Perguntas | Evolução, óbitos, casos e geografia | Perguntas que o dashboard deve responder |
| KPIs | Casos, óbitos e letalidade aparente | Medidas próprias do novo domínio |
| Regras especiais | Snapshots acumulados, cobertura e sobreposição geográfica | Regras de negócio e granularidade da nova base |
| Filtros | Período, estado e município | Dimensões realmente presentes |
| Visuais | Série temporal, ranking e tabela | Visuais mais adequados às novas perguntas |
| Ferramenta final | Power BI Desktop | Outra ferramenta, se necessário |
| Mockup | React + Tailwind CSS + Recharts | Stack desejada |
| Paleta | Tema claro, azul e verde | Identidade visual do projeto |
| Formato | Desktop 1920x1080 | Resolução e dispositivos-alvo |
| Medidas em massa | DAX em TMDL | Manter se o destino for Power BI; adaptar se for outra plataforma |
| Modelo existente | Inventário de medidas e objetos do Power BI | Substituir pelo inventário do novo modelo antes de executar o TMDL |
| Conflitos | Prefixo `COVID_` quando necessário | Adaptar o prefixo e conferir nomes duplicados |

### Como usar

1. Anexe a base real e envie o **Prompt 1** ao Claude.
2. Revise e aprove a análise, especialmente a granularidade e os cálculos.
3. Na mesma conversa, envie o **Prompt 2**.
4. Forneça ao Claude o inventário das medidas e tabelas já existentes no Power BI.
5. Revise o script incremental, o relatório de impacto e o diff na TMDL View antes de aplicar em uma cópia do modelo.
