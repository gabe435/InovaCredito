<div align="center">
  <img src="static/images/logo.png" alt="Logo InovaCrédito" width="180" />
  <h1>InovaCrédito</h1>
  <p><strong>Plataforma de Análise de Risco e Crédito Inclusivo para Pessoa Física</strong></p>

  <p>
    <img src="https://img.shields.io/badge/Status-Conclu%C3%ADdo%20(Sprint%203)-2e9e44?style=for-the-badge" alt="Status do Projeto" />
    <img src="https://img.shields.io/badge/FATEC-API%201%C2%BA%20DSM-083b66?style=for-the-badge" alt="FATEC API DSM" />
    <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
    <img src="https://img.shields.io/badge/Flask-Web%20App-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask" />
  </p>
</div>

---

## Sumário

* [Descrição do Desafio](#descrição-do-desafio)
* [Product Backlog](#product-backlog)
* [Cronograma de Sprints e Burndown](#cronograma-de-sprints-e-burndown)
* [Metodologia do Score de Vulnerabilidade (US07)](#metodologia-do-score-de-vulnerabilidade-us07)
* [Fontes de Dados Oficiais](#fontes-de-dados-oficiais)
* [Tecnologias e Arquitetura](#tecnologias-e-arquitetura)
* [Estrutura do Projeto](#estrutura-do-projeto)
* [Como Executar Localmente](#como-executar-localmente)
* [Equipe](#equipe)

---

## Descrição do Desafio

No mercado brasileiro de crédito para Pessoa Física, análises superficiais costumam gerar dois extremos prejudiciais: negar acesso a perfis com capacidade real de pagamento ou ofertar linhas de alto custo para públicos em situação de vulnerabilidade, alimentando o superendividamento.

O **InovaCrédito** foi desenvolvido como **API (Aprendizagem por Projeto Integrado)** no 1º semestre do curso de **Desenvolvimento de Software Multiplataforma (DSM)** para enfrentar esse cenário. Nossa plataforma web integra bases públicas oficiais — **Banco Central do Brasil (SCR e API Olinda)**, **IBGE (SIDRA)** e **Ministério da Fazenda** — transformando dados brutos em inteligência regional, comparativos históricos e recomendações práticas de produtos de crédito.

---

## Product Backlog

| ID | Sprint | Prioridade | User Story | Critérios de Aceite | Status |
| :---: | :---: | :---: | :--- | :--- | :---: |
| **US01** | 1 | Alta | **Como analista de crédito**, quero comparar a carteira de inadimplência com os valores a vencer em até 90 dias por UF e Região, para identificar mercados com maior capacidade de recuperação rápida. | - Extração e limpeza dos arquivos anuais do SCR (2024–2026) para Pessoa Física.<br>- Gráficos comparativos por UF e por Grande Região.<br>- Filtro regional dinâmico funcional na interface web. | Concluída |
| **US02** | 1 | Alta | **Como analista de risco**, quero visualizar a proporção entre dívida saudável (patrimonial) e dívida crítica (alto custo), para avaliar a qualidade do endividamento em cada região. | - Classificação das submodalidades do SCR entre dívida saudável (imóveis, veículos) e crítica (rotativo, cheque especial, crédito pessoal).<br>- Gráficos percentuais empilhados por estado e região. | Concluída |
| **US03** | 1 | Alta | **Como analista de mercado**, quero comparar as taxas de juros das maiores instituições financeiras em uma mesma modalidade, para garantir benchmarks justos de precificação. | - Consumo da API Olinda (`TaxasJurosMensalPorMes`).<br>- Filtro padronizado no Financiamento Imobiliário pós-fixado em TR (taxas de mercado).<br>- Gráfico do mês mais recente e série histórica desde jan/2024. | Concluída |
| **US04** | 2 | Média | **Como gestor de crédito**, quero monitorar a evolução mensal de depósitos e apostadores em plataformas de apostas (Bets), para mensurar o impacto desse comportamento no orçamento familiar. | - Integração dos dados mensais consolidados do Ministério da Fazenda.<br>- Visualização conjunta do volume financeiro (R$ bilhões) e número de apostadores (milhões). | Concluída |
| **US05** | 2 | Média | **Como analista regional**, quero consultar indicadores demográficos, IDH e renda per capita por estado, para contextualizar o potencial econômico de cada UF. | - Consulta de dados estaduais do IBGE.<br>- Cards de KPI (Área, IDH 2021 e Densidade Demográfica).<br>- Gráfico de duplo eixo cruzando População e Renda Per Capita (2022–2025). | Concluída |
| **US06** | 3 | Alta | **Como tomador de decisão**, quero acompanhar a evolução histórica real da renda mensal entre 2012 e 2025, para avaliar a trajetória do poder de compra por região e comparar estados. | - Consumo direto da API SIDRA/IBGE (Tabela 7437).<br>- Alternância entre visão por Regiões, por Estado e Comparação Multiestados.<br>- Tabela resumo automática com valor inicial, final, variação em R$, percentual e tendência. | Concluída |
| **US07** | 3 | Alta | **Como tomador de decisão**, quero um Score de Vulnerabilidade regional e estadual vinculado a recomendações de produto, para direcionar a oferta de crédito mais adequada a cada perfil. | - Cruzamento da Tabela 4099 do IBGE (desocupação e subutilização) com a taxa média de juros da API Olinda.<br>- Cálculo do Score ($0$ a $100$) e do Índice de Possível Inadimplência.<br>- Gráficos de corte, ranking Top 10 UFs e tabelas com recomendação automática de produto. | Concluída |
| **US08** | 3 | Alta | **Como usuário final**, quero acessar todas as análises em uma plataforma web unificada e responsiva, para explorar os indicadores com filtros interativos sem depender de notebooks. | - Migração completa dos scripts do Google Colab para servidor Flask.<br>- Interface em HTML5 e CSS3 seguindo a identidade visual da InovaCrédito.<br>- Sistema de cache local (CSV) e em memória para carregamento rápido e resiliente. | Concluída |

---

## Cronograma de Sprints e Burndown

| Sprint | Foco da Entrega | User Stories | Status |
| :---: | :--- | :---: | :---: |
| **Sprint 1** | Coleta, tratamento e visualizações iniciais do Banco Central (SCR e Olinda) | US01, US02, US03 | Entregue |
| **Sprint 2** | Ampliação socioeconômica com impacto das Bets e indicadores demográficos do IBGE | US04, US05 | Entregue |
| **Sprint 3** | Série histórica de renda, motor de Score/Recomendação e entrega da plataforma web Flask | US06, US07, US08 | Entregue |

> **Burndown da Sprint 3:** O backlog da entrega final (US06, US07 e US08) foi concluído de forma linear e zerado com **1 dia de antecedência** em relação à data planejada, permitindo tempo dedicado para testes integrados, otimização de cache e validação visual.
>
> *(Opcional: salve o print do Burndown em `docs/burndown-sprint3.png` e descomente a linha abaixo para exibi-lo no GitHub)*
> <!-- ![Burndown Sprint 3](docs/burndown-sprint3.png) -->

---

## Metodologia do Score de Vulnerabilidade (US07)

O motor de decisão da **US07** cruza os dados trimestrais mais recentes da PNAD Contínua (**IBGE SIDRA — Tabela 4099**) com a taxa média mensal de juros de referência da **API Olinda (BCB)**:

1. **Pressão de Informalidade:** diferença entre a Taxa Composta de Subutilização e a Taxa de Desocupação.
2. **Normalização:** cada componente é normalizado pelo maior valor observado na amostra (região ou UF) para manter a escala proporcional entre $0$ e $100$.
3. **Score de Vulnerabilidade ($0$ a $100$):**

$$
\text{Score} = \left( 0{,}40 \cdot \text{Desocupação}_{\text{norm}} + 0{,}40 \cdot \text{Subutilização}_{\text{norm}} + 0{,}20 \cdot \text{Informalidade}_{\text{norm}} \right) \times 100
$$

4. **Índice de Possível Inadimplência (%):**

$$
\text{Inadimplência Estimada} = \left( 0{,}60 \cdot \text{Desocupação} + 0{,}40 \cdot \text{Subutilização} \right) \times \left( 1 + \frac{\text{Juros Médio BCB}}{10} \right)
$$

5. **Faixas de Recomendação de Produto:**

| Faixa de Score | Nível de Vulnerabilidade | Produto Recomendado |
| :---: | :---: | :--- |
| $\ge 65$ | Alta | **Microcrédito Orientado** |
| $45 \text{ a } 64{,}99$ | Moderada | **Crédito Alternativo** |
| $< 45$ | Baixa | **Crédito Tradicional** |

---

## Fontes de Dados Oficiais

* **Banco Central do Brasil (SCR — Dados Abertos):** arquivos anuais compactados (`scrdata_2024.zip` a `scrdata_2026.zip`) filtrados para carteira de Pessoa Física.
* **Banco Central do Brasil (API Olinda):** serviço OData `TaxasJurosMensalPorMes` (v2).
* **IBGE (API SIDRA — Tabela 7437):** rendimento médio mensal real da população residente com rendimento (2012–2025).
* **IBGE (API SIDRA — Tabela 4099):** taxa de desocupação (variável `4099`) e taxa composta de subutilização da força de trabalho (variável `4118`).
* **Ministério da Fazenda & IBGE (Bases Consolidadas):** série mensal do mercado de apostas (Bets) e indicadores demográficos estaduais.

---

## Tecnologias e Arquitetura

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas" />
  <img src="https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge" alt="Matplotlib" />
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
  <img src="https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white" alt="Google Colab" />
  <img src="https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white" alt="VS Code" />
</p>

* **Backend e ETL (`app.py`):** servidor Flask que recebe filtros via parâmetros `GET`, processa grandes volumes do SCR em *chunks* com Pandas e gera gráficos no backend `Agg` do Matplotlib convertidos em Base64.
* **Estratégia de Cache e Resiliência:**
  * Persistência em CSV local (`dados_scr/`) para os dados agregados do SCR e da API Olinda (com `User-Agent` dedicado e parada antecipada de paginação);
  * Cache em memória para as APIs do IBGE e Ministério da Fazenda, além de tratamento de exceções (`try/except` com `timeout`) para impedir quedas da aplicação caso algum serviço externo oscile.
* **Frontend (`templates/` e `static/`):** HTML5 semântico com Jinja2, CSS3 responsivo em CSS Grid, navegação fixa por âncoras para cada US e paleta de cores baseada na identidade visual da logo.

---

## Estrutura do Projeto

```text
API_INOVA/
├── app.py                     # Servidor Flask, pipelines ETL, cache e geração de gráficos
├── dados_scr/                 # Cache local gerado automaticamente (SCR e API Olinda)
├── templates/
│   └── index.html             # Interface principal com filtros interativos e tabelas
└── static/
    ├── css/
    │   └── style.css          # Estilização responsiva e variáveis de tema
    └── images/
        ├── logo.png           # Logotipo oficial da InovaCrédito
        └── background.jpg     # Fundo do banner principal (opcional)
```

---

## Como Executar Localmente

### Pré-requisitos
* **Python 3.10+**
* **Git**

### Passo a passo

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
   cd API_INOVA
   ```

2. **Crie e ative o ambiente virtual (`venv`):**
   * **Linux / macOS:**
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```
   * **Windows (PowerShell):**
     ```powershell
     python -m venv venv
     .\venv\Scripts\Activate
     ```

3. **Instale as dependências:**
   ```bash
   pip install flask pandas requests matplotlib
   ```

4. **Execute a aplicação:**
   ```bash
   python3 app.py
   ```
   *(No Windows, utilize `python app.py`)*

5. **Acesse no navegador:**
   Abra [http://127.0.0.1:5000](http://127.0.0.1:5000).

> **Dica para o primeiro acesso:** as seções da **API Olinda (US03)**, **Bets (US04)** e **IBGE (US05, US06 e US07)** são carregadas automaticamente e armazenadas em cache. Para baixar e agregar os arquivos pesados da **Base SCR (US01 e US02)** pela primeira vez, clique no botão **"Baixar e Processar Base SCR Agora"** na primeira seção do site.

---

## Equipe

| Integrante | Papel | LinkedIn | GitHub |
| :--- | :--- | :---: | :---: |
| **Gabriel Hatano Rocha** | Product Owner (PO) | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/SEU-LINKEDIN-GABRIEL) | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/SEU-GITHUB-GABRIEL) |
| **João Manoel de Almeida Sales e Silva** | Scrum Master (SM) | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/SEU-LINKEDIN-JOAO) | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/SEU-GITHUB-JOAO) |
| **Enzo Zani** | Developer | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/SEU-LINKEDIN-ENZO) | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/SEU-GITHUB-ENZO) |
| **Luan Henrique Borsoi Alves** | Developer | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/SEU-LINKEDIN-LUAN) | [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/SEU-GITHUB-LUAN) |