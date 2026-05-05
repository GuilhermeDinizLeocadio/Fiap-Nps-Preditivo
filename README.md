# NPS Preditivo — Tech Challenge Fase 1

> Projeto desenvolvido como parte da Pós-graduação em Ciência de Dados + IA  
> FIAP PosTech — Turma 1IAST

## Objetivo do projeto

Transformar dados operacionais de um e-commerce (pedidos, logística e
atendimento) em insights acionáveis capazes de antecipar a satisfação
do cliente, medida pelo Net Promoter Score (NPS) antes da aplicação
da pesquisa.

## Problema de negócio

Atualmente o NPS é coletado apenas após o encerramento da jornada de
compra, limitando a capacidade da empresa de agir preventivamente.
Este projeto busca identificar os fatores operacionais que mais
influenciam a satisfação e construir um modelo preditivo capaz de
classificar clientes como Promotores, Neutros ou Detratores.

## Descrição da base de dados

Base histórica de pedidos de e-commerce com 19 variáveis, incluindo:

- **Dados do cliente:** idade, região, tempo de relacionamento
- **Dados do pedido:** valor, itens, desconto, parcelas
- **Dados logísticos:** tempo de entrega, atraso, tentativas
- **Dados de atendimento:** contatos, tempo de resolução, reclamações
- **Target:** `nps_score` (0 a 10) → convertido em Detrator / Neutro / Promotor

## Estrutura do repositório
```
fiap-nps-preditivo/
│
├── data/
│   ├── raw/                  # Base original (nunca modificada)
│   └── processed/            # Dados após limpeza e feature engineering
│
├── notebooks/
│   ├── 01_eda.ipynb          # Análise exploratória
│   ├── 02_preprocessing.ipynb
│  
│
├
│
├── reports/
│   ├── figures/              # Gráficos exportados
│   └── analise_negocio.md    # Análise e entendimento do negócio
│
└── README.md
```

## Documentação

- [Análise de Negócio](reports/analise_negocio.md)

> **Nota:** O arquivo CSV foi incluído neste repositório 
> exclusivamente para fins educativos e reprodutibilidade. 
> Em ambiente de produção, dados brutos não devem ser 
> versionados no Git.

## Metodologia

1. **Entendimento do negócio** — análise do problema e definição da target
2. **EDA** — análise exploratória com foco em insights de negócio
3. **Pré-processamento** — limpeza, encoding e feature engineering
4. **Modelagem** — classificação em 3 classes (Detrator / Neutro / Promotor)
5. **Avaliação** — métricas e interpretabilidade com SHAP
6. **Storytelling** — apresentação gerencial dos resultados

## Como reproduzir
```bash
# 1. Clone o repositório
git clone https://github.com/GuilhermeDinizLeocadio/Fiap-Nps-Preditivo.git
cd Fiap-Nps-Preditivo

# 2. Instale as dependências
pip install -r requirements.txt

# 3. Execute os notebooks na ordem numérica
jupyter notebook
```

## Tecnologias utilizadas

- Python 3.10+
- pandas, numpy
- matplotlib, seaborn
- scikit-learn
- xgboost
- shap

## Apresentação e Vídeo

- [Slides da Apresentação](reports/NPS%20PREDITIVO.pdf)
- [Vídeo Executivo](https://drive.google.com/file/d/1a00I94VwIAuutmfZNcsP6a-ENavLLfUq/view?usp=sharing)

## Autor

Guilherme Diniz Leocadio
