Aqui está o documento com todos os traços removidos:

---

# Análise de Negócio, NPS Preditivo

> **Projeto:** Tech Challenge Fase 1, Pós-graduação em Ciência de Dados + IA (FIAP)
> **Contexto:** E-commerce nacional com alta variabilidade no NPS entre diferentes perfis de clientes
> **Objetivo:** Transformar dados operacionais em insights acionáveis para antecipar a satisfação do cliente

---

## 1. Qual problema de negócio está sendo resolvido?

O problema central é a incapacidade de agir preventivamente sobre a insatisfação do cliente. Atualmente, o NPS é coletado apenas após o encerramento da jornada de compra, ou seja, quando já é tarde demais para intervir naquele pedido específico.

O e-commerce cresceu em volume e, com isso, passou a lidar com alta variabilidade no NPS entre diferentes perfis de clientes. Mesmo com indicadores operacionais aparentemente similares, alguns clientes tornam-se promotores da marca enquanto outros tornam-se detratores. Isso indica que há fatores específicos, logísticos, de atendimento ou do próprio pedido, que influenciam a experiência de formas distintas.

A empresa precisa transformar dados operacionais em sinais antecipados de insatisfação, permitindo que equipes de logística, atendimento e produto atuem de forma proativa, antes da pesquisa ser aplicada e antes que o cliente vire um detrator.

---

## 2. Por que o NPS é importante para um e-commerce?

O Net Promoter Score vai muito além de uma nota de satisfação. No contexto de e-commerce, ele funciona como um termômetro da saúde do relacionamento com o cliente e tem impacto direto em três dimensões de negócio:

### Recompra
Clientes promotores (nota 9 a 10) têm propensão significativamente maior de voltar a comprar. Em e-commerce, onde o custo de aquisição de novos clientes (CAC) é alto, reter um cliente satisfeito é muito mais rentável do que conquistar um novo. Um NPS baixo é um sinal antecipado de churn.

### Boca a boca
Promotores recomendam ativamente a marca para amigos e familiares, o chamado marketing orgânico. Detratores fazem o oposto: além de não recomprar, compartilham experiências negativas em redes sociais e plataformas como Reclame Aqui, amplificando o dano à reputação da empresa.

### Market share
Em um mercado de e-commerce altamente competitivo, a experiência do cliente é um dos principais diferenciadores. Empresas com NPS consistentemente alto tendem a crescer mais do que a média do mercado porque combinam retenção elevada com aquisição orgânica. Um NPS baixo, por outro lado, aumenta a taxa de abandono e facilita a migração para concorrentes.

---

## 3. Quais áreas se beneficiam dos insights?

| Área | Como se beneficia |
|---|---|
| **Logística** | Identificar se atrasos e múltiplas tentativas de entrega são os principais gatilhos de insatisfação |
| **Atendimento (CS)** | Entender se o volume de contatos e o tempo de resolução impactam o NPS, e priorizar casos de risco |
| **Produto** | Verificar se o valor do pedido, quantidade de itens ou tipo de pagamento influenciam a experiência |
| **Pricing / Comercial** | Avaliar se descontos e frete têm relação com a percepção de valor do cliente |
| **Estratégia** | Usar o modelo preditivo para segmentar clientes em risco e criar campanhas preventivas |

---

## 4. Como o NPS impacta o negócio, reflexão estratégica

### Recompra e retenção
Estudos de mercado indicam que adquirir um novo cliente custa entre 5 e 7 vezes mais do que reter um cliente existente. Isso transforma o projeto de NPS preditivo em um argumento financeiro concreto para a liderança: se for possível identificar clientes em risco de virar detratores antes da pesquisa, a empresa pode agir de forma corretiva e evitar perdas de receita no longo prazo.

### Boca a boca e reputação digital
No e-commerce, a reputação online tem peso direto na taxa de conversão de novos clientes. Avaliações negativas em plataformas públicas reduzem a confiança de potenciais compradores. Um modelo preditivo de NPS permite que a empresa priorize a resolução proativa de casos críticos antes que eles se tornem reclamações públicas.

### Market share e posicionamento competitivo
O NPS é amplamente usado como benchmark competitivo no setor. Empresas como Mercado Livre e Amazon Brasil operam com NPS acima de 50 pontos, um referencial importante para contextualizar os resultados desta análise.

---

## 5. Indicadores de mercado complementares

Para enriquecer a análise e contextualizar os resultados internos, os seguintes benchmarks externos são relevantes:

- NPS do setor de e-commerce: Média brasileira entre 30 e 50 pontos. Posicionar a empresa nesse espectro ajuda a calibrar o nível de urgência das ações.
- SLA logístico regional: O prazo médio de entrega varia por região, Sul e Sudeste tendem a ser mais rápidos que Norte e Nordeste. Comparar `delivery_time_days` com benchmarks regionais ajuda a separar problemas estruturais de problemas operacionais.
- Taxa de reclamação no Reclame Aqui: Alta correlação com NPS baixo. Pode ser usada como validação externa do modelo.
- Custo de aquisição vs. retenção (CAC vs. LTV): Argumento financeiro para justificar investimento em melhoria de experiência.

---

## 6. Definição da variável target

### Qual variável representa a satisfação do cliente?
A variável `nps_score`, que registra a nota de 0 a 10 atribuída pelo cliente após a experiência de compra.

### Por que ela foi escolhida?
Porque é a única variável na base que captura diretamente a percepção subjetiva do cliente sobre toda a jornada. As demais variáveis são operacionais, elas descrevem o que aconteceu, mas não como o cliente se sentiu em relação ao que aconteceu.

### Em que momento da jornada essa informação é coletada?
Após o encerramento completo da jornada de compra, depois da entrega, do pagamento e de eventual contato com o atendimento. Isso significa que o NPS é um indicador retrospectivo, não em tempo real.

### Classificação utilizada no modelo

Para fins de modelagem preditiva, o `nps_score` será convertido em 3 categorias seguindo a metodologia padrão do NPS:

| Nota | Categoria |
|---|---|
| 0 a 6 | Detrator |
| 7 a 8 | Neutro |
| 9 a 10 | Promotor |

Essa abordagem de classificação é preferível à regressão contínua porque:
1. A empresa não precisa saber a nota exata, precisa saber quem está em risco
2. Permite ações segmentadas por categoria (ex: acionar CS para detratores prováveis)
3. É mais robusta a ruídos na coleta da nota

### Riscos de uso inadequado da variável

Data Leakage com `csat_internal_score`: Essa variável é um score interno de satisfação provavelmente calculado a partir do próprio NPS ou coletado no mesmo momento. Usá-la como feature do modelo seria uma forma de "trapacear", o modelo estaria usando informação que não estaria disponível no momento em que a previsão precisaria ser feita na prática. Ela será excluída do modelo.

Viés de resposta: Clientes que respondem à pesquisa de NPS tendem a ser os mais satisfeitos ou os mais insatisfeitos, os neutros frequentemente não respondem. Isso pode criar um viés na base de dados que o modelo aprende e reproduz.

Uso como métrica absoluta: O NPS não deve ser usado isoladamente para tomar decisões. Uma nota 7 pode ser satisfatória em um setor e insatisfatória em outro. O contexto sempre importa.

