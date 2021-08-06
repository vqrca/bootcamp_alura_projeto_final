[![Badge](https://img.shields.io/badge/Author-Valquíria_Alencar-%237159c1?style=flat-square&logo=ghost)](https://github.com/vqrca/) [![Gmail Badge](https://img.shields.io/badge/-valquiria.c.alencar@gmail.com-6633cc?style=flat-square&logo=Gmail&logoColor=white&link=mailto:valquiria.c.alencar@gmail.com)](mailto:valquiria.c.alencar@gmail.com)[![Linkedin Badge](https://img.shields.io/badge/-Valquíria_Alencar-6633cc?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/valquiria-alencar/)](https://www.linkedin.com/in/valquiria-alencar/) [![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg?style=flat-square)](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/LICENSE)

<p align="center"> 
 <img src="https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Images/cover_projeto_final.png" />
</p>

# **Sumário:**
<!--ts-->
   * [Resumo](#resumo)
   * [Introdução](#intro)
   * [Dados](#dados)
   * [Hipóteses](#hip)
   * [Conclusões](#conclusoes)
   * [Considerações finais](#final)
   * [Referências](#ref)
   * [Documentação](#doc)
   * [Agradecimentos](#agra)
   * [Contato](#contact)
   <!--te-->

<a name="resumo"></a>
# Resumo 🏃‍♀️

- Com sua rápida disseminação, a doença **COVID-19** criou uma forte demanda por hospitais e leitos nas UTIs (Unidades de Terapia Intensiva). Esta maior necessidade de recursos hospitalares levou ao **colapso dos sistemas de saúde** em todo o mundo, o que pode ter contribuído para as maiores taxas de mortalidade relatadas. 

- Pensando nisso, o **Hospital Sírio Libânes disponibilizou um *dataset*** contendo **informações sobre vários pacientes**, com os seguintes objetivos: **Prever admissão na UTI de casos confirmados de COVID-19 e prever a NÃO admissão à UTI de casos COVID-19 confirmados**.  

- **Dessa forma, o presente projeto dedicou-se a criar um modelo de Machine learning  para prever quais pacientes precisarão ser admitidos na unidade de terapia intensiva e assim, definir qual a necessidade de leitos de UTI do hospital, a partir dos dados clínicos individuais disponíveis**. 

- Os dados deste dataset estão organizados em janelas tempo, após a admissão dos pacientes no hospital: 0-2 horas, 2-4 horas, 4-6 horas, 6-12 horas e  acima de 12 horas após a admissão. Além disso, o dataset conta com informações demográficas, doenças pré-existentes, resultados de exames de sangue e sinais vitais. Finalmente, o dataset contém a coluna `ICU`, que é a variável de interesse e indica se o paciente foi ou não para UTI. 

- Então, **os dados foram pré-processados e somente a janela de 0-2 horas foi utilizada**, já que quanto mais cedo a previsão for feita é melhor, tornando-se clinicamente mais relevante. Além disso, as features com alta correlação foram retiradas e o conjunto de dados foi dividido em treinamento e teste. 

- A biblioteca ***LazyPredict* foi utilizada para identificar quais seriam os melhores classificadores possíveis para esses dados**. Em seguida, os **classificadores que apresentaram melhor desempenho** foram estudados individualmente, passando por **análises de métricas e *Cross-Validation***. 

- Dois classificadores se mostraram mais adequados: *XGBClassifier* e *RandomForestClassifier*, e a partir deles os hiperparâmetros foram testados, através do *GridSearchCV*. O **modelo escolhido**, por apresentar as melhores métricas, após o ajuste de hiperparâmetros, foi o ***XGBClassifier***. O modelo apresentou, nos dados de teste, **83.10% de acurácia e AUC de 0.84**. **Se o paciente realmente precisa de UTI, o modelo tem 82% de chance de acertar**. Enquanto isso,  **no caso do paciente não necessitar de internação em leito de UTI o modelo acerta em 84%**. 

- Será imprescindível tentar melhorar ainda mais estes resultados e difundir o uso de uma ferramenta como essa para definir qual a necessidade de leitos de UTI nos hospitais, não só para o COVID-19, mas para outras doenças - aumentando a excelência no planejamento de recursos e o nível de atendimento ao paciente.

## Notebooks: 

🧹 [Notebook da Limpeza dos Dados](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Notebooks/Valquiria_Alencar_Projeto_final_Limpeza.ipynb)

🤿 [Notebook da Análise Exploratória dos Dados]()

🔮 [Notebook das Previsões com Machine Learning]()
> Para uma experiência melhor eu recomendo que esse notebook seja aberto pelo Google Colaboratory 😉

👩‍💻 Uma publicação no Medium, sumarizando os principais resultados, pode ser encontrada [aqui]()


