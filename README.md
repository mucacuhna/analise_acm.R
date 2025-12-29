# 📊 Aplicação da ACM dentro do R: Usando a estatística como meio de estudo acadêmico

> **Projeto de Pesquisa: Evasão e Permanência dentro do curso de Ciências Sociais na FCLAR - PET Ciências Sociais**
> Autor do código: Murilo Cunha

Este repositório contém o script de tratamento de dados e aplicação da **Análise de Correspondência Múltipla (ACM)** para investigar perfis de estudantes e fatores associados à evasão e permanência no curso de Ciências Sociais. Esse script pode ser usado como modelo para realização de outras ACMs em outros estudos estatísticos que possuem o objetivo de, além de cruzar informações, observar, estatisticamente
o que une e separa os agentes sociais dentro daquele universo observado.

### 🎯 Objetivo
Identificar padrões visuais (clusters) que relacionam variáveis socioeconômicas e acadêmicas, transformando dados qualitativos em um mapa perceptual para auxiliar na compreensão do fluxo estudantil.

---

### 🛠️ Tecnologias Utilizadas
* **Linguagem:** R
* **Pacotes Principais:**
    * `FactoMineR` (Cálculo da ACM)
    * `factoextra` (Visualização e extração de resultados)
    * `ggplot2` (Customização gráfica avançada)

---

### 📂 Estrutura dos Dados
Para otimizar a visualização gráfica (Clusterização), as respostas foram recodificadas utilizando siglas.
É de suma importância que seja feito um dicionário de códigos para que, após a recodificação das respostas,
haja uma maneira eficiente de identificar o que cada código representa dentro daqueles quatro quadrantes.
* **Padrão:** As categorias seguem a lógica `Variável` + `Resposta`.
* **Exemplos:**
    * `G2` = Homem Cisgênero
    * `I3` = 23-25 anos
    * `S3` = Bissexual

---

### 🚀 Como executar este projeto
1.  Certifique-se de ter o **R** e o **RStudio** instalados.
2.  Clone este repositório e, caso queira testar antes, baixe os arquivos e rode o programa.
3.  Abra o arquivo `analise_acm.R`.
4.  Certifique-se de que o arquivo de dados `Formulário Recodificado.xlsx - Planilha1.csv` está na mesma pasta do script.
5.  Execute o script linha a linha.

### 📊 Resultado Esperado
O script irá gerar e salvar automaticamente o arquivo `mapa_acm_final.png`, que apresenta a dispersão das variáveis nas duas primeiras dimensões da ACM.

---

# ===============================================================
# Título: Análise de Correspondência Múltipla (ACM) - Ciências Sociais
# Projeto: Evasão e Permanência (PET Ciências Sociais)
# Autor: Murilo Cunha
# =============================================================

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

---
📫 **Contato:** [https://www.linkedin.com/in/murilo-cunha-71aa72299/]
