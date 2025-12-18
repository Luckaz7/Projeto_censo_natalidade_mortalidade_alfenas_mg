# Projeto censo natalidade e mortalidade da cidade de Alfenas/MG - anos: 2004-2024

Fonte dos dados: https://cidades.ibge.gov.br/brasil/mg/alfenas/pesquisa/20/29767

Este projeto tem como objetivo analisar os dados de natalidade e mortalidade da cidade de Alfenas, Minas Gerais, abrangendo o período de 2004 a 2024. O foco é extrair, padronizar, transformar e visualizar esses dados para identificar tendências e padrões nos registros de nascimentos e óbitos, tanto em registros hospitalares quanto em cartórios de registro civil (CRC).

Processos Realizados:

    Importação de Bibliotecas e Credenciais: 
        -> As bibliotecas necessárias (pandas, matplotlib, google.cloud.storage) foram importadas e as credenciais para acesso ao Google Cloud Storage (GCS) foram configuradas para garantir a segurança e a capacidade de armazenamento dos dados.

    Extração de Dados:
        -> Uma função extracao_dados foi criada para ler um arquivo CSV (Registro civil - Alfenas.csv) do Google Drive, utilizando o separador;
        -> Os dados brutos foram carregados em um DataFrame (df) e as primeiras linhas foram exibidas para inspeção inicial.

    Filtragem e Seleção:
        -> Foram aplicados filtros para selecionar apenas as linhas relevantes para o projeto, especificamente os indicadores de 'Hospital' e 'Lugar do registro' (CRC) para 'pessoas' nas categorias de nascimentos e óbitos;
        -> Dois DataFrames separados foram criados: df_nascidos para dados de natalidade e df_obitos para dados de mortalidade.

    Padronização e Transformação de Dados:
        -> Uma função padronizacao_dados foi desenvolvida para converter os nomes das colunas para minúsculas e resetar o índice dos DataFrames, facilitando a manipulação;
        -> Valores NaN foram preenchidos com 0.
        -> Colunas foram renomeadas de indicador para local e unidade para tipo;
        -> Os rótulos das colunas local foram ajustados para 'registro hospitalar' e 'registro CRC' para maior clareza;
        -> As colunas foram reordenadas para exibir local, tipo e os anos de 2004 a 2024;
        -> Colunas total e media foram calculadas para cada linha, somando e calculando a média dos valores anuais, respectivamente.

    Carga de Dados (Silver Layer):
        -> Os DataFrames df_nascidos e df_obitos, agora limpos e transformados, foram carregados em um bucket do Google Cloud Storage (datalake_taxa_natalidade_mortalidade);
        -> Os dados foram armazenados no formato Parquet, otimizado para análise, em caminhos específicos: dados_natalidade/silver/dados_natalidade_limpo.parquet e dados_mortalidade/silver/dados_mortalidade_limpo.parquet.

    Visualização de Dados:
        -> Foram gerados gráficos de barras para visualizar as taxas de natalidade e mortalidade em diferentes períodos (2004-2010, 2011-2017, 2018-2024 para natalidade; 2008-2012, 2013-2018, 2019-2024 para mortalidade);
        -> Cada gráfico utiliza um colormap (Greens, Blues, Reds para natalidade; Greys para mortalidade) para exibir as barras em tons variados da mesma cor, facilitando a diferenciação visual entre os anos.

Resultados Obtidos:

    Taxa de Natalidade:

        -> 2004-2010: Os gráficos mostram a distribuição dos nascimentos entre 'registro hospitalar' e 'registro CRC'. Observa-se que a maioria dos nascimentos foi registrada via CRC, com o registro hospitalar tendo uma participação menor ou zero em alguns anos iniciais;

        -> 2011-2017: Durante este período, o registro CRC continua predominante e exibem números mais elevados de nascimentos anuais em comparação com o registro hospitalar. Há uma variação ano a ano, mas a tendência geral de CRC ser o principal local de registro se mantém;

        -> 2018-2024: Neste período mais recente, os dados indicam que o registro CRC manteve um volume consistentemente alto, e em alguns anos, como 2022-2024, apresentou picos significativos, superando os 1400 e 1500 nascimentos. O registro hospitalar, por sua vez, mostra uma média mais estável, em torno de 900 nascimentos anuais.

    Taxa de Mortalidade:

        -> 2008-2012: Os gráficos de óbitos mostram que o registro CRC apresenta um número maior de óbitos na maioria dos anos, com o registro hospitalar tendo uma quantidade ligeiramente inferior ou comparável. Os anos de 2010-2012 exibem um aumento notável em ambos os tipos de registro;

        -> 2013-2018: A tendência de mais óbitos registrados via CRC do que hospitalar continua. Há uma certa estabilidade no número de óbitos registrados anualmente, com algumas flutuações;

        -> 2019-2024: O registro CRC continua a ter um volume mais alto de óbitos. Observa-se um aumento nos óbitos em 2020 e 2021 em ambos os tipos de registro, possivelmente refletindo eventos de saúde pública global, seguido por uma leve redução ou estabilização nos anos seguintes, embora permaneçam em patamares elevados.

Conclusão:

O projeto conseguiu processar e visualizar os dados de natalidade e mortalidade para Alfenas/MG no período de 2004 a 2024. A análise dos dados revela que, de forma geral, o número de nascimentos (total de 44.148) supera significativamente o número de óbitos (total de 25.119), indicando um crescimento populacional na cidade durante o período analisado.

É fundamental ressaltar que os registros do CRC podem incluir nascimentos e óbitos de indivíduos que residem em municípios vizinhos, mas que foram registrados em Alfenas. Isso sugere que os dados do CRC podem não refletir exclusivamente a demografia da população residente de Alfenas, enquanto os registros hospitalares tendem a ser mais representativos dos eventos ocorridos dentro da cidade ou com residentes locais. As visualizações coloridas ajudam a distinguir as tendências por ano dentro de cada período, proporcionando uma compreensão clara da dinâmica demográfica observada, com a ressalva da amplitude geográfica dos registros do CRC.
