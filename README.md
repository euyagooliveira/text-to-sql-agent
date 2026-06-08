#  Agente Text-to-SQL com LLM

Agente inteligente que converte perguntas em linguagem natural para consultas SQL, executa no banco de dados e responde em português — sem o usuário precisar saber nada de SQL.

---

##  Como funciona

```
Usuário faz uma pergunta em português
        ↓
Guardrail valida se a pergunta é relevante
        ↓ (sim)
LLM (LLaMA 3.3) gera o SQL automaticamente
        ↓
SQLite executa a consulta no banco de dados
        ↓
LLM formata a resposta em português
        ↓
Usuário recebe a resposta com contexto do histórico
```

---

##  Arquitetura

O agente é composto por 4 camadas principais:

**1. Guardrail** — valida se a pergunta faz sentido para o banco de dados antes de processar. Perguntas fora do escopo são bloqueadas imediatamente.

**2. Geração de SQL** — o LLM recebe a pergunta + o schema do banco via system prompt e gera o SQL correto, incluindo JOINs complexos e funções de agregação.

**3. Execução** — o SQL é executado no SQLite e os dados retornados são estruturados em colunas e linhas.

**4. Resposta em português** — os dados brutos são enviados de volta ao LLM que formata uma resposta clara e objetiva em português.

---

##  Exemplos de perguntas

| Pergunta | SQL gerado |
|---|---|
| Quais clientes são de MG? | `SELECT * FROM clientes WHERE estado = 'MG'` |
| Qual o produto mais vendido? | `SELECT ... GROUP BY ... ORDER BY SUM(quantidade) DESC LIMIT 1` |
| Qual o total gasto por cliente? | `SELECT nome, SUM(preco * quantidade) ... JOIN ... GROUP BY` |
| Total de vendas em 2023 e 2024? | `SELECT SUM(CASE WHEN STRFTIME('%Y'...) ...)` |

---

## Tecnologias

- **Groq API** — LLM rápido e gratuito (LLaMA 3.3 70B)
- **SQLite** — banco de dados leve, sem necessidade de servidor
- **Python puro** — sem frameworks, código simples e didático

---

##  Funcionalidades

- ✅ Conversão de linguagem natural para SQL
- ✅ Guardrail para perguntas fora do escopo
- ✅ Histórico de conversa — agente lembra o contexto
- ✅ Tratamento de erros robusto
- ✅ Resposta sempre em português

---

## Como executar

1. Acesse o notebook pelo Google Colab
2. Crie uma conta gratuita em [console.groq.com](https://console.groq.com) e gere uma API key
3. Insira sua API key na célula de configuração
4. Execute todas as células em ordem

---



**Yago Oliveira**  
Cientista de Dados | Staff AI Engineer  
[GitHub](https://github.com/euyagooliveira) 
