# Testes de Integração com GenAI

## 1. Objetivo

Este repositório apresenta um experimento de utilização de Inteligência Artificial Generativa (GenAI) para apoiar a geração de casos de teste de integração de software.

O objetivo é comparar duas estratégias de prompting e analisar seus efeitos na qualidade, diversidade e duplicidade dos casos gerados, além de identificar ajustes que contribuam para resultados mais relevantes.

## 2. Cenário de integração

O cenário considerado é uma aplicação que permite cadastrar solicitações de automação por meio do endpoint REST `POST /solicitacoes`.

A API recebe os dados da solicitação, realiza validações e interage com um componente de persistência.

O cenário é fictício e foi utilizado para orientar a geração dos casos de teste.

## 3. Prompts utilizados

Os dois prompts foram aplicados no LLM para gerar casos de teste com objetivos distintos.

| Prompt | Estratégia | Objetivo |
|---|---|---|
| Prompt 1 | Zero-shot | Gerar testes funcionais para validar o fluxo básico da API. |
| Prompt 2 | Few-shot | Gerar testes de exceção, limites e falhas de integração, utilizando exemplos como referência. |

## 4. Estrutura do repositório

```text
testes-integracao-genai/
├── README.md
├── prompts/
│   ├── prompt-01-funcionais.md
│   └── prompt-02-excecoes-limites.md
├── casos-de-teste/
│   ├── testes-funcionais.md
│   └── testes-excecoes-limites.md
└── analise/
    └── comparacao-resultados.md
```

### Descrição dos arquivos

- **`prompts/`**: contém os prompts utilizados no experimento.
- **`casos-de-teste/`**: documenta os casos funcionais e os cenários de exceção e limites gerados.
- **`analise/`**: apresenta a comparação entre os resultados e as observações sobre as duas estratégias.

## 5. Resultados do experimento

A aplicação dos prompts resultou em:

- **4 casos funcionais**, contemplando cadastro válido, ausência de campo obrigatório, formato inválido e verificação da persistência.
- **6 casos de exceção e limites**, contemplando campo vazio, valor-limite, tipo incorreto, falha de persistência, duplicidade e divergência entre resposta e dados armazenados.

Os casos foram analisados quanto à clareza, diversidade, possíveis sobreposições e dependência de regras de negócio ainda não especificadas.

## 6. Critérios de avaliação

- **Qualidade:** clareza dos objetivos, pré-condições e resultados esperados.
- **Diversidade:** variedade de cenários contemplados pelos prompts.
- **Duplicidade:** identificação de casos com objetivos iguais ou semelhantes.
- **Ajustes nos prompts:** análise das instruções que direcionam a geração e ajudam a reduzir ambiguidades.

## 7. Limitações

O cenário não possui uma API real nem um contrato OpenAPI formal. Por isso, alguns códigos HTTP e comportamentos esperados foram apresentados como hipóteses que precisam ser confirmadas.

A avaliação realizada foi documental: os casos gerados foram revisados, mas não foram executados contra uma aplicação real. Portanto, o experimento avalia a utilidade dos prompts para a elaboração de casos de teste, não a aprovação dos testes em execução.

## 8. Conclusão

O experimento permitiu explorar duas estratégias de prompting para objetivos complementares. A abordagem zero-shot foi direcionada à cobertura funcional básica, enquanto a abordagem few-shot enfatizou exceções, limites e falhas de integração.

A comparação dos casos evidencia a importância de especificar o contexto, delimitar o objetivo de cada prompt e revisar os resultados gerados por uma LLM. A análise crítica é necessária para identificar redundâncias, esclarecer premissas e adequar os casos às regras reais do sistema.

## 9. Contexto acadêmico

Atividade acadêmica sobre a aplicação de GenAI na especificação e geração de testes de integração de software.