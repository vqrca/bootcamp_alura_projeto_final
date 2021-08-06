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

<a name="intro"></a>
# Introdução

## Coronavírus SARS-CoV-2 e a COVID-19

Os coronavírus (CoVs) são vírus de RNA de fita simples que causam doenças em humanos e animais. Os coronavírus humanos (HCoVs - human coronaviruses) foram identificados pela primeira vez como causas de infecções respiratórias agudas em 1962. Nos últimos anos, os HCoVs foram mais frequentemente associados a infecções graves do trato respiratório superior e inferior. Eles foram identificados como a principal causa de pneumonia em adultos mais velhos e pacientes imunocomprometidos [[1]](https://academic.oup.com/cid/article/31/1/96/321510). 
Nas últimas duas décadas, dois coronavírus humanos altamente patogênicos foram identificados, incluindo coronavírus associados à Síndrome respiratória aguda grave e a Síndrome respiratória do Oriente Médio, que surgiu em diferentes regiões do mundo [[2]](https://www.nejm.org/doi/full/10.1056/nejmoa030747). Em 31 de dezembro de 2019, uma nova cepa de coronavírus foi isolada e nomeada como Síndrome respiratória aguda grave coronavírus 2 (SARS-Cov-2) pelo Comitê Internacional de Taxonomia de Vírus (ICTV - International Committee on Taxonomy of Viruses) de pacientes com pneumonia de etiologia desconhecida na cidade de Wuhan, China [[3](https://jamanetwork.com/journals/jama/fullarticle/2760500). 
A doença causada por este novo coronavírus recebeu o  nome  de COVID-19: COVID é a junção de letras que se referem a (co)rona (vi)rus (d)isease, o que na tradução para o português seria "doença do coronavírus". Já o número 19 está ligado a 2019, quando os primeiros casos foram publicamente divulgados [[4]](https://portal.fiocruz.br/pergunta/por-que-doenca-causada-pelo-novo-coronavirus-recebeu-o-nome-de-covid-19). Em 11 de março de 2020, a Organização Mundial da Saúde (OMS) anunciou que COVID-19 é uma "emergência de saúde pública de interesse internacional" [[5]](https://onlinelibrary.wiley.com/doi/10.1002/jmv.25701).
As características clínicas da COVID-19 são variadas e inespecíficas. A apresentação da doença pode variar de assintomática a pneumonia grave e morte [[6]](https://www.who.int/docs/default-source/coronaviruse/who-china-joint-mission-on-covid-19-final-report.pdf).
Foi relatado que os sintomas aparecem após um período de incubação entre 2–14 dias [[7]](https://www.sciencedirect.com/science/article/abs/pii/S0896841120300469). O período desde o início dos sintomas de SARS-CoV-2 até a morte variou de 6 a 41 dias,  dependendo da idade e do estado do sistema imunológico do paciente [[7]](https://www.sciencedirect.com/science/article/abs/pii/S0896841120300469). Além disso, estudos relataram que a COVID-19 progrediu mais rapidamente entre os idosos em comparação com aqueles com idade inferior a 60 anos [[8]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7167192/). Um estudo de pesquisa analisando 1.099 pacientes confirmados por laboratório em Wuhan, encontrou características clínicas comuns caracterizadas como sintomas leves e moderados, que incluem febre (88,7%), tosse (67,8%), fadiga (38,1%), produção de expectoração (33,4%), dispneia (18,7%), dor de garganta (13,9%) e cefaleia (13,6%). No entanto, alguns dos pacientes apresentam sintomas gastrointestinais, com diarreia (3,8%) e vômitos (5,0%). Portadores assintomáticos de SARS-CoV-2, que apresentavam histórico de condições de saúde subjacentes, como hipertensão, doença pulmonar obstrutiva crônica, diabetes, doença cardiovascular, desenvolveram posteriormente doenças críticas, que se manifestaram como insuficiência respiratória, choque séptico, falência de múltiplos órgãos e eventualmente morte [[7]](https://www.sciencedirect.com/science/article/abs/pii/S0896841120300469) [[9]](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext). 
Por ser altamente transmissível, essa nova doença, se espalhou rapidamente por todo o mundo. Superou de forma esmagadora o SARS e o MERS em termos de número de pessoas infectadas e da amplitude espacial das áreas epidêmicas [[10]](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30260-9/fulltext).

## Contexto: Como uma pandemia pode afetar o Sistema de Saúde

Com sua rápida disseminação, a COVID-19 criou uma forte demanda por hospitais e leitos nas UTIs (Unidades de Terapia Intensiva). Esta maior necessidade de recursos hospitalares levou ao colapso dos sistemas de saúde em todo o mundo, o que pode ter contribuído para as maiores taxas de mortalidade relatadas [[11]](https://doi.org/10.1016/S0140-6736(20)30627-9P). Em países com sistemas de saúde já sobrecarregados, como é o caso do Brasil, não havia recursos suficientes de equipamentos médicos, medicamentos e pessoal treinado para lidar com o aumento no número de pacientes com COVID-19 que precisvam de suporte hospitalar [[12]](https://doi.org/10.1056/NEJMsb2005114).


## O problema descrito pelo hospital Sírio Libanês

A pandemia de COVID-19 atingiu o mundo inteiro, sobrecarregando os sistemas de saúde - despreparados para uma solicitação tão intensa e demorada de leitos de UTI, profissionais, equipamentos de proteção individual e recursos de saúde. O Brasil registrou o primeiro caso COVID-19 em 26 de fevereiro de 2020 e atingiu a transmissão na comunidade em 20 de março de 2020. 
Existe uma urgência na obtenção de dados precisos para melhor prever e preparar os sistemas de saúde e evitar colapsos, definido pela necessidade de leitos de UTI acima da capacidade (assumindo que recursos humanos, EPIs e profissionais estejam disponíveis), usando dados clínicos individuais - em vez de dados epidemiológicos e populacionais. Isso seria imprescindível para evitar o colapso no sistema de saúde, como podemos observar na figura abaixo: 

Pensando nisso, o Hospital Sírio Libânes disponibilizou no [Kaggle](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) um dataset contendo informações sobre vários pacientes, com os seguintes objetivos: 

- **Prever admissão na UTI de casos confirmados de COVID-19**, com base em dados disponíveis, para fornecer aos hospitais terciários e trimestrais a resposta mais precisa, para que os recursos da UTI possam ser arranjados ou a transferência do paciente possa ser agendada.

- **Prever NÃO admissão à UTI de casos COVID-19 confirmados**, para fornecer aos hospitais locais e temporários uma resposta boa o suficiente, para que os médicos de linha de frente possam dar alta com segurança e acompanhar remotamente esses pacientes.



