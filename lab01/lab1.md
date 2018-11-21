Laboratório 1 - Análise de Gastos de Deputados
================
Juan Barros
29 de agosto de 2018

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 3.5.1

    ## -- Attaching packages ----------------------------------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.4
    ## v tibble  1.4.2     v dplyr   0.7.4
    ## v tidyr   0.8.1     v stringr 1.3.0
    ## v readr   1.1.1     v forcats 0.3.0

    ## Warning: package 'ggplot2' was built under R version 3.5.1

    ## Warning: package 'readr' was built under R version 3.5.1

    ## Warning: package 'forcats' was built under R version 3.5.1

    ## -- Conflicts -------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(knitr)
dados <- read_csv("dadosCEAP.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   nomeParlamentar = col_character(),
    ##   idCadastro = col_integer(),
    ##   sgUF = col_character(),
    ##   sgPartido = col_character(),
    ##   tipoDespesa = col_character(),
    ##   especDespesa = col_character(),
    ##   fornecedor = col_character(),
    ##   CNPJCPF = col_character(),
    ##   tipoDocumento = col_integer(),
    ##   dataEmissao = col_datetime(format = ""),
    ##   valorDocumento = col_double(),
    ##   valorGlosa = col_integer(),
    ##   valorLíquido = col_double()
    ## )

Quais são os deputados que gastaram mais dinheiro da CEAP? Quais são os mais econômicos
---------------------------------------------------------------------------------------

``` r
group <- 
  dados %>%
  group_by(nomeParlamentar) %>%
  summarise(gasto = sum(valorLíquido))
first <- 
  group %>%
  arrange(desc(gasto)) %>%
  slice(1:10)
last <-
  group %>%
  arrange(gasto) %>%
  slice(1:10)
  
knitr::kable(last,caption="Economicos")
```

| nomeParlamentar   |     gasto|
|:------------------|---------:|
| JOÃO CALDAS       |  -1791.57|
| ELISEU PADILHA    |  -1487.52|
| RUI COSTA         |   -376.99|
| ANTÔNIO ANDRADE   |   -167.37|
| CAMILO COLA       |      0.62|
| MARCIO MONTEIRO   |     14.18|
| MARCELO ALMEIDA   |     26.16|
| RENAN FILHO       |     35.51|
| HENRIQUE OLIVEIRA |     40.43|
| CEZAR SILVESTRI   |     67.54|

Quais os estados cujos deputados gastam mais no exterior? Quais os estados cujos deputados gastam menos no exterior?
--------------------------------------------------------------------------------------------------------------------

Quais os partidos cujos parlamentares mais usam CEAP no estado da Paraíba? Quais são os que menos usam? Mesmas perguntas considerando valores em R$. (7,5 pts)

Quais os deputados que mais ultrapassam o limite de CEAP do seu estado? Os dados com os limites de CEAP por estado estão disponíveis neste link. (7,5 pts)
----------------------------------------------------------------------------------------------------------------------------------------------------------

Quais estados cujos parlamentares gastam mais com passagens aéreas? (7,5 pts)
-----------------------------------------------------------------------------

Escolha três partidos e responda: Quais são os tipos de despesa mais utilizados no uso da CEAP pelos deputados desses partidos? Mesma pergunta considerando valores em R$.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
