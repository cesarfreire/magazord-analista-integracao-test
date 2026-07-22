# Teste Prático - Analista de Integrações

# Teste Prático – Analista de Negócios (Integrações, APIs e Qualidade)

Este repositório contém o **Teste Prático para Avaliação de Candidatos à vaga de Analista de Negócios** com foco em **Integrações Terceiras, APIs e Garantia de Qualidade (QA)**.

---

## 🎯 Objetivo da Avaliação

Avaliar a capacidade analítica e técnica do candidato em:
- Compreender fluxos de negócio e arquitetura de integração via APIs (REST, JSON, Webhooks).
- Diagnosticar falhas, analisar logs e mitigar problemas de comunicação entre sistemas.
- Mapear e especificar requisitos funcionais e não funcionais para equipes de desenvolvimento.
- Estruturar casos e cenários de teste de borda/qualidade.
- Priorizar demandas considerando impacto operacional, esforço técnico e valor de negócio.

---

## 📊 Estrutura do Teste & Pontuação

| Etapa | Foco da Avaliação | Pontuação |
| :--- | :--- | :---: |
| **Etapa 1** | Conceitos Básicos de APIs, Protocolos e Status HTTP | 15 pts |
| **Etapa 2** | Investigação e Análise de Falhas | 20 pts |
| **Etapa 3** | Prática Hands-on: API E-commerce / Magazord | 25 pts |
| **Etapa 4** | Especificação de Requisitos e User Stories | 25 pts |
| **Etapa 5** | Priorização e Visão de Negócio | 15 pts |
| **Total** | | **100 pts** |

---

## 📝 Questões da Avaliação

### Etapa 1 – Conceitos Básicos de APIs e Protocolos (15 pontos)

#### Questão 1 (10 pontos)
Responda de forma objetiva aos conceitos abaixo:
1. O que é uma API REST e qual a diferença de aplicação entre os métodos **GET, POST, PUT, PATCH e DELETE**?
2. O que significa uma autenticação via **Bearer Token** no cabeçalho (*Header*) de uma requisição HTTP?
3. O que indicam as famílias de status code HTTP **2xx, 4xx e 5xx**?

#### Questão 2 (5 pontos)
Em qual situação funcional você recomendaria a utilização de cada um dos códigos HTTP abaixo em uma API de integração?
- `200 OK` vs. `201 Created`
- `400 Bad Request` vs. `401 Unauthorized` vs. `422 Unprocessable Entity`
- `500 Internal Server Error`

---

### Etapa 2 – Investigação e Análise de Falhas (20 pontos)

#### Questão 3 (10 pontos)
Um cliente relata:  
> *"Ao tentar consultar o status de faturamento de uma Nota Fiscal via integração, o sistema exibe apenas o erro genérico: 'Falha na comunicação com o parceiro'."*

- Quais perguntas você faria ao cliente ou ao parceiro para delimitar o problema?
- Quais verificações prévias (logs, ferramentas de teste de API como Postman/Insomnia, payloads, cabeçalhos) você realizaria antes de acionar a equipe de desenvolvimento?

#### Questão 4 (10 pontos)
Considere que um parceiro tentou incluir um lote de pedidos e recebeu o seguinte retorno JSON:

```json
{
  "success": false,
  "message": "Erro ao importar dados."
}
```

- Explique por que esse retorno é inadequado para o ecossistema de integração de e-commerce/ERP.
- Reescreva este JSON propondo uma **estrutura ideal de resposta** para falhas em lote ou validação de campos, permitindo que o sistema de origem identifique exatamente qual item e qual campo falhou.

---

### Etapa 3 – Prática Hands-on: API E-commerce / Magazord (25 pontos)

