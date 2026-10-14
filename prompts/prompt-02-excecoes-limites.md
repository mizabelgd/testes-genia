Atue como especialista em testes de integração de APIs REST.

**Contexto:** a API `POST /solicitacoes` recebe os dados de uma solicitação de automação e interage com componentes de validação e persistência.

Gere testes adicionais, priorizando cenários de exceção, limites e falhas de integração. Não repita os casos funcionais básicos.

Use os exemplos abaixo como referência de formato:

- **Exemplo 1:** campo obrigatório ausente → verificar se a API rejeita a requisição conforme o contrato.
- **Exemplo 2:** serviço dependente indisponível → verificar se a API apresenta um erro controlado e não registra dados indevidamente.

Gere casos para situações como:
- Campos vazios ou valores nos limites permitidos.
- Requisições com tipos de dados incorretos.
- Falha na persistência.
- Requisições duplicadas, caso exista regra de idempotência ou prevenção de duplicidade.
- Inconsistências entre a resposta da API e os dados persistidos.

**Regras:**
- Não assuma códigos HTTP ou regras de negócio não documentados; indique o que precisa ser confirmado.
- Para cada caso, informe identificador, objetivo, pré-condições, dados enviados, resultado HTTP esperado, resultado esperado nos componentes envolvidos e justificativa.
- Priorize cenários diferentes entre si e que revelem falhas de integração.

**Formato:** tabela Markdown. Ao final, liste as premissas e dúvidas que precisam ser esclarecidas antes da implementação dos testes.