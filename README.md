# Projeto Big Data IPCA

## Tema do projeto
Análise da evolução da inflação brasileira com base no IPCA, utilizando Python e dados oficiais do IBGE.

## Objetivo
O objetivo deste projeto é coletar automaticamente a série histórica do IPCA mensal, tratar os dados, calcular estatísticas descritivas e gerar visualizações que mostrem o comportamento da inflação no Brasil ao longo do tempo.

## Fonte dos dados
- Instituto Brasileiro de Geografia e Estatística (IBGE)
- Sistema IBGE de Recuperação Automática (SIDRA)
- Endpoint utilizado: `https://apisidra.ibge.gov.br/values/t/1737/n1/all/v/63/p/all?format=json`

## Por que foi usada a variação mensal do IPCA
O projeto utiliza a variação mensal do IPCA (`v/63`) porque esse indicador representa diretamente a taxa de inflação observada em cada mês. Isso facilita a análise estatística, a identificação de máximos e mínimos históricos e a comparação da média anual da inflação.

## Bibliotecas utilizadas
- `requests`
- `pandas`
- `matplotlib`
- `numpy`
- `scikit-learn`
- `streamlit`

## Como instalar
```bash
pip install -r requirements.txt
```

## Como executar a análise principal
```bash
python main.py
```

## Como executar o painel
```bash
pip install -r requirements.txt
python main.py
streamlit run dashboard.py
```

Se o preview da IDE perder a conexão, abra o painel diretamente no navegador em `http://localhost:8501`.
O projeto inclui configuração local do Streamlit para reduzir reinicializações automáticas no Windows.

## Funcionamento do sistema
Ao executar o projeto, o script principal:

1. consulta automaticamente todos os registros disponíveis do IPCA mensal na API do IBGE;
2. remove a primeira linha descritiva da resposta;
3. utiliza os campos reais `D3C`, `D3N` e `V`;
4. converte os dados para um `DataFrame`;
5. organiza a série histórica em ordem cronológica;
6. calcula estatísticas descritivas da inflação, incluindo a comparação com o período após o Plano Real;
7. exporta os dados tratados para CSV;
8. gera três gráficos em formato PNG;
9. informa no terminal o último período disponível e o último valor retornado pela API.

## Painel interativo
O arquivo `dashboard.py` cria um painel em Streamlit para apresentação acadêmica do projeto. O painel:

- lê os dados diretamente de `dados/dados_ipca.csv`;
- mostra o período mais recente disponível;
- exibe métricas com `st.metric`;
- apresenta gráficos da série histórica, média anual, comparação com o período após o Plano Real e tendência simples;
- orienta o usuário a executar `python main.py` caso o CSV ainda não exista.

## Observação para apresentação
Para uma apresentação mais completa, o projeto pode ser demonstrado de duas formas:

- `python main.py`: mostra a análise textual no terminal e regenera os arquivos do projeto;
- `streamlit run dashboard.py`: abre o painel interativo para uma visualização mais bonita e intuitiva.

## Arquivos gerados
Os arquivos abaixo são gerados localmente pela execução do projeto e não precisam ser versionados no repositório:

- `dados/dados_ipca.csv`: base tratada com as colunas `Data`, `Codigo_Periodo`, `Periodo`, `IPCA`, `Ano` e `Mes`.
- `graficos/evolucao_ipca.png`: gráfico de linha com a evolução histórica do IPCA mensal.
- `graficos/media_anual.png`: gráfico de barras com a média anual do IPCA mensal.
- `graficos/tendencia_ipca.png`: gráfico da série histórica com linha de tendência calculada por regressão linear simples.

## Explicação dos gráficos gerados pelo main.py
- `evolucao_ipca.png`: apresenta a evolução completa do IPCA mensal ao longo da série histórica.
- `media_anual.png`: resume a média anual do IPCA mensal para cada ano disponível.
- `tendencia_ipca.png`: mostra a série histórica acompanhada de uma linha de tendência linear, sem previsão futura.

## Atualização automática dos dados
O projeto não utiliza datas fixas nem limita manualmente o período analisado. Em cada execução, a API do IBGE é consultada com o parâmetro `p/all`, garantindo a busca de todos os registros disponíveis até o último período publicado oficialmente.

## Validação realizada
O projeto foi validado com os seguintes comandos:

```bash
python -m py_compile main.py
python -m py_compile dashboard.py
python main.py
```

## Estrutura do projeto
```text
.
|-- dashboard.py
|-- main.py
|-- requirements.txt
|-- README.md
|-- dados/
|   `-- dados_ipca.csv
`-- graficos/
    |-- evolucao_ipca.png
    |-- media_anual.png
    `-- tendencia_ipca.png
```
