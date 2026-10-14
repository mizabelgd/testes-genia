# Comparação dos Resultados dos Prompts

## 1. Objetivo

Comparar os resultados da aplicação de dois prompts no LLM para gerar casos de teste de integração de uma API REST fictícia, considerando qualidade, diversidade, duplicidade e ajustes nas instruções.

- **Prompt 1:** geração de testes funcionais, utilizando zero-shot.
- **Prompt 2:** geração de testes de exceção e limites, utilizando exemplos como referência (few-shot).

## 2. Resultados obtidos

A aplicação dos prompts produziu dez casos de teste documentados.

| Prompt | Quantidade | Cenários gerados |
|---|---:|---|
| Prompt 1 — Funcionais | 4 | Cadastro válido, campo obrigatório ausente, formato inválido e verificação da persistência. |
| Prompt 2 — Exceções e limites | 6 | Campo vazio, valor no limite, tipo incorreto, falha de persistência, requisição duplicada e divergência entre resposta e dados persistidos. |

A quantidade de casos não representa, isoladamente, maior qualidade. É necessário considerar a relevância, a clareza e a complementaridade dos cenários.

## 3. Comparação por critério

| Critério | Prompt 1 — Funcionais | Prompt 2 — Exceções e limites |
|---|---|---|
| Qualidade | Os casos possuem objetivo, pré-condições, requisição e resultado esperado, facilitando a revisão. | Os casos incluem justificativas e consideram os efeitos das falhas nos componentes envolvidos. |
| Diversidade | Concentra-se no fluxo básico, na validação e na persistência bem-sucedida. | Amplia a cobertura para condições excepcionais, limites e inconsistências. |
| Duplicidade | Os cenários são distintos, embora a validação de formato e a de campos obrigatórios possam compartilhar regras. | Há possível sobreposição com os testes de campos ausentes e formatos inválidos do primeiro prompt. |
| Dependência de contexto | Requer definição dos campos obrigatórios, tipos e contrato de resposta. | Requer também limites documentados, regras de duplicidade e formas de simular falhas. |
| Contribuição | Estabelece uma base inicial para a cobertura funcional. | Complementa essa base com cenários menos comuns e falhas de integração. |

## 4. Análise da qualidade

O primeiro prompt definiu o papel da LLM, o endpoint, os cenários básicos e um formato estruturado para a resposta. O resultado foi um conjunto de casos organizados, com objetivos e resultados esperados que podem ser revisados antes da implementação.

O segundo prompt acrescentou exemplos de situações excepcionais e instruiu a LLM a priorizar cenários não contemplados nos testes funcionais básicos. Os casos gerados passaram a considerar falhas no armazenamento, limites de campos e consistência entre a resposta da API e os dados persistidos.

Entretanto, a estrutura dos casos não garante que todos os resultados esperados estejam corretos. Como não foi fornecido um contrato formal da API, alguns códigos HTTP e comportamentos foram indicados como hipóteses.

## 5. Diversidade e duplicidade

O segundo prompt ampliou a variedade de cenários, mas também produziu casos com possíveis sobreposições em relação ao primeiro.

### Sobreposições identificadas

- **Formato inválido e tipo incorreto:** o CT-03 do primeiro prompt e o CT-07 do segundo tratam de entradas incompatíveis com o contrato. A distinção pode ser reforçada definindo o primeiro como uma validação geral e o segundo como um teste específico de tipos e efeitos nos componentes.
- **Campo ausente e campo vazio:** o CT-02 e o CT-05 são complementares quando o primeiro verifica a ausência da propriedade e o segundo verifica uma propriedade presente, mas sem conteúdo.
- **Persistência bem-sucedida e falha de persistência:** o CT-04 e o CT-08 têm objetivos diferentes. Um verifica o armazenamento correto; o outro avalia o tratamento de falhas.
- **Persistência e consistência da resposta:** o CT-04 e o CT-10 podem parecer semelhantes. Para diferenciá-los, o CT-04 deve verificar se o registro foi armazenado, enquanto o CT-10 compara os dados armazenados com os valores retornados pela API.

Essa análise indica que a diversidade depende não apenas da quantidade de casos gerados, mas também da distinção entre seus objetivos.

## 6. Ajustes nos prompts

Os prompts foram elaborados com instruções específicas para direcionar os resultados:

1. **Definição do papel:** a LLM foi orientada a atuar como especialista em testes de integração.
2. **Contextualização:** foram informados o endpoint e os componentes envolvidos.
3. **Separação dos objetivos:** o primeiro prompt priorizou os fluxos funcionais, enquanto o segundo enfatizou exceções e limites.
4. **Padronização da saída:** foram solicitados identificador, objetivo, pré-condições, requisição e resultados esperados.
5. **Restrição de suposições:** os prompts instruíram a LLM a não inventar regras de negócio ou códigos HTTP sem documentação.
6. **Tratamento de lacunas:** foram solicitadas premissas e dúvidas a esclarecer antes da implementação.
7. **Exemplos no segundo prompt:** os exemplos ajudaram a explicitar o tipo de cenário esperado e a orientar a geração de testes complementares.

Esses elementos foram incorporados à construção dos prompts. Não foi realizado um experimento controlado para medir quantitativamente o impacto individual de cada instrução.

## 7. Limitações do experimento

A análise foi realizada sobre os casos gerados na LLM a partir de um cenário fictício. Não foi utilizada uma especificação OpenAPI nem executados testes contra uma API real.

Assim, os resultados permitem comparar a estrutura, o foco e a complementaridade dos casos propostos, mas não comprovam a correção dos comportamentos esperados nem a eficácia dos testes em execução.

## 8. Conclusão

A aplicação dos dois prompts resultou em dez casos de teste com objetivos complementares. O primeiro estabeleceu a cobertura funcional inicial, enquanto o segundo ampliou os cenários para incluir exceções, limites e falhas de integração.

A principal contribuição observada foi a possibilidade de direcionar a geração de casos distintos por meio de instruções específicas e exemplos. A análise também mostrou a importância de revisar possíveis sobreposições e de explicitar as regras ainda desconhecidas.

Conclui-se que a GenAI pode apoiar a elaboração de casos de teste de integração, desde que os resultados sejam revisados por uma pessoa e confrontados com o contrato e as regras reais do sistema.