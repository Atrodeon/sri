# sri
Sistema de recomendação por imagens
# 📸 Sistema de Recomendação Visual por Similaridade de Imagem

## 🎯 Objetivo do Projeto

O objetivo deste projeto é desenvolver um Sistema de Recomendação que sugira produtos relacionados, não com base em metadados textuais (preço, marca, modelo), mas sim na **similaridade de sua aparência física** (formato, cor, textura). O sistema utiliza técnicas de Deep Learning para extrair características visuais das imagens e um algoritmo de vizinhos mais próximos para encontrar os itens mais parecidos.

## ⚙️ Arquitetura e Atividades

O desenvolvimento do sistema foi dividido nas seguintes etapas principais:

### 1. Configuração do Ambiente e Ferramentas
* **Ambiente:** Google Colaboratory.
* **Bibliotecas Principais:** TensorFlow/Keras, scikit-learn (sklearn), OpenCV e Pillow.
* **Setup:** Montagem do Google Drive para acesso ao dataset de imagens.

### 2. Extração de Características (Feature Extraction)
* **Modelo Base (Backbone):** Foi utilizada a rede neural convolucional **ResNet50**, pré-treinada no dataset ImageNet.
* **Técnica:** O modelo ResNet50 foi carregado sem a camada de classificação (`include_top=False`), usando a camada de *Global Average Pooling* (`pooling='avg'`) para gerar um vetor de características compactado para cada imagem.
* **Atividade:** Implementação da função `extract_features` para pré-processar as imagens (redimensionamento para 224x224 e normalização) e obter o vetor de características de alta dimensão.

### 3. Modelagem de Similaridade
* **Algoritmo:** **$k$-Nearest Neighbors (KNN)**.
* **Métrica:** A **Distância Cosseno** foi escolhida como métrica de similaridade. Esta métrica mede o ângulo entre os vetores de características, sendo ideal para determinar a similaridade vetorial (sem considerar magnitude), garantindo que as imagens com padrões visuais semelhantes fiquem próximas no espaço latente.
* **Atividade:** O modelo KNN foi treinado com os vetores de características extraídos de todo o dataset de produtos (`all_features_np`).

### 4. Geração de Recomendações
* **Processo:** Uma imagem de consulta (`query`) tem suas características extraídas e é comparada ao conjunto de dados usando o modelo KNN.
* **Resultado:** O sistema retorna os **$k$** vizinhos mais próximos (os produtos visualmente mais similares), juntamente com o valor da Distância Cosseno, que indica o grau de similaridade.
* **Atividade:** Implementação da função `recommend_similar_products` e teste final com a imagem de consulta (`rel1.jpg`).

### 5. Visualização e Conclusão
* **Visualização:** Utilização da biblioteca `matplotlib` para carregar e exibir a imagem de consulta e os produtos recomendados lado a lado no notebook.
* **Resultado Final:** O sistema conseguiu identificar produtos visualmente correlatos, validando o uso de Deep Learning para recomendação baseada em conteúdo visual.

## 🚀 Como Usar

1.  **Clone o Repositório:** Faça o download deste projeto.
2.  **Abra no Colab:** Abra o arquivo `.ipynb` no Google Colab.
3.  **Configure o Caminho:** Altere a variável `IMGS_DIR` para o caminho onde suas imagens de produto estão armazenadas no Google Drive (ex: `/content/drive/MyDrive/images`).
4.  **Execute as Células:** Execute as células em ordem, garantindo que o `QUERY_IMAGE_PATH` aponte para uma imagem válida para testar as recomendações.
