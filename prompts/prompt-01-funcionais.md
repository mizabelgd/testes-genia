Atue como uma pessoa engenheira de qualidade de software especializada em testes de integração de APIs REST.

**Contexto:** existe uma API para cadastrar solicitações de automação por meio do endpoint `POST /solicitacoes`.

**Tarefa:** gere casos de teste de integração para validar o comportamento funcional desse endpoint.

Considere:
- Cadastro com dados válidos.
- Campos obrigatórios ausentes.
- Dados em formato inválido.
- Respostas HTTP esperadas.
- Validação da persistência dos dados.

**Regras:**
- Não invente comportamentos que não estejam definidos. Quando faltar informação, sinalize a premissa.
- Priorize testes que validem a interação entre a API e seus componentes dependentes.
- Cada caso deve ter identificador, objetivo, pré-condições, requisição, resultado HTTP esperado e resultado esperado no sistema.
- Evite casos duplicados.

**Formato:** apresente os casos em uma tabela Markdown, com linguagem objetiva e verificável.