Considere a documentação oficial da [API Magazord](https://docs.api.magazord.com.br/) como referência de contexto de e-commerce/ERP para responder aos exercícios abaixo.

#### Questão 5 – Consulta de Nota Fiscal / Pedido (10 pontos)
Imagine que o time comercial precisa validar se as Notas Fiscais dos pedidos faturados estão disponíveis para sincronização com o WMS/ERP terceiro.
1. Indique qual o método HTTP e qual a estrutura de endpoint/recurso tipicamente utilizado para consultar um pedido ou Nota Fiscal por ID/Chave.
2. Monte o exemplo de um **Header** de requisição mínimo necessário para realizar essa consulta (considerando autenticação e formato de dados).

#### Questão 6 – Análise de Payload e Cenários de Teste (15 pontos)
Analise a estrutura abaixo referente ao payload JSON de criação de um pedido de venda:

```json
{
  "codigoPedidoCliente": "PED-99823",
  "dataCriacao": "2026-07-22T10:00:00Z",
  "cliente": {
    "nome": "João da Silva",
    "cpfCnpj": "12345678900",
    "email": "joao@email.com"
  },
  "itens": [
    {
      "sku": "CAMISA-AZUL-G",
      "quantidade": 2,
      "precoUnitario": 59.90
    }
  ],
  "pagamento": {
    "formaPagamento": "PIX",
    "valorTotal": 119.80
  }
}
```

- Identifique pelo menos **3 cenários de testes de borda e garantia de qualidade (QA)** que você executaria para garantir a robustez e integridade dessa API de inclusão (ex: divergência de valores, validação de caracteres/máscara, estoque, idempotência).

---

### Etapa 4 – Especificação de Requisitos e Histórias de Usuário (25 pontos)

#### Questão 7 (25 pontos)
Transforme a dor de negócio descrita a seguir em uma **Especificação Técnica e Funcional** completa para o time de engenharia:

> *"Durante a importação em lote de pedidos via API, quando um único item da lista estiver sem estoque, o sistema atualmente cancela e rejeita a requisição inteira. Precisamos que a API permita processar os itens disponíveis e retorne um relatório de sucesso parcial informando exatamente quais itens falharam e o motivo."*

Sua especificação deve conter obrigatoriamente:
1. **Objetivo & Problema Atual**
2. **Regras de Negócio (RNs)**
3. **Critérios de Aceite (Definition of Done)**
4. **Exemplo de Payload de Resposta esperada** (Estrutura de Erro/Sucesso Parcial com HTTP 207 Multi-Status ou HTTP 422 tratado)
5. **Matriz de Impacto e Riscos** (o que pode ser afetado no ERP, estoque ou faturamento)

---

### Etapa 5 – Priorização e Visão de Negócio (15 pontos)

#### Questão 8 (15 pontos)
Ordene as demandas abaixo por ordem de prioridade (da **mais urgente/importante** para a **menos urgente**) sob a ótica de **Qualidade, Estabilidade e Valor de Negócio**, justificando resumidamente o motivo de cada escolha:

1. **Ajuste em endpoint existente** para retornar mensagens de erro mais detalhadas em vez de erros genéricos.
2. **Correção de bug crítico** em produção onde a API não está registrando a Chave da Nota Fiscal/Código de Rastreio nos pedidos faturados.
3. **Inclusão de um novo campo opcional** no endpoint de cadastro de produtos solicitada por um cliente pontual.
4. **Desenvolvimento de uma nova integração** solicitada por um parceiro logístico estratégico para fechar um contrato relevante.
5. **Atualização da documentação (Swagger)** de endpoints legados.

---

## 📐 Critérios Globais de Avaliação

| Critério de Avaliação | Descrição do Foco | Peso % |
| :--- | :--- | :---: |
| **Conhecimento em APIs & Protocolos** | Domínio sobre verbos, status HTTP, JSON e autenticação em integrações. | 20% |
| **Capacidade Analítica & QA** | Habilidade de investigar falhas, formular perguntas de negócio e prever cenários de teste de borda. | 25% |
| **Estruturação de Requisitos** | Clareza, objetividade e riqueza de detalhes ao transformar dores em regras e critérios de aceite. | 25% |
| **Orientação a Negócios & Priorização** | Tomada de decisão ponderando impacto financeiro, relacional e esforço técnico. | 15% |
| **Prática Hands-On (E-commerce / APIs)** | Familiaridade com estruturas de payloads de pedidos/notas fiscais de e-commerce. | 15% |

---
*Documento preparado para processo seletivo da área de Qualidade e Análise de Negócios em Integrações.*


