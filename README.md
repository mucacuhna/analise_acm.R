# analise_acm.R
Script em R para tratamento de dados categóricos e aplicação de ACM (FactoMineR). Estudo de caso sobre o perfil dos estudantes de Ciências Sociais.
# ==============================================================================
# Título: Análise de Correspondência Múltipla (ACM) - Ciências Sociais
# Projeto: Evasão e Permanência (PET Ciências Sociais)
# Autor: Murilo Cunha
# ==============================================================================

# --- 1. Instalação e Carregamento de Pacotes ---

# Verifica se os pacotes existem. Se não, instala e carrega.
pacotes <- c("FactoMineR", "factoextra", "ggplot2", "readr")

novos_pacotes <- pacotes[!(pacotes %in% installed.packages()[,"Package"])]
if(length(novos_pacotes)) install.packages(novos_pacotes)

library(FactoMineR) # Cálculos da ACM
library(factoextra) # Visualização gráfica
library(ggplot2)    # Customização de gráficos
library(readr)      # Leitura otimizada de CSV

# --- 2. Importação e Tratamento dos Dados ---

# Lendo o arquivo recodificado (Certifique-se que o arquivo está na pasta do projeto)
# O argumento 'stringsAsFactors = TRUE' é crucial para ACM, pois trata texto como categoria.
dados <- read.csv("Formulário Recodificado.xlsx - Planilha1.csv", 
                  sep = ",", 
                  stringsAsFactors = TRUE, 
                  encoding = "UTF-8")

# Visualizar as primeiras linhas e nomes das colunas para conferência
head(dados)
colnames(dados)

# LIMPEZA IMPORTANTE:
# A coluna "Carimbo de data/hora" não entra na análise estatística.
# Vamos remover a primeira coluna (assumindo que seja o timestamp) ou selecionar pelo nome.
dados_acm <- dados[, -1] 

# Opcional: Se houverem outras colunas de identificação (como Email), remova-as aqui.
# Exemplo: dados_acm <- subset(dados_acm, select = -c(Email))

# --- 3. Execução da ACM (MCA) ---

# graph = FALSE evita plotar o gráfico padrão imediatamente para customizarmos depois
res.mca <- MCA(dados_acm, graph = FALSE)

# Resumo estatístico rápido (Autovalores e inércia)
summary(res.mca, nbelements = 0, ncp = 2)

# --- 4. Plotagem do Gráfico (Mapa Perceptual) ---

# Criação do objeto gráfico
grafico <- fviz_mca_var(res.mca, 
             repel = TRUE,        # Algoritmo para evitar sobreposição de textos
             geom = c("point", "text"), # Mostra pontos e texto
             col.var = "black",   # Cor das variáveis
             alpha.var = 0.7,     # Transparência
             shape.var = 15) +    # Formato do ponto
  
  # Customização visual (Labels e Títulos)
  labs(title = "Mapa Perceptual - Evasão e Permanência",
       subtitle = "Análise de Correspondência Múltipla (ACM)",
       caption = "Fonte: Pesquisa PET Ciências Sociais | Autor: Murilo Cunha",
       x = "Dimensão 1", 
       y = "Dimensão 2") +
  
  # Tema limpo para publicação acadêmica
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    plot.subtitle = element_text(hjust = 0.5, size = 11),
    axis.title = element_text(face = "bold"),
    panel.grid.major = element_line(color = "gray90"),
    panel.background = element_rect(fill = "white", color = NA)
  )

# Exibe o gráfico
print(grafico)

# --- 5. Exportação ---

# Salva em alta resolução (300 DPI) para uso em artigos ou apresentações
ggsave("mapa_acm_final.png", plot = grafico, width = 10, height = 7, dpi = 300)

message("Análise concluída e gráfico salvo como 'mapa_acm_final.png'.")
