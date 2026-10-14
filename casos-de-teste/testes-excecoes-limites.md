# Casos de Teste de Integração — Exceções e Limites

## 1. Objetivo

Avaliar o comportamento da API `POST /solicitacoes` em situações excepcionais, valores-limite e falhas nos componentes integrados, verificando se os erros são tratados adequadamente e se a integridade dos dados é preservada.

## 2. Premissas

- Os códigos HTTP indicados são hipóteses e precisam ser confirmados no contrato da API.
- Os limites dos campos e as regras de duplicidade ainda precisam ser definidos.
- Os cenários de falha dependem de recursos para simular indisponibilidade e erros de persistência no ambiente de teste.

## 3. Casos de teste

### CT-05 — Campo obrigatório enviado vazio

**Objetivo:** verificar o tratamento de campos obrigatórios enviados sem valor.

- **Pré-condições:** API disponível.
- **Requisição:** enviar uma solicitação com um campo obrigatório contendo uma string vazia.
- **Resultado HTTP esperado:** `400 Bad Request` ou outro código definido pelo contrato.
- **Resultado esperado nos componentes envolvidos:** validação rejeita o conteúdo e nenhum registro inválido é persistido.
- **Justificativa:** um campo presente na requisição pode continuar inválido quando seu conteúdo está vazio.

### CT-06 — Valor no limite permitido

**Objetivo:** verificar o comportamento da API diante de um valor situado exatamente no limite definido para um campo.

- **Pré-condições:** conhecer o tamanho máximo ou o intervalo permitido para pelo menos um campo.
- **Requisição:** enviar uma solicitação cujo campo esteja exatamente no limite permitido.
- **Resultado HTTP esperado:** `201 Created`, se os demais dados forem válidos.
- **Resultado esperado nos componentes envolvidos:** o valor é validado e persistido sem truncamento ou alteração indevida.
- **Justificativa:** verificar se a validação e a persistência respeitam os limites definidos.

### CT-07 — Tipo de dado incorreto

**Objetivo:** verificar se a API rejeita dados incompatíveis com o tipo esperado.

- **Pré-condições:** conhecer os tipos definidos no contrato.
- **Requisição:** enviar um valor de tipo incompatível com o esperado por um campo.
- **Resultado HTTP esperado:** `400 Bad Request` ou `422 Unprocessable Content`, conforme o contrato.
- **Resultado esperado nos componentes envolvidos:** a requisição é rejeitada antes da persistência, sem conversões indevidas.
- **Justificativa:** identificar inconsistências entre a validação da API e o modelo de dados.

### CT-08 — Falha no componente de persistência

**Objetivo:** verificar o comportamento da API quando o armazenamento falha durante o cadastro.

- **Pré-condições:** ambiente de teste capaz de simular uma falha de persistência.
- **Requisição:** enviar uma solicitação válida enquanto o componente de armazenamento apresenta uma falha controlada.
- **Resultado HTTP esperado:** erro de servidor, como `500 Internal Server Error` ou `503 Service Unavailable`, conforme o tratamento definido.
- **Resultado esperado nos componentes envolvidos:** a API retorna um erro controlado, sem informar sucesso indevidamente; o estado dos dados permanece consistente.
- **Justificativa:** validar a comunicação entre API e armazenamento em condições de falha.

### CT-09 — Requisição duplicada

**Objetivo:** verificar como a API trata solicitações duplicadas quando existe uma regra de prevenção de duplicidade.

- **Pré-condições:** regra de duplicidade documentada e critérios para identificar solicitações equivalentes definidos.
- **Requisição:** enviar duas vezes a mesma solicitação ou repetir a operação conforme a regra estabelecida.
- **Resultado HTTP esperado:** depende do contrato; pode indicar conflito ou retornar o resultado anterior em uma operação idempotente.
- **Resultado esperado nos componentes envolvidos:** o comportamento observado respeita a regra de duplicidade e evita registros indevidos.
- **Justificativa:** identificar inconsistências entre o tratamento da requisição e a persistência.

### CT-10 — Divergência entre resposta e dados persistidos

**Objetivo:** verificar se os dados armazenados correspondem ao resultado informado pela API.

- **Pré-condições:** possibilidade de consultar o armazenamento no ambiente de teste.
- **Requisição:** enviar uma solicitação válida e comparar a resposta com o registro persistido.
- **Resultado HTTP esperado:** `201 Created`, se o cadastro for concluído.
- **Resultado esperado nos componentes envolvidos:** identificador e campos retornados correspondem ao registro armazenado, conforme as regras de transformação previstas.
- **Justificativa:** identificar divergências entre a resposta da API e o estado efetivo dos dados.

## 4. Premissas e dúvidas para validação

Antes de implementar os testes, é necessário esclarecer:

- Quais campos são obrigatórios e quais aceitam valores vazios?
- Quais são os limites máximos e mínimos dos campos?
- Quais códigos HTTP estão definidos para erros de validação e falhas internas?
- Existe uma regra de idempotência ou prevenção de duplicidade?
- Como simular falhas de persistência no ambiente de teste?
- Quais campos são transformados pela API antes de serem armazenados ou retornados?

## 5. Observações

Os casos foram propostos a partir do segundo prompt, com foco em exceções, limites e integração entre componentes. Os resultados esperados que dependem de regras ainda não documentadas devem ser confirmados antes da execução.

A existência desses casos documentados não significa que tenham sido executados. A validação depende de um ambiente de teste e da confirmação do contrato da API.