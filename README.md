# Análise e Avaliação Automática da Competência 4 de Redações do ENEM

Este projeto realiza uma investigação sobre os elementos de coesão textual em redações e desenvolve múltiplos modelos de Machine Learning para prever a nota da Competência 4, que avalia o conhecimento dos mecanismos linguísticos necessários para a construção da argumentação.

## ⚠ Visualização do Notebook

O GitHub apresentou problemas para renderizar o notebook com as saídas devido aos widgets interativos. Para uma visualização completa, com todos os gráficos e saídas:

1.  Acesse o site **[nbviewer.org](https://nbviewer.org/)**.
2.  Cole o seguinte link do notebook na caixa de pesquisa e pressione Enter:
    ```
    https://github.com/leope22/corretor-automatico-competencia-4/blob/92e3057760362b8f0fe7b4b70906df526d86e3e4/Compet%C3%AAncia_4.ipynb
    ```

## 📜 Contexto do Projeto

A Competência 4 do Exame Nacional do Ensino Médio (ENEM) exige o uso articulado de um repertório coeso de conectivos e referências para construir um texto fluido e bem argumentado. Este projeto busca entender quais características textuais estão mais correlacionadas com notas altas e, a partir disso, construir um sistema de avaliação automática.

## 🔬 Análise Exploratória de Dados

Antes da modelagem, foi realizada uma extensa análise de dados para extrair features e identificar padrões. As principais frentes de investigação foram:

  * **Uso de Conectivos:** Análise da quantidade, diversidade e categorias semânticas dos conectivos utilizados.
  * **Adequação dos Conectivos:** Utilização de um modelo BERT (Masked Language Model) para verificar se os conectivos foram empregados em contextos semanticamente apropriados.
  * **Riqueza Lexical e Repetição:** Medição da repetição de palavras de conteúdo em "janelas deslizantes" para avaliar a fluidez do vocabulário.
  * **Estrutura Paragrafal:** Análise do número, tamanho médio e equilíbrio dos parágrafos.

## 🤖 Modelos Desenvolvidos

Foram implementadas e avaliadas três abordagens progressivamente mais complexas:

### 1\. Avaliador Baseado em Regras

Um sistema de pontuação heurístico que atribui notas com base em métricas extraídas da análise (diversidade de conectivos, tamanho dos parágrafos, taxa de repetição, etc.). Serviu como um baseline para o projeto.

### 2\. Modelo LightGBM com Feature Engineering

Um modelo de Gradient Boosting (LightGBM) treinado com um conjunto robusto de features extraídas de forma segmentada (introdução, D1, D2, conclusão), incluindo métricas de coesão, vocabulário e similaridade semântica entre parágrafos. O modelo demonstrou ser superior ao sistema de regras, especialmente na identificação de redações de nota 200.

### 3\. Modelo BERT com Ponderação de Classes (Melhor Performance)

A abordagem final utilizou o fine-tuning de um modelo Transformer pré-treinado em português, o `neuralmind/bert-base-portuguese-cased`. Diferente dos anteriores, o BERT processa o texto bruto, aprendendo a interpretar o contexto e as nuances semânticas. Foi utilizada uma técnica de ponderação de classes para mitigar o desbalanceamento do dataset.

  * **Resultado:**
      * **Precisão Final: 53.8%**, um avanço considerável em relação às abordagens anteriores, demonstra uma boa capacidade de acerto.
      * **Recall para Nota 200: 82%**, demonstrando a principal força do modelo: identificar com alta confiança as redações de máxima performance.
      * **Desafio:** O modelo ainda apresenta dificuldade em classificar as notas minoritárias (0 e 40), o que é esperado dada a baixa representatividade delas no dataset.

## 🛠️ Tecnologias Utilizadas

  * **Linguagem:** Python
  * **Análise de Dados:** Pandas, NumPy, Matplotlib, Seaborn
  * **Processamento de Linguagem Natural (NLP):** spaCy, Transformers (Hugging Face)
  * **Machine Learning:** Scikit-learn, LightGBM, Imbalanced-learn
  * **Deep Learning:** PyTorch
