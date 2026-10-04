# Choques do Petróleo e Passthrough Cambial: Uma Abordagem VAR/VECM

Este repositório documenta o desenvolvimento de uma aplicação econométrica em Python para análise de mecanismos de transmissão de choques externos. O projeto utiliza técnicas de séries temporais multivariadas (VAR/VECM) para compreender o impacto das flutuações do preço do barril de petróleo (Brent) e da taxa de câmbio (BRL/USD) sobre a inflação brasileira (IPCA), focando na vulnerabilidade estrutural da economia em cenários de estresse geopolítico e cambial.

## 1. O Problema da Modelagem de Choques Tradicional
Análises macroeconômicas superficiais frequentemente ignoram a endogeneidade entre variáveis ou falham ao não isolar decisões políticas artificiais da dinâmica natural de mercado. Este projeto rejeita regressões lineares simples e univariadas, exigindo um processo robusto de modelagem *step-by-step* que captura a retroalimentação temporal entre inflação, câmbio e commodities, adequado aos padrões institucionais de pesquisa econômica.

## 2. A Arquitetura VAR/VECM
Para mapear a transmissão estrutural da inflação global, este projeto implementa um sistema de Vetores Autorregressivos (VAR) e Modelos de Correção de Erros (VECM). O modelo opera em duas frentes analíticas:

- **Canal Direto (Commodity):** Mensura o encarecimento imediato da matriz de transportes, combustíveis e fretes através das variações internacionais do barril de Petróleo Brent.
- **Canal Indireto (ERPT - Exchange Rate Pass-Through):** Avalia como o comportamento da taxa de câmbio atua como amplificador (quando o dólar sobe junto com o petróleo) ou amortecedor desses choques externos ao longo do tempo.

<img width="1340" height="800" alt="newplot (8)" src="https://github.com/user-attachments/assets/404c0195-894c-43e0-bde5-f0cf433a5f3f" />

## 3. Engenharia de Dados e Isolamento Regulatório
Modelos econométricos colapsam na prática se não considerarem quebras estruturais e ruídos regulatórios. Este código foi desenhado com salvaguardas quantitativas para lidar com intervenções estatais e garantir o alinhamento das séries temporais:

- **Integração Automática e Frequência:** Consumo direto de fontes oficiais via APIs (IBGE/SIDRA e IPEA Data) e U.S. EIA, garantindo a padronização e o alinhamento da frequência mensal dos dados.
- **Variável Dummy Exógena (PPI):** Criação de uma *dummy* para isolar o período de vigência da Política de Paridade de Importação (PPI) da Petrobras (Out/2016 a Mai/2023). Isso impede que o modelo confunda decisões de represamento de preços com a verdadeira dinâmica de mercado.
- **Decomposição da Variância (FEVD):** Medição exata de qual percentual da volatilidade futura do IPCA é explicado pelas oscilações do dólar e do petróleo, revelando o peso de cada fator na inflação.

<img width="900" height="600" alt="newplot (11)" src="https://github.com/user-attachments/assets/4e5db7e5-8df1-4c17-a88d-54aee0b23b10" />*

## 4. Validação Institucional (Robustez Estatística)
Para validar cientificamente a tese de modelagem e evitar regressões espúrias, a série temporal foi submetida a uma bateria de testes rigorosos antes da extração de inferências:

- **Estacionariedade (ADF e KPSS):** Confirmação da ordem de integração das séries (identificação de raízes unitárias e necessidade de diferenciação).
- **Critérios de Informação e Cointegração:** Seleção do número ótimo de defasagens via AIC/BIC e aplicação do Teste de Johansen para verificar relações de equilíbrio de longo prazo, justificando a adoção do modelo VECM.
- **Funções de Resposta ao Impulso (IRF):** Mapeamento dinâmico que ilustra quantos meses a economia real demora para absorver um choque não antecipado (inovação de 1 desvio padrão) no preço do Petróleo e na Taxa de Câmbio.

<img width="612" height="346" alt="WhatsApp Image 2026-10-04 at 13 56 23" src="https://github.com/user-attachments/assets/31e2a28c-2a6a-4bf5-a0c4-75c71a10082f" />

<img width="515" height="470" alt="WhatsApp Image 2026-10-04 at 13 57 29" src="https://github.com/user-attachments/assets/ce882f4e-4cb2-4195-ab42-c7f2a568a92f" />


<img width="1000" height="500" alt="newplot (10)" src="https://github.com/user-attachments/assets/08c5e6ae-45e2-41db-bfb8-da6ab6ea1042" />

## 5. Stack Tecnológico
Infraestrutura desenvolvida inteiramente em Python e renderizada para web:
- `pandas` e `numpy`: Tratamento de séries temporais, defasagens (lags), vetorização e transformações logarítmicas.
- `statsmodels`: Motor econométrico pesado para modelagem multivariada (VAR/VECM) e testes de hipótese estatística.
- `sidrapy`, `ipeadatapy` e `yfinance`: Integração via API para extração de dados macroeconômicos e cotações.
- `Quarto`: Renderização do *Jupyter Notebook* para documento HTML fluido de leitura (`theme: flatly`), embutindo equações matemáticas em LaTeX e outputs gráficos.

## 6. Como Executar o Modelo
1. Clone este repositório: `git clone https://github.com/joaovictoraraujo231234-maker/Choques-de-Petr-leo-via-Pass-through-Cambial-no-IPCA-por-VAR-VECM
.git`
2. Instale as dependências executando: `pip install -r requirements.txt` (incluindo as bibliotecas do IBGE e IPEA).
3. Abra o arquivo `.ipynb` no Jupyter Notebook ou Google Colab para executar o pipeline econométrico bloco a bloco.

## 4. Referências Bibliográficas e Framework Teórico
O modelo integra fundamentos de macroeconomia contemporânea e econometria de séries temporais baseados nas seguintes obras de referência:
- ENDERS, W. *Applied Econometric Time Series*. John Wiley & Sons, 4th ed., 2014.
- LÜTKEPOHL, H. *New Introduction to Multiple Time Series Analysis*. Springer, 2005.
