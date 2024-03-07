<h1><a href="https://vcforjaz.github.io/Meus-Projetos/"><img align="center" width="40px" src="https://vcforjaz.github.io/Meus-Projetos/favicon.ico"></a><a href="https://vcforjaz.github.io/Meus-Projetos/"><span>Acesse meu site de portfólios hospedado no Git Pages.</span></a></h1>

# Como fazer uma Análise de Dados em Python :
> [!Tip]
> <p>Há dois arquivos upados nessa seção,.</p>
<p> <b>inicial.ipynb</b> que é o arquivo aberto pelo VS Code, onde se escreve o programa e análisa os dados </p>
<p> <b>cancelamentos_50k.csv</b> que é o banco de dados de uma empresa com 50 mil clientes.</p>
<p></p>

# Atenção !
> [!WARNING]
> Quanto maior a quantidade de dados, maior o uso de memória e possibilidades de travamentos. Para utilizar esses arquivos como teste é necessário alterar o nome do banco de dados para o nome desejavel. Fica em import "".

> [!WARNING]
> Bibliotecas necessárias: pandas, numpy, openxl, nbformat, ipkernel, plotly.
> Podem ser instaladas pelo terminal do VS Code digitando: 
`pip install pandas, numpy, openxl, nbformat, ipkernel, plotly`

# Primeiro foi elaborado um passo-a-passo para o desenvolvimento do código:
![image](https://github.com/Vcforjaz/analiseDeDadosPython/assets/148176726/ec813a62-7b63-4faf-8a5b-94c1a17cd2a3)


# Importando a DB:
![image](https://github.com/Vcforjaz/analiseDeDadosPython/assets/148176726/7c76b27d-b753-4170-9a99-f064db4914e8)

`#1 Importar DB
import pandas as pd
tabela = pd.read_csv("cancelamentos.csv")`

`#2 Visualizar DB
tabela = tabela.drop(columns="CustomerID")
display(tabela)`

-Aqui estamos importando a biblioteca pandas e apelidando a mesma como pd, assim podendo invocar sua execução chamando seu apelido.
-Informamos que a tabela é cancelamentos.csv, se for usar os arquivos daqui, é necessário colocar o nome correto que é cancelamentos_50k.csv
-pd.read_csv é a função de pd que é o apelido da biblioteca pandas, _csv é o tipo de arquivo de banco de dados.
-Foi "dropado", excluído a coluna CustomerID, por ser irrelevante.
-Display é a função de Pandas que exibe(tabela) que é o banco de dados(DB).
-Para iniciar a importação + exibição basta clicar no play(Execute Cell).
-No print vemos que meu código encontrou 881666 linhas e 11 colunas no DB.
-

`#3 Corrigir valores vázios ou erros de preenchimento
display(tabela.info())
tabela = tabela.dropna()`

-Aqui dropamos as linhas que possuem algum valor em branco, pois esses valores poderiam atrapalhar nosso aferimento.
-dropna = drop nan, nan = Not a number (vazio).
-

![image](https://github.com/Vcforjaz/analiseDeDadosPython/assets/148176726/73e9ccea-473c-4ce8-98d6-a7defe3ee1b6)

`#4 Análise de cancelamentos
#busca simples de cancelamentos x clientes atuaias:
display(tabela["cancelou"].value_counts())
#busca em porcentagem escrito em decimal:
display(tabela["cancelou"].value_counts(normalize=True))
#busca em porcentagem:
display(tabela["cancelou"].value_counts(normalize=True).map("{:.1%}".format))`

-Aqui temos 3 tipos de exibição, sendo a ultima a mais interessante, porém complexa em termos de código.
-

![image](https://github.com/Vcforjaz/analiseDeDadosPython/assets/148176726/4417f55a-8a12-41d8-a826-f556a51f4656)
![image](https://github.com/Vcforjaz/analiseDeDadosPython/assets/148176726/10111489-ca9b-4fb6-9782-c8bb3b734876)

`#5 Análise de causas de cancelamento
import plotly.express as px`

`#criar o grafico
for coluna in tabela.columns:
    grafico = px.histogram(tabela, x=coluna, color="cancelou")
    #exibir o grafico
    grafico.show()`

-Foi gerado um gráfico para cada coluna existente na DB.
-Foi utilizado um "Laço de repetição, FOR" para que enquanto houver colunas in tabela.columns (Nas colunas de cancelamentos_50k.csv) seja criado e exibido um gráfico especifico para uma a uma até que não haja mais colunas para exibir.
-px é o apelido da biblioteca plotly função express, px.histogram é a função que exibe gráficos, no caso exibindo cada coluna e diferenciando com cor quem cancelou (valor 1, binário) e quem não cancelou (valor 0).
-

![image](https://github.com/Vcforjaz/analiseDeDadosPython/assets/148176726/212b5e4d-5904-4bc0-8bf3-b098eb70ce08)
<h2>Qual o impacto caso haja solução nesses 3 motivos de cancelamentos?</h2>
Sem entrar em detalhes das soluções, caso sejam feitas, haverá uma redução de 81.6% de taxa de cancelamento para 18.4%

`#6 Qual o impacto caso haja solução dos problemas
tabela = tabela[tabela["duracao_contrato"]!="Monthly"]
tabela = tabela[tabela["ligacoes_callcenter"]<=4]
tabela = tabela[tabela["dias_atraso"]<=20]
display(tabela["cancelou"].value_counts(normalize=True).map("{:.1%}".format))`

# Tutorial elaborado por *Victor Forjaz* baseado em materiais do Lira da Hashtag programação.
