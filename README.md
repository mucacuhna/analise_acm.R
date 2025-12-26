# 📊 Análise de um Projeto Acadêmico: Aplicação de ACM em R

> **Projeto de Pesquisa: Evasão e Permanência dentro do curso de Ciências Sociais na FCLAR - PET Ciências Sociais**
> Autor: Murilo Cunha

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
É de suma importância que seja feito um dicionário de códigos para, após a recodificação das respostas,
haja uma maneira eficiente de identificar o que cada código representa.
* **Padrão:** As categorias seguem a lógica `Variável` + `Resposta`.
* **Exemplos:**
    * `G2` = Homem Cisgênero
    * `I3` = 23-25 anos
    * `S3` = Bissexual

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
📫 **Contato:** [https://www.linkedin.com/in/murilo-cunha-71aa72299/]
