# Casos de Teste de Integração — Funcionais

## 1. Objetivo

Validar o comportamento funcional do endpoint `POST /solicitacoes`, responsável por cadastrar solicitações de automação. Os testes verificam a validação dos dados recebidos pela API e a persistência das informações.

## 2. Premissas

- A API disponibiliza o endpoint `POST /solicitacoes`.
- O cadastro exige campos obrigatórios, ainda não especificados.
- Os códigos HTTP esperados abaixo são hipóteses e precisam ser confirmados com o contrato da API.
- A persistência dos dados pode ser verificada no componente de armazenamento.

## 3. Casos de teste

### CT-01 — Cadastro com dados válidos

**Objetivo:** verificar se uma solicitação válida é cadastrada corretamente.

- **Pré-condições:** API disponível e ambiente de teste preparado.
- **Requisição:** enviar uma solicitação com todos os campos obrigatórios preenchidos corretamente.
- **Resultado HTTP esperado:** `201 Created` (a confirmar).
- **Resultado esperado no sistema:** solicitação persistida com os dados enviados e identificador gerado, caso previsto pelo contrato.

### CT-02 — Cadastro sem campo obrigatório

**Objetivo:** verificar se a API rejeita solicitações incompletas.

- **Pré-condições:** API disponível.
- **Requisição:** enviar uma solicitação sem um dos campos obrigatórios.
- **Resultado HTTP esperado:** `400 Bad Request` (a confirmar).
- **Resultado esperado no sistema:** mensagem de validação adequada e ausência de novo registro persistido.

### CT-03 — Cadastro com formato inválido

**Objetivo:** verificar a validação dos tipos e formatos dos dados recebidos.

- **Pré-condições:** API disponível.
- **Requisição:** enviar um campo com formato incompatível com o contrato, como um valor textual em um campo que exige número.
- **Resultado HTTP esperado:** `400 Bad Request` ou `422 Unprocessable Content`, conforme o contrato.
- **Resultado esperado no sistema:** requisição rejeitada e nenhum registro inválido persistido.

### CT-04 — Verificação da persistência após cadastro

**Objetivo:** confirmar que os dados enviados pela API foram armazenados corretamente.

- **Pré-condições:** acesso ao mecanismo de consulta do armazenamento de teste.
- **Requisição:** enviar uma solicitação válida ao endpoint `POST /solicitacoes`.
- **Resultado HTTP esperado:** `201 Created` (a confirmar).
- **Resultado esperado no sistema:** registro localizado no armazenamento, com os valores correspondentes aos dados enviados e ao identificador retornado, se aplic