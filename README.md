# Desafio: Aumentar as Vendas de uma Loja de Roupas

Projeto de análise de dados desenvolvido em **linguagem R**.

## 📌 Contexto

- A empresa é uma loja de roupas e vende bermudas
- Possui 5 lojas
- Está querendo aumentar as vendas

## ❓ Problema

**O que fazer para aumentar as vendas?**

## 📂 Informações disponíveis

- Base de vendas (`Vendas.xlsx`)

## 🛠️ Tecnologias e bibliotecas

| Pacote | Para que serve |
|--------|----------------|
| [`dplyr`](https://dplyr.tidyverse.org/) | Manipulação de dados |
| [`readxl`](https://readxl.tidyverse.org/) | Leitura de arquivos Excel |
| [`ggplot2`](https://ggplot2.tidyverse.org/) | Criação de gráficos |

Instalação e carregamento:

```r
install.packages("dplyr")
install.packages("readxl")
install.packages("ggplot2")

library(dplyr)
library(readxl)
library(ggplot2)
```

## 📁 Estrutura do projeto

```
projeto_r/
├── dados/
│   └── Vendas.xlsx   # base de vendas
├── script.r         # script da análise
└── README.md
```

## 🔎 Etapas da análise

### 1. Importação e conhecimento dos dados

```r
vendas_df <- read_excel("dados/Vendas.xlsx")

View(vendas_df)   # visualiza a tabela
head(vendas_df)   # primeiras linhas
str(vendas_df)    # estrutura do arquivo
summary(vendas_df) # resumo estatístico
```

### 2. Manipulação dos dados (análise do faturamento)

**Faturamento total**

```r
faturamento <- sum(vendas_df$Valor_Final)
```

**Faturamento por loja**

```r
faturamento_loja <- vendas_df %>%
  group_by(ID_Loja) %>%
  summarise(Faturamento_Total = sum(Valor_Final))
```

**Faturamento por produto em cada loja**

```r
faturamento_produto <- vendas_df %>%
  group_by(ID_Loja, Produto) %>%
  summarise(Faturamento_Total = sum(Valor_Final))
```

### 3. Visualização dos dados

**Faturamento por loja**

```r
ggplot(faturamento_loja, aes(x = ID_Loja, y = Faturamento_Total)) +
  geom_col() +
  theme_minimal() +
  labs(
    title = "Faturamento por Loja",
    subtitle = "Iguatemi Campinas é a responsável pelo maior faturamento da empresa",
    x = NULL,
    y = "Faturamento"
  )
```

**Faturamento por produto**

```r
ggplot(faturamento_produto, aes(x = ID_Loja, y = Faturamento_Total, fill = Produto)) +
  geom_col(position = "dodge") +
  theme_minimal() +
  labs(
    title = "Faturamento por produto",
    subtitle = "Bermuda liso é o produto de maior sucesso",
    x = NULL,
    y = "Faturamento",
    fill = NULL
  )
```

## 📊 Principais conclusões

- **Iguatemi Campinas** é a loja responsável pelo maior faturamento da empresa.
- **Bermuda liso** é o produto de maior sucesso.

## ▶️ Como executar

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/seu-repositorio.git
   ```
2. Abra o projeto no RStudio.
3. Coloque o arquivo `Vendas.xlsx` na pasta `dados/`.
4. Instale os pacotes e execute o script `script.r`.

## 🎓 Créditos

Este projeto foi desenvolvido com base na aula **[Como Sair do ZERO no R em Apenas Uma Aula!](https://www.youtube.com/watch?v=W7UtGnbBiro)** do canal **[Hashtag Programação](https://www.youtube.com/channel/UCafFexaRoRylOKdzGBU6Pgg)**.

## 👤 Autor

Seu nome - [GitHub](https://github.com/seu-usuario)
