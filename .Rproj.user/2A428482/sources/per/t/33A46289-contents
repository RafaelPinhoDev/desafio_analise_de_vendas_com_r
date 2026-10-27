
# Instalação e Carregamento dos Pacotes -----------------------------------
install.packages("dplyr") # Manipulação de dados 
install.packages("readxl") # Lê arquivos em excel
install.packages("ggplot2") # Cria gráficos

# Carregamento dos pacotes
library(dplyr)
library(readxl)
library(ggplot2)

# Importação e Conhecimento dos Dados  ------------------------------------
vendas_df <- read_excel("E:/Pessoal/projetos/projeto_r/dados/Vendas.xlsx")

# Vê as tabelas disponíveis
View(vendas_df)

# Recorta uma visualização das primeiras linhas do arquivo
head(vendas_df)

# Verifica a estrutura do arquivo
str(vendas_df)

# Faz um resumo estatístico dos dados
summary(vendas_df)

# Manipulação dos Dados ---------------------------------------------------

#Calcular o faturamento 
faturamento <- sum(vendas_df$Valor_Final)
faturamento

#Calcular faturamento por loja sem pipe
faturamento_loja <- group_by(vendas_df, ID_Loja)
faturamento_loja <- summarise(faturamento_loja, Faturamento_Total = sum(Valor_Final))

#Calcular faturamento por loja com pipe
faturamento_loja2 <-  vendas_df %>% 
  group_by(ID_Loja) %>%
  summarise(Faturamento_Total = sum(Valor_Final))
 

#calcular Faturamento por produto
faturamento_produto <- vendas_df %>%
  group_by(ID_Loja, Produto) %>%
  summarise(Faturamento_Total = sum(Valor_Final))

# Visualização dos Dados --------------------------------------------------

# Primeira camada do gráfico, definindo o eixo x e y
ggplot(data = faturamento_loja, mapping = aes(x = ID_Loja, y = Faturamento_Total)) + 
  geom_col() +
  theme_minimal() +
  labs(
    title = "Faturamento por Loja",
    subtitle = "Iguatemi Campinas é a responsável pelo maior faturamento da empresa",
    x = NULL,
    y = "Faturamento"
    )
  

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

