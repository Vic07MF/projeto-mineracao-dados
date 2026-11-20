# Faltas escolares, segurança e bem-estar na PeNSE 2024

Projeto brasileiro de Mineração de Dados para investigar padrões de absenteísmo autorrelatado. O objetivo é distinguir perfis de faltas e identificar quais respostas de contexto aparecem associadas a cada motivo de ausência. A evasão é a motivação educacional; o questionário não acompanha desligamentos.

## Abrir no VS Code

1. Extraia todo o ZIP e abra a pasta que contém este README. Use Python 3.12 e as extensões Python e Jupyter.
2. Crie um ambiente com **Python: Create Environment** e selecione **Venv**. Abra o notebook e escolha esse ambiente em **Selecionar Kernel**.
3. Na primeira execução, se necessário, crie uma célula temporária e rode o comando abaixo. Se o notebook tiver aberto dentro de notebooks/, use ../requirements.txt. Reinicie o kernel após instalar.

~~~python
%pip install -r requirements.txt
~~~

4. Abra **notebooks/analise_pense2024.ipynb** e clique em **Executar Tudo**. Os caminhos são relativos. Havendo internet, a segunda etapa baixa os arquivos oficiais que faltam. Para usar seu download prévio, coloque o CSV com o nome PENSE2024_MICRODADOS.csv e o dicionário como dicionario.xlsx em dados/original/. Também é possível colocar Dados.zip e Documentacao.zip nessa pasta ou ajustar as variáveis csv e xlsx na primeira célula. O notebook espera o CSV original com vírgula e as colunas de controle do IBGE. Uma base reduzida de sete variáveis não contém as informações necessárias.
5. Em Colab, extraia o projeto em uma pasta da sessão, abra o notebook e use %cd para entrar na pasta que contém este README antes da primeira etapa. Arquivos processados podem ser baixados após a execução.

## Método e resultados

Verificação da chave composta, auditoria dos motivos de ausência por quesito e leitura seletiva de colunas. Cinco indicadores ordinais escalados para K-Means. Comparam-se K de 2 a 8 por Silhouette e inércia (K = 1 como referência para a inércia). O Apriori de dois níveis é implementado com Pandas: contagem dos itens individuais, poda por suporte, formação e contagem dos pares candidatos. O conjunto de regras tem um único item contextual no antecedente e uma falta no consequente.

O arquivo tem 153.870 registros e 430 colunas. O domínio tem 148.736 registros. Em 146.099 casos completos, o maior valor de Silhouette foi 0,336 para cinco grupos. Em 145.915 transações, sete regras passaram pelos limiares principais. A associação de maior lift foi tristeza frequente com falta por insegurança na escola (1,78). Os números são descritivos da amostra sem ponderação. Causalidade e evasão individual não podem ser inferidas.

## Arquivos

- notebooks/analise_pense2024.ipynb — análise executável em células sequenciais.
- dados/original/ — entradas oficiais locais, obtidas do IBGE.
- dados/processados/ — bases individuais geradas localmente na execução. O índice indica a posição original do registro (inicia em zero).
- resultados/tabelas/ — frequências, categorias e métricas em CSV.
- resultados/graficos/ — cinco figuras em PNG.
- relatorio.pdf e relatorio.md — trabalho escrito e versão editável.
- apresentacao.pptx e roteiro_15min.md — slides com notas e divisão sugerida em dupla.
- requirements.txt — bibliotecas da execução.


## Bibliografia 

Fonte: [microdados e documentação oficial do IBGE](https://ftp.ibge.gov.br/pense/2024/microdados/).
