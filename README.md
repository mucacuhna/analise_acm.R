# 📊 Análise de Evasão e Permanência: Aplicação de ACM em R

> **Projeto de Pesquisa - PET Ciências Sociais**
> Autor: Murilo Cunha

Este repositório contém o script de tratamento de dados e aplicação da **Análise de Correspondência Múltipla (ACM)** para investigar perfis de estudantes e fatores associados à evasão e permanência no curso de Ciências Sociais.

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

### 📂 Dicionário de Variáveis (Legenda do Gráfico)
Como os dados foram recodificados para a análise estatística, utilize a tabela abaixo para interpretar as siglas apresentadas no gráfico:

| Variável (Código) | Significado | Categorias Principais |
| :--- | :--- | :--- |
| **GEN** | Gênero | **M** (Masculino), **F** (Feminino), **NB** (Não-binário) |
| **ETN** | Etnia (Autodeclaração) | **B** (Branco), **P** (Pardo), **PT** (Preto) |
| **BOL** | Possui Bolsa? | **S** (Sim), **N** (Não) |
| **TRA** | Trabalha? | **S** (Sim), **N** (Não) |
| **ANO** | Ano de Ingresso | Ex: **2020**, **2021**, **2022** |
*(Adicione outras categorias aqui se necessário)*

---

### 🚀 Como executar este projeto
1.  Certifique-se de ter o **R** e o **RStudio** instalados.
2.  Clone este repositório ou baixe os arquivos.
3.  Abra o arquivo `analise_acm.R`.
4.  Certifique-se de que o arquivo de dados `Formulário Recodificado.xlsx - Planilha1.csv` está na mesma pasta do script.
5.  Execute o script linha a linha.

### 📊 Resultado Esperado
O script irá gerar e salvar automaticamente o arquivo `mapa_acm_final.png`, que apresenta a dispersão das variáveis nas duas primeiras dimensões da ACM.

---
📫 **Contato:** [Insira seu LinkedIn aqui]
