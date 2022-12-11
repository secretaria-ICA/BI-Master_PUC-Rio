<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->
# Classificação de Imagens de Ultrassonografia Mamária por meio de Aprendizagem Profunda

#### Aluno: [Geilson Gomes Araujo](https://github.com/Geilson-Araujo)
#### Orientadora: [Manoela Kohler](https://github.com/manoelakohler).


---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bimaster/) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código](https://github.com/Geilson-Araujo/BI-Master_PUC-Rio). <!-- caso não aplicável, remover esta linha -->

---

### Resumo

<!-- trocar o texto abaixo pelo resumo do trabalho, em português -->

A proposta deste trabalho é classificar por meio de aprendizagem profunda imagens de ultrassonografia mamária, a fim de corroborar que tais técnicas podem ser aliadas à Saúde, especificamente no diagnóstico de câncer de mama.
Utilizou-se, assim, 3 (três) modelos de redes neurais convolucionais (CNNs): Resnet50, VGG16, Densenet121 e 3 (três) de Visual Transformers (ViTs): ViT-Base-Patch32, ViT-Small-Patch32, ViT-Large-Patch32.

O modelo CNN com melhor desempenho alcançou um F1-score (macro) de 0.90 sobre os dados de teste, enquanto o modelo ViT, 0.81, demonstrando, portanto, de forma satisfatória o objetivo principal deste trabalho.


### 1. Introdução

O câncer de mama, segundo dados do Instituto Nacional de Câncer ([INCA](www.inca.gob.br/mama)), é o de maior incidência no Brasil - exceto pelos tumores de pele não melanoma - e a principal causa de morte por câncer na população feminina - com exceção da região Norte, onde o câncer de colo do útero é a causa principal.

Assim, desde meados nos anos 80, políticas públicas vêm sendo desenvolvidas pelo Estado a fim de estabelecer ações de controle da doença no país. Dentre essas ações há o __rastreamento__ por meio de exames de imagens.

Quanto mais cedo o câncer de mama for detectado, maior a possibilidade de tratamentos menos agressivos, mais efetivos e menor morbidade associada. [referência: 

O aprendizado de máquina profundo tem se mostrado um aliado à sociedade no auxílio de diagnósticos por imagens médicas pelos profissionais de saúde, colaborando, por conseguinte, para que vidas sejam salvas.

Predominantemente, utilizam-se redes neurais convolucionais (CNNs) para o processo de análise de imagens digitais. Contudo, outros modelos podem também ser promissores. 
Esse trabalho procura avaliar se os recentes modelos de visão computacional baseados em transformers (Vision Transformers - [ViT](https://arxiv.org/abs/2010.11929)) são também promissores em relação aos modelos CNNs já estabelecidos.

utiliza-se esse sentido, o aprendizado de máquina profundo pode ser um grande aliado da sociedade, contribuindo para que o diagnóstico realizado pelos profissionais de saúde sejam mais eficientes e, por conseguinte, colaborando também para que vidas sejam salvas.


### 2. Modelagem

Neste trabalho foram utilizadas duas bases de dados públicas:

* A Breast Ultrasound Images Dataset ([BUSI](https://www.kaggle.com/datasets/aryashah2k/breast-ultrasound-images-dataset)), que possui 780 imagens de ultrassonografias de mama, sendo  133 de casos normais, 437 de tumores benígnos e 210 malignos;
* E a Breast Ultrasound Image ([BUI](https://data.mendeley.com/datasets/wmy84gzngw/1)), contendo 250 imagens de câncer de mama, sendo 100 imagens referentes a tumores benignos e 150 malignos, no formato BMP.

O pré-processamento realizado consistiu em converter todas as imagens para 224x224 pixels, cada qual com três dimensões correspondentes ao RGB. Além disso, para normalização, foram utilizados para média e desvio-padrão os mesmo valores utilizados para o modelo originalmente treinado.

Os dados foram separados em dois subconjuntos, sendo 80% para treino e 20% para teste, de forma estratificada, ou seja, procurou-se manter as mesmas proporções das categorias das  imagens em ambos os grupos.

Para os experimentos foram utilizados os seguintes modelos - 3 (três) modelos de redes neurais convolucionais (CNNs) e 3 (três) modelos vision transformers (ViTs):

* Resnet50;
* VGG16;
* Densenet121;
* ViT Base Patch32;
* ViT Small Patch32;
* ViT Large Patch32.

Na etapa de treinamento e validação foi realizada a validação-cruzada com 5 (cinco) folds. Utilizou-se também a cross entropy loss como função de custo, a F1-Score (macro) como métrica principal, o Adam como otimizador e a taxa de aprendizado do modelo era ajustada quando não havia melhora por 10 épocas.

Foram conduzidos três tipos de experimentos por modelo. No primeiro caso não se utilizou _transfer learning_, somente a estrutura do modelo foi utilizada para o treinamento. Já no segundo, utilizou-se o método _fine tuning_ e por último, o _feature extraction_.


### 3. Resultados

Abaixo seguem as tabelas dos resultados para os experimentos realizados com as redes convolucionais e ViTs.

Obs.: Para aqueles modelos que demonstraram potencial de melhoria próximo a 50 épocas, utilizou-se 100 épocas.

Foram obtidos os seguintes resultados para os modelos CNNs:

![results_cnn](assets/results_cnn.png)

Foram obtidos os seguintes resultados para os modelos ViTs:

![results_vit](assets/results_vit.png)

Conforme as tabelas acima, no caso das redes convolucionais, o modelo que obteve melhor desempenho foi o fine tuning da Densenet121, com F1-score (macro) de 0.90 sobre a base de teste. E no caso dos modelos ViTs, o de melhor desempenho foi o feature extraction do ViT Base 32, por meio do qual se obteve um F1-score (macro) de 0.81.

Em complemento às informações acima, seguem a matriz de confusão e o o _classification report_ do melhor modelo CNN e ViT, respectivamente:

<table><tr>
<td> <img src="assets/confusion_matrix_cnn.png" alt="Drawing" style="width: 500px;"/> </td>
<td> <img src="assets/classification_report_cnn.png" alt="Drawing" style="width: 500px;"/> </td>
</tr></table>

<table><tr>
<td> <img src="assets/confusion_matrix_vit.png" alt="Drawing" style="width: 500px;"/> </td>
<td> <img src="assets/classification_report_vit.png" alt="Drawing" style="width: 500px;"/> </td>
</tr></table>


### 4. Conclusões

Para o conjunto de dados, modelos e parâmetros utilizados, todas as redes neurais convolucionais superaram em algum dos experimentos o melhor resultado obtido pelos modelos que utilizam vision transformers.

Contudo, há ainda outras técnicas que podem ser agregadas ao experimento: data augmentation, balanceamento de classes, outras funções de custo, outras métricas, test-time augmentation, modelos híbridos.

Entretanto, o resultado mais relevante foi o modelo com melhor resultado ter conseguido prever todos os casos de tumores malignos corretamente na base de testes, sem falsos negativos, havendo margem para melhorias.

Dessa forma, o resultado obtido corrobora o pressuposto de os modelos de aprendizagem profunda serem potencialmente grandes aliados na área da saúde. E quanto mais avanços nesse campo, mais e melhores modelos disponíveis, mais vidas poderão ser salvas.


---

Matrícula: 192.110.140

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
