[![Badge](https://img.shields.io/badge/Author-Valquíria_Alencar-%237159c1?style=flat-square&logo=ghost)](https://github.com/vqrca/) [![Gmail Badge](https://img.shields.io/badge/-valquiria.c.alencar@gmail.com-6633cc?style=flat-square&logo=Gmail&logoColor=white&link=mailto:valquiria.c.alencar@gmail.com)](mailto:valquiria.c.alencar@gmail.com)[![Linkedin Badge](https://img.shields.io/badge/-Valquíria_Alencar-6633cc?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/valquiria-alencar/)](https://www.linkedin.com/in/valquiria-alencar/) [![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg?style=flat-square)](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/LICENSE)

<p align="center"> 
 <img src="https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Images/cover_projeto_final.png" />
</p>

# **Sumário:**
<!--ts-->
   * [Resumo](#resumo)
   * [Introdução](#intro)
   * [Objetivo](#obj)
   * [Métodos](#met)
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

🤿 [Notebook da Análise Exploratória dos Dados](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Notebooks%5CValquiria_Alencar_Projeto_final_An%C3%A1lise_Explorat%C3%B3ria_Features.ipynb)

🔮 [Notebook das Previsões com Machine Learning](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Notebooks/Valqu%C3%ADria_Alencar_Projeto_final_ML.ipynb)
> Para uma experiência melhor eu recomendo que esse notebook seja aberto pelo Google Colaboratory 😉

👩‍💻 Uma publicação no Medium, sumarizando os principais resultados, pode ser encontrada [aqui]()

<a name="intro"></a>
# Introdução

## Coronavírus SARS-CoV-2 e a COVID-19

- **Os coronavírus (CoVs) são vírus de RNA de fita simples que causam doenças em humanos e animais**. Os coronavírus humanos (HCoVs - human coronaviruses) foram identificados pela primeira vez como causas de infecções respiratórias agudas em 1962. Nos últimos anos, os HCoVs foram mais frequentemente associados a infecções graves do trato respiratório superior e inferior. Eles foram identificados como a principal causa de pneumonia em adultos mais velhos e pacientes imunocomprometidos [[1]](https://academic.oup.com/cid/article/31/1/96/321510). 
- **Nas últimas duas décadas, dois coronavírus humanos altamente patogênicos foram identificados**, incluindo coronavírus associados à **Síndrome respiratória aguda grave e a Síndrome respiratória do Oriente Médio**, que surgiu em diferentes regiões do mundo [[2]](https://www.nejm.org/doi/full/10.1056/nejmoa030747). **Em 31 de dezembro de 2019, uma nova cepa de coronavírus foi isolada e nomeada como Síndrome respiratória aguda grave coronavírus 2 (SARS-Cov-2)** pelo Comitê Internacional de Taxonomia de Vírus (ICTV - International Committee on Taxonomy of Viruses) de pacientes com pneumonia de etiologia desconhecida na cidade de Wuhan, China [[3]](https://jamanetwork.com/journals/jama/fullarticle/2760500). 
- A doença causada por este novo coronavírus recebeu o  nome  de **COVID-19: COVID é a junção de letras que se referem a (co)rona (vi)rus (d)isease**, o que na tradução para o português seria "doença do coronavírus". Já o número 19 está ligado a 2019, quando os primeiros casos foram publicamente divulgados [[4]](https://portal.fiocruz.br/pergunta/por-que-doenca-causada-pelo-novo-coronavirus-recebeu-o-nome-de-covid-19). Em 11 de março de 2020, a Organização Mundial da Saúde (OMS) anunciou que COVID-19 é uma "emergência de saúde pública de interesse internacional" [[5]](https://onlinelibrary.wiley.com/doi/10.1002/jmv.25701).
- As características clínicas da COVID-19 são variadas e inespecíficas. **A apresentação da doença pode variar de assintomática a pneumonia grave e morte** [[6]](https://www.who.int/docs/default-source/coronaviruse/who-china-joint-mission-on-covid-19-final-report.pdf).
Foi relatado que os **sintomas aparecem após um período de incubação entre 2–14 dias** [[7]](https://www.sciencedirect.com/science/article/abs/pii/S0896841120300469). O período desde o início dos sintomas de SARS-CoV-2 até a morte variou de 6 a 41 dias,  dependendo da idade e do estado do sistema imunológico do paciente [[7]](https://www.sciencedirect.com/science/article/abs/pii/S0896841120300469). Além disso, **estudos relataram que a COVID-19 progrediu mais rapidamente entre os idosos em comparação com aqueles com idade inferior a 60 anos** [[8]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7167192/). Um estudo de pesquisa analisando 1.099 pacientes confirmados por laboratório em Wuhan, encontrou características clínicas comuns caracterizadas como sintomas leves e moderados, que incluem febre (88,7%), tosse (67,8%), fadiga (38,1%), produção de expectoração (33,4%), dispneia (18,7%), dor de garganta (13,9%) e cefaleia (13,6%). 
- No entanto, alguns dos pacientes apresentam sintomas gastrointestinais, com diarreia (3,8%) e vômitos (5,0%). Portadores assintomáticos de SARS-CoV-2, que apresentavam histórico de condições de saúde subjacentes, como hipertensão, doença pulmonar obstrutiva crônica, diabetes, doença cardiovascular, desenvolveram posteriormente doenças críticas, que se manifestaram como insuficiência respiratória, choque séptico, falência de múltiplos órgãos e eventualmente morte [[7]](https://www.sciencedirect.com/science/article/abs/pii/S0896841120300469) [[9]](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext). 
- **Por ser altamente transmissível, essa nova doença, se espalhou rapidamente por todo o mundo**. Superou de forma esmagadora o SARS e o MERS em termos de número de pessoas infectadas e da amplitude espacial das áreas epidêmicas [[10]](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30260-9/fulltext).

## Contexto: Como uma pandemia pode afetar o Sistema de Saúde

Com sua rápida disseminação, a COVID-19 criou uma **forte demanda por hospitais e leitos nas UTIs** (Unidades de Terapia Intensiva). Esta maior necessidade de recursos hospitalares levou ao **colapso dos sistemas de saúde em todo o mundo**, o que pode ter contribuído para as maiores taxas de mortalidade relatadas [[11]](https://doi.org/10.1016/S0140-6736(20)30627-9P). Em países com sistemas de saúde já sobrecarregados, como é o caso do Brasil, não havia recursos suficientes de equipamentos médicos, medicamentos e pessoal treinado para lidar com o aumento no número de pacientes com COVID-19 que precisavam de suporte hospitalar [[12]](https://doi.org/10.1056/NEJMsb2005114).


## O problema descrito pelo hospital Sírio Libanês

A pandemia de COVID-19 atingiu o mundo inteiro, sobrecarregando os sistemas de saúde - despreparados para uma solicitação tão intensa e demorada de leitos de UTI, profissionais, equipamentos de proteção individual e recursos de saúde. O Brasil registrou o primeiro caso COVID-19 em 26 de fevereiro de 2020 e atingiu a transmissão na comunidade em 20 de março de 2020. 
**Existe uma urgência na obtenção de dados precisos para melhor prever e preparar os sistemas de saúde e evitar colapsos**, definido pela necessidade de leitos de UTI acima da capacidade (assumindo que recursos humanos, EPIs e profissionais estejam disponíveis), usando dados clínicos individuais - em vez de dados epidemiológicos e populacionais. Isso seria imprescindível para evitar o colapso no sistema de saúde, como podemos observar na figura abaixo: 

<p align="center"> 
 <img src="https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Images/curva-corrigido-post.gif" />
</p>

Pensando nisso, o Hospital Sírio Libânes disponibilizou no [Kaggle](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) um dataset contendo informações sobre vários pacientes, com os seguintes objetivos: 

- **Prever admissão na UTI de casos confirmados de COVID-19**, com base em dados disponíveis, para fornecer aos hospitais terciários e trimestrais a resposta mais precisa, para que os recursos da UTI possam ser arranjados ou a transferência do paciente possa ser agendada.

- **Prever NÃO admissão à UTI de casos COVID-19 confirmados**, para fornecer aos hospitais locais e temporários uma resposta boa o suficiente, para que os médicos de linha de frente possam dar alta com segurança e acompanhar remotamente esses pacientes.

<a name="obj"></a>
# Objetivo
O objetivo deste projeto é **prever** quais pacientes precisarão ser admitidos na unidade de terapia intensiva e assim, **definir** qual a necessidade de leitos de UTI do hospital, a partir dos dados clínicos individuais disponíveis.
> Quando conseguimos definir a quantidade de leitos necessários em um determinado hospital, conseguimos evitar rupturas, visto que, caso outra pessoa procure ajuda e, eventualmente, precise de cuidados intensivos, o modelo preditivo já conseguirá detectar essa necessidade e, desta forma, a remoção e transferência deste(a) paciente pode ser organizada antecipadamente.

<a name="met"></a>
# Métodos

## Coleta dos dados 🎲
Os dados utilizados neste projeto foram obtidos da base de dados da COVID-19, disponibilizada pelo Hospital Sírio Libanês, no [Kaggle](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) e foram armazenados na pasta [Data](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Data/Kaggle_Sirio_Libanes_ICU_Prediction.xlsx) deste respositório. 
> Após, a etapa de limpeza dos dados, o arquivo final foi salvo na pasta [Clean](https://github.com/vqrca/bootcamp_alura_projeto_final/tree/main/Data/Clean) deste respositório.
>  
Nesta base de dados encontramos diversos tipos de informações que foram separadas em 4 grupos:
- Informações demográficas - 3 variáveis do tipo categórica
- Doenças pré-existentes - 9 variáveis do tipo categórica
- Resultados do exame de sangue - 36 variáveis, do tipo contínua: quando necessário, expandidas em média, mediana, max, min, diff(max-min) e diff relativa (diff/mediana)
- Sinais vitais - 6 variáveis do tipo contínua
- Neste dataset, temos algumas janelas de dados, coluna denominada como WINDOW, onde os pacientes foram agregados por janelas em ordem cronológica, que correspondem ao tempo que os pacientes entraram na UTI após a admissão no hospital: 
 
|WINDOW|DESCRIÇÃO|
|:---------:|:-----------------------------------:|
| 0-2	    |  From 0 to 2 hours of the admission |
| 2-4	    | From 2 to 4 hours of the admission  |
| 4-6	    |  From 4 to 6 hours of the admission |
| 6-12    |	From 6 to 12 hours of the admission |
| Above-12|     	Above 12 hours from admission |

- No dataset também temos uma coluna denominada ICU, que corresponde à entrada do paciente na UTI.

Então, foi um critério obrigatório para este projeto, não utilizar os dados quando o paciente deu entrada na UTI: ICU = 1,  pois não sabemos se os dados dos exames de sangue foram coletados antes ou depois do paciente ter sido encaminhado para UTI.

Além disso, somente a janela de 0-2 horas foi utilizada, já que quanto mais cedo a previsão for feita é melhor, tornando-se clinicamente mais relevante.

**Após a importação das bibliotecas e dos dados, as seguintes etapas foram realizadas:**

## Limpeza dos dados 🧹
Todos os processos de pré-processamento dos dados estão disponíveis do [Notebook da Limpeza dos Dados](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Notebooks/Valquiria_Alencar_Projeto_final_Limpeza.ipynb).

## Análise exploratória 🤿
Todas as análises realizadas para explorar os dados antes de testar os modelos de Machine Learning estão disponíveis no [Notebook da Análise Exploratória dos Dados](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Notebooks%5CValquiria_Alencar_Projeto_final_An%C3%A1lise_Explorat%C3%B3ria_Features.ipynb).

## Modelos de Machine Learning 🔮
Conceitos sobre Machine Learning, modelos testados e análise de métricas estão disponíveis no [Notebook das Previsões com Machine Learning](https://github.com/vqrca/bootcamp_alura_projeto_final/blob/main/Notebooks/Valqu%C3%ADria_Alencar_Projeto_final_ML.ipynb).
> Para uma experiência melhor eu recomendo que esse notebook seja aberto pelo Google Colaboratory 😉

## Bibliotecas utilizadas e suas respectivas funções 🐍
- Featurewiz: Seleção das melhores features do dataset
- Lazypredict: Construção de modelos de Machine Learning
- Matplotlib: Plotar os gráficos
- Numpy: Cálculos numéricos
- Pandas: Manipulação dos datasets
- Sckit-learn: Métricas para avaliar os modelos gerados 
- Seaborn: Plotar os gráficos
> O notebook *.ipynb* foi construído no google colab usando Python 3.7.10

<a name="conclusoes"></a>
# Conclusões 💡

- Ao realizar a análise exploratória dos dados, antes de aplicar os modelos de Machine Learning, é possível tirar as seguintes conclusões:

 	- Após realizar todas as etapas de limpeza, vemos que o **conjunto de dados** não está desbalanceado, pois o número de pacientes internados na UTI e o número de entradas não admitidas na UTI é próximo. Portanto, **não existe desequilíbrio para a variável que vamos prever e não será necessário realizar um balanceamento nos modelos de Machine Learning**.

	- Vemos que até a faixa etária de 60 anos a maior parte dos pacientes não vai para UTI. Na faixa etária de 70 anos vemos que 50% dos pacientes precisaram de internação na UTI e **após os 80 anos as chances de ir para UTI aumentam bruscamente**. 

	- É possível observar que **as chances de internação são menores nas mulheres**. Estudos já mostraram que a COVID-19 tem uma incidência maior em homens, que têm 50% mais probabilidade de morrer de COVID-19 do que mulheres ([Saghazadeh & Rezaei, 2020](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7157951/); [Qin *et al.,* 2020](https://pubmed.ncbi.nlm.nih.gov/32161940/))

	- **Os pacientes com hipertensão e os paciente imunocomprimidos apresentaram uma chance ligeiramente maior de precisar da UTI**. Alguns resultados clínicos com COVID-19 indicam que as comorbidades associadas ao envelhecimento, como diabetes e função renal prejudicada, além da hipertensão, estão entre os fatores importantes que determinam a necessidade de internação em UTI [(Martini *et al.,* 2020)](https://pubmed.ncbi.nlm.nih.gov/32319439/).

 	- Além disso, outros estudos já mostraram pacientes com comprometimento do sistema imunológico (imunocomprometidos), valores (carga viral) do exame de PCR, porcentagem de LDH ou desidrogenase láctica, sódio, baixa saturação de O2 e percentual de idade são fatores ligados à admissão na UTI [(Huang *et al.,* 2020](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext); [Wang *et al.,* 2020)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7042881/).

	- Outra *feature* que não foi analisada graficamente, mas que é extremamente relevante é o sódio, um mineral importante para o corpo e ajuda a regular a quantidade de água dentro e ao redor das células. O nível de sódio no sangue é um dos fatores importantes na predição da probabilidade de admissão na UTI. A diminuição excessiva ou acentuada do nível de sódio no sangue é um dos importantes fatores preditivos na determinação da necessidade de admissão na UTI [(Lippi *et al.,* 2020)](https://pubmed.ncbi.nlm.nih.gov/32266828/).

- Entre as *features* que os modelos mais deram importância, podemos destacar: `LEUKOCYTES_MEDIAN`, `PCR_MEDIAN`, `CALCIUM_MEDIAN` e `AGE_PERCENTIL`. A *feature* `LEUKOCYTES_MEDIAN` foi uma das principais em três dos quatro modelos testados. 

  - O aumento da contagem total de leucócitos e contagem diferencial de neutrófilos foi mais comumente observado em pacientes com COVID-19 grave ([Yuan *et al.,* 2020](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7103893/); [Anurag *et al.,* 2020](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7605785/)).
 
  - A quantidade de vírus que pode ser encontrada através da análise de PCR afeta diretamente o processo inflamatório agudo que ocorre em diferentes tecidos, especialmente os tecidos dos pulmões, vasos sanguíneos e rins, o que contribui para a deterioração do estado do paciente ([Martini *et al.,* 2020](https://pubmed.ncbi.nlm.nih.gov/32319439)).
 
  - Estudos realizados por [Zhou e colaboradores (2020)](https://portlandpress.com/bioscirep/article/40/12/BSR20202690/227080/Low-serum-calcium-a-new-important-indicator-of#3174684), mostraram que o equilíbrio de cálcio é um golpe primário de COVID-19 e um biomarcador de gravidade clínica no início do início dos sintomas. O cálcio está intimamente associado a lesões em múltiplos órgãos associadas ao aumento de citocinas inflamatórias. 
	
  - Em pacientes com COVID-19, a idade tem sido apontada como um importante fator de risco para doença mais grave e mortalidade ([Zou *et al.,* 2020](https://linkinghub.elsevier.com/retrieve/pii/S0140673620305663)).
	

- O modelo gerado pelo **XGBClassifier** apresentou a melhor acurácia (83.10%) e um AUC de 0.84.

- Diversos trabalhos têm mostrado que o uso do modelo XGBClassifier traz bons resultados, já que ele possui um algoritmo de árvore impulsionada, para construir o modelo. Sendo assim, esse modelo pode controlar o *overfitting* seguindo o princípio do aumento de gradiente e usando a formalização de modelo mais regularizado, o que lhe confere um desempenho aprimorado. Esse modelo foi projetado para portabilidade, desempenho e eficiência, o que o torna um método de aprendizado de máquina de última geração para dados tabulares ([Friedman, 2001](https://projecteuclid.org/journals/annals-of-statistics/volume-29/issue-5/Greedy-function-approximation-A-gradient-boostingmachine/10.1214/aos/1013203451.full ) , [Chen & Guestrin, 2016](https://arxiv.org/pdf/1603.02754.pdf) , [Ezz *et al.,* 2021](https://www.techscience.com/cmc/v69n2/43880)).

- O modelo **XGBClassifier** contendo os hiperparâmetros: 
`XGBClassifier(learning_rate=0.02, colsample_bytree=0.6, gamma=1, max_depth=6, min_child_weight=1, subsample = 1.0)` foi escolhido como o melhor neste projeto:

  - Teve um acerto de **0.82** para pacientes que devem ser internados na UTI (**verdadeiro positivo**) e de **0.84** para pacientes que não devem ser internados (**verdadeiro negativo**).
 
  - Além disso, o modelo teve **0.16** para pacientes que devem ser internados, mas que na realidade não deveriam ser internados (**falso positivo**) e **0.18** para pacientes que não deveriam ser internados, sendo que necessitavam de internação (**falso negativo**).

- Após analisar o *Classification Report* desse modelo, é possível observar que:

  - Para valores igual a 0 (pacientes que não precisam de UTI), possuímos uma precisão de 79% e para valores iguais a 1 (pacientes que precisam de UTI) a precisão é de 83%. 
 
  - O *Recall* apresentou um desempenho ótimo para valores iguais a 0 (de 87%) e de 73% para valores iguais a 1. 
 
  - O *F1 score* nos mostra uma média harmônica entre precisão e recall. Para 0, apresentou 82% e para 1 apresentou 77%.

- Estudos anteriores realizados por [Ezz e colaboradores (2021)](https://www.techscience.com/cmc/v69n2/43880) com o mesmo dataset utilizado neste trabalho e com o mesmo modelo (XGBClassifier), porém empregando os dados coletados nas primeiras 12 horas em quatro estágios de acordo com janelas de tempo, mostraram que na primeira janela (0-2 horas) o modelo o atingiu uma AUC de 0.73 e conforme as análises foram feitas nas janelas seguintes, foi observado que o desempenho do modelo melhora, atingindo valores de AUCs de 0.92 (janela de 2-4 horas), 0.95 (janela de 4-6 horas) e 0.97 (janela de 6-12 horas). Desse modo, vemos que o pré-processamento e hiperparâmetros definidos aqui gerou com esse mesmo modelo um AUC de 0.84 na janela inicial (0-2 horas), o que é algo relevante e que pode ser ainda melhorado utilizando essas janelas seguintes. 

<a name="final"></a>
# Considerações finais 🚀

- Será imprescindível tentar melhorar ainda mais estes resultados, tentando utilizar as janelas seguintes à janela inicial de 0-2 horas. 

- Os valores de acertos para falsos negativos e falsos positivos precisam ser melhorados, pois é extremamente ruim, por exemplo, não conceder o leito de UTI para alguém que precisa, mas que foi marcado como falso negativo. 

- Por último, ferramentas como essa, após possuírem alta sensibilidade e desempenho na classificação, precisam ser difundidas para definir qual a necessidade de leitos de UTI nos hospitais, não só para o COVID-19, mas quem sabe para outras doenças - aumentando a excelência no planejamento de recursos e o nível de atendimento ao paciente.


<a name="ref"></a>
# **Referências** 📄
[[1]](https://academic.oup.com/cid/article/31/1/96/321510)  El-Sahly HM, Atmar RL, Glezen WP, et al. Spectrum of clinical illness in hospitalized patients with “common cold” virus infections. Clinl Infect Dis. 2000; 31(1):96–100.
 
[[2]](https://www.nejm.org/doi/full/10.1056/nejmoa030747 ) Drosten C, Günther S, Preiser W, et al. Identification of a novel coronavirus in patients with severe acute respiratory syndrome. N Engl J Med. 2003; 348(20):1967–1976.
 
[[3]](https://jamanetwork.com/journals/jama/fullarticle/2760500)  Phelan AL, Katz R, Gostin LO. The novel coronavirus originating in Wuhan, China: challenges for global health governance. JAMA. 2020 Jan 30; 323(8):709.
 
[[4]](https://portal.fiocruz.br/pergunta/por-que-doenca-causada-pelo-novo-coronavirus-recebeu-o-nome-de-covid-19) Portal Fiocruz: COVID-19 Perguntas e Respostas
 
[[5]](https://onlinelibrary.wiley.com/doi/10.1002/jmv.25701)  Li X, Wang W, Zhao X, et al. Transmission dynamics and evolutionary history of 2019-nCoV. J Med Virol. 2020 May;92(5):501–511.
 
[[6]](https://www.who.int/docs/default-source/coronaviruse/who-china-joint-mission-on-covid-19-final-report.pdf)  Organization WH, Organization WH Report of the who-china joint mission on coronavirus disease 2019 (COVID-19). Geneva; 2020.

[[7]](https://www.sciencedirect.com/science/article/abs/pii/S0896841120300469)  Rothan HA, Byrareddy SN. The epidemiology and pathogenesis of coronavirus disease (COVID-19) outbreak. J Autoimmun. 2020; 109:102433.

[[8]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7167192/) Wang W, Tang J, Wei F. Updated understanding of the outbreak of 2019 novel coronavirus (2019‐nCoV) in Wuhan, China. J Med Virol. 2020;92(4):441–447.

[[9]](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext)  Huang C, Wang Y, Li X, et al. Clinical features of patients infected with 2019 novel coronavirus in Wuhan, China. Lancet. 2020; 395(10223):497–506.

[[10]](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30260-9/fulltext) Nowcasting and forecasting the potential domestic and international spread of the 2019-nCoV outbreak originating in Wuhan, China: a modelling study. 

[[11]](https://doi.org/10.1016/S0140-6736(20)30627-9) Remuzzi A, Remuzzi G. COVID-19 and Italy: what next? The Lancet. 2020; 395(10231):1225–8.


[[12]](https://doi.org/10.1056/NEJMsb2005114) Emanuel EJ, Persad G, Upshur R, Thome B, Parker M, Glickman A, et al. Fair Allocation of Scarce Medical Resources in the Time of Covid-19. N Engl J Med. 2020; 382(21):2049–55. 

[[13]](http://ganj-ie.iust.ac.ir:8081/images/6/69/Interpretable-machine-learning.pdf) Molnar, Christoph. Interpretable Machine Learning: A Guide for Making Black Box Models Explainable, 2018. 

[[14](https://pubmed.ncbi.nlm.nih.gov/32319439) Martini N, Piccinni C, Pedrini A, Maggioni A. CoViD-19 e malattie croniche: conoscenze attuali, passi futuri e il progetto MaCroScopio [CoViD-19 and chronic diseases: current knowledge, future steps and the MaCroScopio project.]. Recenti Prog Med. 2020; Apr;111(4):198-201.

[[15]](https://linkinghub.elsevier.com/retrieve/pii/S0140673620305663) Zhou F, Yu T, Du R, Fan G, Liu Y, Liu Z, et al. Clinical course and risk factors for mortality of adult inpatients with COVID-19 in Wuhan, China: a retrospective cohort study. Lancet (London, England). 2020; 395(10229):1054–62. pmid:32171076

[[16]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7103893/) Yuan J, Zou R, Zeng L, et al. The correlation between viral clearance and biochemical outcomes of 94 COVID-19 infected discharged patients. Inflamm Res. 2020; 69(6):599-606. 

[[17]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7605785/) Anurag A, Jha PK, Kumar A. Differential white blood cell count in the COVID-19: A cross-sectional study of 148 patients. Diabetes Metab Syndr. 2020; 14(6):2099-2102. 

[[18]](https://portlandpress.com/bioscirep/article/40/12/BSR20202690/227080/Low-serum-calcium-a-new-important-indicator-of#3174684) Xi Zhou, Dong Chen, Lan Wang, Yuanyuan Zhao, Lai Wei, Zhishui Chen, Bo Yang; Low serum calcium: a new, important indicator of COVID-19 patients from mild/moderate to severe/critical. Biosci Rep 23 December 2020; 40 (12): BSR20202690. doi:

[[19]](https://projecteuclid.org/journals/annals-of-statistics/volume-29/issue-5/Greedy-function-approximation-A-gradient-boostingmachine/10.1214/aos/1013203451.full) Friedman J. H. Greedy function approximation: A gradient boosting machine. Annals of statistics, 2001; 29(5): 1189–1232.

[[20]](https://arxiv.org/pdf/1603.02754.pdf) Chen T, Guestrin C. Xgboost: A scalable tree boosting system, in The 22nd ACM SIGKDD Int. Conf. 2016; San Francisco, California, USA, pp. 785–794. 

[[21]](https://www.techscience.com/cmc/v69n2/43880) Ezz M, Elbashir M. K,, Shabana H. Predicting the Need for ICU Admission in COVID-19 Patients Using XGBoost. CMC-Computers, Materials & Continua, 2021; 69(2): 2077–2092.

[[22]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7157951/) Saghazadeh A, Rezaei N. Immune-epidemiological parameters of the novel coronavirus—a perspective. Expert Rev Clin Immunol. 2020; 16(5):465–70 

[[23]](https://pubmed.ncbi.nlm.nih.gov/32161940/) Qin C, Zhou L, Hu Z, Zhang S, Yang S, Tao Y, et al. Dysregulation of Immune Response in Patients With Coronavirus 2019 (COVID-19) in Wuhan, China. Clinical Infectious Diseases. 2020; 71(15):762–8.

[[24]](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext) Huang C, Wang Y, Li X, Ren L, Zhao J et al. Clinical features of patients infected with 2019 novel coronavirus in Wuhan, China. The Lancet.2020; 395(10223): 497–506, 2020.

[[25]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7042881/) Wang D, Hu B, Hu C, Zhu F, Liu X et al. Clinical characteristics of 138 hospitalized patients with 2019 novel coronavirus–infected pneumonia in Wuhan, China. JAMA Journal. 2020, 323(11): 1061–1069, 2020.

[[26]](https://pubmed.ncbi.nlm.nih.gov/32266828/) Lippi G, South AM, and Henry BM. Electrolyte imbalances in patients with severe coronavirus disease 2019 (covid19). Annals of Clinical Biochemistry. 2020; 57(3): 262–265, 2020.

<a name="doc"></a>
# Documentação 📚

[Featurewiz](https://pypi.org/project/featurewiz/) 

[Lazypredict](https://pypi.org/project/lazypredict/) 

[Matplotlib](https://matplotlib.org/)
 
[Numpy](https://numpy.org/)
 
[Pandas](https://pandas.pydata.org/)
 
[Scikit-learn](https://scikit-learn.org/)
 
[Seaborn](https://seaborn.pydata.org/)
 
<a name="agra"></a>
# Agradecimentos 👏

Esse Bootcamp mudou a minha vida e me deu o desejo de reinventar a minha carreira. Foi durante ele que surgiram oportunidades profissionais para migração de área. Sem dúvidas, hoje uma das minhas maiores alegrias é ter entrado no mundo dos Dados. 

Gostaria de deixar meu agradecimento a todos os instrutores do Bootcamp: Thiago Gonçalves, Guilherme Silveira, Allan Spadini e Karoline Penteado. Vocês foram incríveis e trouxeram conteúdos maravilhosos, sempre de forma didática.

Aos amigos que fiz nesse Bootcamp e que levarei para vida: Os Bootcampers Carolina Dias e Junior Torres. 
	
Ao Glaudemias Grangeiro, o nosso Rei dos mapas, com quem eu tive muitas discussões relevantes sobre os projetos. 

Ao João Vitor pelos cafezinhos e por nos dar dicas valiosas sobre como melhorar as apresentações  

Ao pessoal do Scuba Team e do Discord, que em todos esses meses tiraram dúvidas, trouxeram discussões e ideias muito interessantes

E é claro, obrigada por terem acreditado no meu potencial e pela bolsa de estudos para esse Bootcamp! ❤️

<p align="center"> <img src=https://media.giphy.com/media/ZfK4cXKJTTay1Ava29/giphy.gif </p>


<a name="contact"></a>
# Onde encontrar meu trabalho? 📪
 
[Medium](https://valquiria-c-alencar.medium.com/)
 
[LinkedIn](https://www.linkedin.com/in/valqu%C3%ADria-alencar-786a8911b/)
 
[ResearchGate](https://www.researchgate.net/profile/Valquiria-Alencar)
 
 

