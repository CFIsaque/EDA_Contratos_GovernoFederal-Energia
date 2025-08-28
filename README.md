# EDA_Contratos_GovernoFederal-Energia
Análise exploratória de dados dos valores dos contratos de distribuição de energia do Governo Federal.

## Problema:
Quanto o governo gastou em contratos relacionado a serviços de fornecimento e distribuição de energia desde 2023. O Governo Federal tem uma API aberta com os dados da compras públicas (fonte: https://dados.gov.br/dados/conjuntos-dados/compras-publicas-do-governo-federal). Como podem ver nas imagens abaixo, nessa API os valores dos serviços/contratos e os tipos de serviços estão em endpoints diferentes. Então para fazer a requisição, além das informações de valores e tipos de serviços, também precisamos encontrar um id ou chave que faça a união dos dois endpoints. 

<img width="1471" height="482" alt="image" src="https://github.com/user-attachments/assets/88b1357e-4f7b-4801-896b-8133a823d5b1" /><img width="1471" height="276" alt="image" src="https://github.com/user-attachments/assets/f388e179-9924-4932-bdeb-34ecd06cbe4a" />

Durante a investigação, foi identificado que os contratos do governo apresentam elevada variabilidade quando observados em recortes temporais, como meses e anos. Essa oscilação pode ser explicada, em grande parte, pelo início, término ou renovação de contratos, que não seguem um padrão linear. Outro fator relevante refere-se a investimentos pontuais decorrentes de determinadas medidas públicas (por exemplo, políticas de isenção), que resultam em valores atípicos quando comparados aos contratos de caráter rotineiro.

Diante desse cenário, o objetivo da análise, além de mensurar o montante gasto pelo Governo Federal, é avaliar a concentração dos contratos com base na Princípio de Pareto. Especificamente, busca-se identificar quantos contratos foram responsáveis por atingir 80% do valor total nos anos de 2023, 2024 e 2025.

## Solução:

Para apresentar a solução, é necessário, primeiramente, compreender o conceito da regra de Pareto e sua relação com a análise.

O princípio de Pareto (também conhecida como princípio 80/20), popularizado por Richard Koch (1997),  Desde então, esse princípio tem sido amplamente aplicado em diferentes áreas, sugerindo que, em muitos fenômenos, aproximadamente 80% dos efeitos são explicados por 20% das causas.

No contexto da nossa investigação, esse conceito é utilizado para avaliar a concentração dos contratos do Governo Federal. Em outras palavras, buscamos compreender se uma parcela relativamente pequena de contratos concentra uma proporção significativa do montante total gasto. Essa abordagem permite identificar padrões de concentração e medir a relevância de contratos específicos dentro do orçamento. 

Para aplicar pareto, fizemos algumas etapas utilizando python, mais precisamente pandas:


  🔹Integração de dados: Leitura da documentação da API, compreensão das nomenclaturas e regras governamentais, seguida da conexão e união de dados de dois endpoints (nomes dos serviços e valores dos contratos)
  
  🔹Tratamento de dados: Limpeza e padronização (remoção de contratos duplicados, normalização de palavras com acentuação diferente, ex: "elétrica" e "eletrica")
  
  🔹Análise exploratória: Inicialmente, analisei a média de valores mensais (comparando 2023 vs 2024). Como foi falado anteriormente, foi identificado alta variabilidade na distribuição (meses com mais contratos, meses com contratos de valores elevados etc), como pode ser visto na imagem abaixo 

<img width="566" height="454" alt="image" src="https://github.com/user-attachments/assets/1239f3f7-2293-4160-8603-3953998d91bb" />

## Aplicação do princípio de Pareto

Para cada ano, os contratos foram agrupados e somados pelo valor global, sendo posteriormente ordenados em ordem decrescente. Em seguida, foi calculada a participação percentual de cada contrato no total e a soma acumulada desses percentuais, resultando na curva de Pareto. 

O ponto de corte de 80% foi identificado ao localizar o menor número de contratos cuja soma acumulada atingisse esse valor. Dessa forma, é possível determinar quantos contratos foram responsáveis por concentrar 80% dos gastos em cada ano e qual a proporção desse número em relação ao total de contratos analisados. Veja imagem abaixo:

<img width="1590" height="1790" alt="image" src="https://github.com/user-attachments/assets/801c76f3-4b37-4e6c-a38a-22d9a551e56e" />


## Referências:
OROUEDINADL, Ehsan. Pareto Principle (80/20 Rule) in Data Analysis. The Data School, 10 nov. 2024. Disponível em: https://www.thedataschool.com.au/ehsan-forouedinadl/pareto-principle-80-20-rule-in-data-analysis/

