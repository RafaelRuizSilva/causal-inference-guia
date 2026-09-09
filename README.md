# Árvore de Decisão da Inferência Causal

Um mapa de perguntas que leva de **"qual é a minha pergunta causal?"** até o **método certo** para respondê-la.

🔗 **Online:** https://causal-inference-guia.vercel.app

---

## O que é isto

Uma página única (HTML, sem dependências) com uma árvore de decisão interativa. Você clica em cada nó e vê:

- as **hipóteses** que aquele método exige para funcionar;
- os **métodos principais** para aquele caso;
- um **exemplo em Python** com um cenário do Mercado Livre (dados sintéticos, material de estudo).

A ideia é simples: antes de sair rodando regressão, primeiro decidir *qual pergunta* você está fazendo e *o que o mundo te deixa medir*. O método vem depois.

## O caminho que a árvore percorre

1. **Defina o alvo antes do método** — escreva o "ensaio-alvo" (*target trial*): o experimento que você faria se pudesse.
2. **Você consegue randomizar o tratamento?**
   - Sim → RCT / Teste A/B, ou Switchback / Geo-experimento.
   - Não → segue para a próxima pergunta.
3. **Existe uma variação quase-aleatória no mundo?** (um corte de regra, um choque externo, um instrumento)
   - Regressão Descontínua (RDD), Variáveis Instrumentais (IV / 2SLS), Diferença em Diferenças (DiD), Controle Sintético.
4. **Você mediu todos os confundidores?**
   - Sim → ajuste por covariáveis observadas; efeitos heterogêneos (CATE / uplift).
   - Não → análise de sensibilidade + *bounds*.
5. **Tratamento e confundidores mudam ao longo do tempo?** → métodos para dados longitudinais.
6. Em volta de tudo: **desenhe o DAG antes de estimar** e faça **cheques de robustez depois de estimar**.

## Onde ler cada coisa

A árvore é uma síntese. A profundidade está em dois livros, os dois gratuitos:

- **Hernán & Robins — *Causal Inference: What If*** — texto de referência da área ([PDF em Harvard](https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/)).
- **Matheus Facure — *Causal Inference for the Brave and True*** — em Python, [online e gratuito](https://matheusfacure.github.io/python-causality-handbook/).

A própria página tem uma tabela cruzando cada tema com os capítulos dos dois livros.

## Como rodar localmente

É um arquivo estático. Basta abrir no navegador:

```bash
# opção 1: abrir direto
start Arvore-Decisao-Inferencia-Causal-MELI.html   # Windows

# opção 2: servir localmente
python -m http.server 8000
# depois acesse http://localhost:8000/Arvore-Decisao-Inferencia-Causal-MELI.html
```

## Deploy

Hospedado no **Vercel**, com deploy automático a cada `push` na branch `main`.

O [vercel.json](vercel.json) faz a raiz (`/`) servir a árvore de decisão:

```json
{ "rewrites": [ { "source": "/", "destination": "/Arvore-Decisao-Inferencia-Causal-MELI.html" } ] }
```

## Estrutura

| Arquivo | O que é |
| --- | --- |
| `Arvore-Decisao-Inferencia-Causal-MELI.html` | a árvore de decisão interativa (o conteúdo do site) |
| `vercel.json` | configuração do deploy estático |
| `.gitignore` | mantém o resumo do curso apenas localmente |

---

*Material didático. Os cenários do Mercado Livre usam dados sintéticos e servem só como exemplo.*
