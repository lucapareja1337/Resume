# Resumo do Livro : Projetando sistemas de Machine Learning: processo interativo para aplicações prontas para produção

![Capa do livro](img/Livro.jpg)


# Capítulo 01 - Visão Geral de Sistemas de Aprendizado de Máquina

Este capítulo visa introduzir ao leitor uma série de considerações relevantes na construção e aplicação de modelos de aprendizado de máquina (ML). Entre os tópicos destacados estão a aplicação de redes neurais em larga escala pela Google em sua ferramenta de tradução, o entusiasmo geral em torno do ML e a implementação de modelos de ML em ambientes de produção, bem como MLOPS, que compreende um conjunto de práticas e decisões para disponibilizar o aprendizado de máquina em produção. Considerações sobre quando utilizar ou não o aprendizado de máquina são discutidas, além do reconhecimento de que o ML não é uma solução universal. A definição do ML como uma abordagem para aprender padrões complexos a partir de dados existentes e usá-los para fazer previsões sobre dados desconhecidos é ressaltada. Há ênfase no sucesso em tarefas complexas, como reconhecimento de fala e detecção de objetos, mas também na ressalva de que os padrões aprendidos pelo modelo só serão úteis se os dados desconhecidos compartilharem esses padrões. Outros pontos de destaque incluem a importância da constância e coerência, a necessidade de aplicação em escala e a consideração ética. O capítulo conclui com a observação de que mesmo melhorias pequenas no desempenho do modelo podem resultar em grandes aumentos nos lucros, destacando a importância da manutenção e implementação para a qualidade do modelo, e ressaltando as diferenças de foco entre o meio acadêmico e o mercado em relação ao ML.

# Capítulo 02 - Introdução ao Design de Sistemas de Aprendizado de Máquina

Neste capítulo, abordaremos a importância e os requisitos para o design de sistemas de aprendizado de máquina (ML). Destacamos a necessidade de compreender por que o sistema é necessário e considerar fatores como confiabilidade, escalabilidade, sustentabilidade e adaptabilidade, bem como a importância de delimitar corretamente um problema e criar trilhas a partir dele. Reconhecemos a fundamental importância dos dados e exploramos a relação entre objetivos de negócios e ML, observando que o aumento da acurácia do modelo impacta as métricas de negócios. Apresentamos os requisitos para sistemas de ML, como confiabilidade, escalabilidade, manutenibilidade e adaptabilidade, variáveis de acordo com o contexto e o caso de uso, incluindo considerações detalhadas sobre autoscaling, gerenciamento de artefatos, logística para manutenção de código e documentação. Observamos a importância do aprendizado contínuo para a qualidade do modelo e definimos um problema de ML por entradas, saídas e pela função objetivo que guia o processo de aprendizagem, classificando as tarefas de ML em classificação e regressão com base na saída do modelo.

# Capítulo 03 - Fundamentos de Engenharia de Dados

Neste capítulo, exploramos os fundamentos da engenharia de dados e sua relação com o aprendizado de máquina. Reconhecemos a relação íntima entre big data e ML, enfatizando a importância do armazenamento de dados e sua estruturação. Destacamos a coleta, processamento, armazenamento e recuperação de grandes volumes de dados visando a construção de sistemas de ML em produção. Exploramos as diferentes fontes de dados e seus métodos de leitura, tratamento e treinamento, bem como os formatos de dados, como JSON, CSV e Parquet, e suas características. Analisamos os modelos de dados, como o relacional e o NoSQL, e suas aplicações, além de distinguir entre dados estruturados e não estruturados, destacando suas características e usos. Observamos as vantagens e desvantagens de cada tipo de dado e apresentamos exemplos práticos.

# Cap 04 - Treinando os dados 
O capítulo em questão parte da pespectiva da ciência de dados mediante os dados de treinamento. Uma observação importante que notei, foi a importância em observar a presença de viés nos modelos de Machine Learning, tendo em vista a qualidade dos dados que estão sendo utilizados.

# Amostragem
Visa emular dados do mundo real, ou parte de uma fonte, que devido ao seu tamanho extenso, não é viável para processamento. Assim, forma-se um processo ainda mais barato e rápido.

#Amostragem não probabilísitca
A seleção de dados não se baseia em nenhum critério de probabilidade.
Amostra por conveniência : É conveniente, pois é conduzida de acordo com a disponibilidade de dados.
Amostragem por bola de neve: Processo baseado em amostras previamente existenstes para a condução do modelo.
Amostragem por julgamento: Necessita da intervenção de especialistas para decidir quais amostras serão usadas.
Amostragem por cotas: Feita por meio do fatiamente de dados, de forma não aleatória.

Em muitos casos, a seleção de dados ainda é baseada na conveniência.

A amostragem não probabilística pode ser uma forma mais rápida e fácil de reunir dados iniciais para impulsionar os primeiros passos de um projeto. Porém, buscando uma melhor qualidade e refinamento do modelo, se torna mais seguro optar por uma alternativa probabilística. 

# Amostragem aleatório simples
Oferece probabilidades iguais a cada amsotra para suas seleções.
Fácil de implementar.
Categorias raras podem não aparecer.
Modelos treinados nessas seleções podem não identificar classes raras

# Amostragem estratificada
Dividir os elementos em grupos de intesse e amostrar cada grupo separadamente.
Ajuda a garantir que classes raras serão selecionadas.
Nem sempre será aplicável, pois algumas vezes, uma amostra pode estar inclusa em em diversos grupos.

#Amostragem ponderada
Cada amostra recebe um peso, que determina a probabilidade de ser selecionada.
Leva em conta o conhecimento de domínio
Pode atribuir um peso maior a determinado ponto de interesse.
Ajuda em momentos em que temos dados oriundos de uma distruibuição diferente em comparação aos dados verdadeiros.
É utilizada para selecionar amostras de treino para o modelo, enquantos os pesos amostrais são usados para atribuir a importância de cada amostra de treinamento. Amostras mais relevantes terão mais impacto quanto a função de perda.

#Amostragem Reservoir
Muito versátil para streaming de dados. Apache Kafka, por exemplo.
Não sabe de antemção a probabilidade de dado elemento ser selecionado.
Consiste em entende que cada elemento possua a mesma probabilidade de ser selecionado.
O algorítimo pode ser parado a qualquer momento, e os elementos serão retornados com a respectiva probabilidade.
O processo dessa amostragem, envolve uma lógica de armazenamento, que pode ser um vetor, e gira em torno de três níveis:
Insere os primeiros elementos K no vetor.
Para cada n-ésimo valor recebido, gera um número aleatório i, de modo que 1</ i n</ (Menor igual/Maior igual)
Se 1<i<k: Substitua o i-ésimo elemento no reservatório pelo n-ésimo elemento. Caso contrário, não faça nada.
Desse modo, a ideia é que todas as amostras tenham chance igual de serem selecionadas.

# Amostragem por importância
Possibilita realizar a amostra de uma distruibuição apenas quando há acesso a outra distribuição.


# Rotulagem
A grande maioria dos modelos de ML, precisa de uma rotulagem adequada para seu funcionamento consistente.
Os rótulos manuais geralmente consistem em um processo que demanda intervenção de especialistas para , podendo ser caro e demorado, e ainda tendo em vista o fator da privacidade dos dados em questão.
Multiplicidade de rótulos: É um problema que tem como causa, na maior parte das vezes, o uso de múltiplas fontes de dados, a intervenção de vários especialistas e suas discordâncias mediante a anatoção dos rótulos. Como abordar esse problema? Em primeior lugar, é importante ter em mente uma visão objetiva do que está ocorrendo. Para isso, pode-se adotar uma aentidade que possua um conceito mais amplo para rotular as classes, e assim também atender a regra de negócio atribuida.
Várias fontes de dados e vários especialistas envolvidos nem sempre vão ajudar.
Data Lineage: Consiste em monitorar as fontes de dados e seus respectivos rótulos. Este processo, acaba favorecendo a melhoria do modelo e a investigação de possíveis viéses.

# Rótulos Naturais
 Diz respeito a ações em que as predições do modelo podem ser avaliadas de forma parcial ou totalmente automatica pelo sistema.
Sistemas de recomendação são um bom caso de uso de rótulos naturais.
Extensão loop feedback: Tarefas em que os rótulos naturais sejam adquiridos em poucos minutos. Sistemas de recomendação geralmetne adotam loops de feedback curtos, o que implica na inferência de um rótulo variar conforme o contexto de interesse.
# Lidando com a falta de rótulos
Weak supervision: Utiliza heurísticas, geralmente as que apresentam ruído, para atribuição de rótulos. Se recomenda um mínimo número de rótulos para direcionar as heurísticas atribuídas.
Semisupervisão: Adota suposições estruturais para criação de rótulos. Precisa de um pequeno número de rótulos para compreende-los como seus e gerar mais rótulos a partir disso.
Aprendizado por transferência: Direciona-se à modelos pré-treinados em uma situação para abordar o novo problema. Para o aprendizado zero-shot, não necessita dispor de um ground-truth, porém caso precise fazer um fine-tuning, será necessário.
Aprendizado ativo: Rotula as amostras mais úteis para aplicação no modelo, e o ground-truth faz-se imprescindível.
Porgramatic Labeling nos oferece uma alternativa mais rápida e barata, e que preza pela privacidade de dados.
O aprendizado por transferência pode ser bem utilizado para tarefas que não tem muitos dados rotulados, e ainda pode auxiliar na redução de custos quanto as aplicações de Machine Learning.

# Classes desbalanceadas
Configura uma distruibuição discrepante entre as classes presentes em uma amostra, podendo prejudicar um eventual modelo. Por isso, pode-se modificar o modelo para calcular as métricas de um percentil mais bem ajustado.
Omodelo as vezes pode entender que uma classe rara não existe.
O modelo pode ficar preso em uma solução não ideal.
Uma predição errada mediante uma classe rara pode levar à um alto custo.

No mundo real, é mais comum lidarmos com grupos de classe que não apresentam equilibrio, e justamente por isso, essas classes tem sido foco de estudo dos últimos 20 anos.
A sensibilidade deste estado pode variar conforme o nível de complexidade do problema.
Um bom modelo, precisa atuar bem com o desbalanceamente.

# Métricas adequadas para avaliação
As métricas certas podem proporcionar um bom direcionamento para a problemática, por isso devem ser tratadas com cautela.
Acurácia e taxa de erro são as mais comuns entre os modelos de ML, mas não atendem muito bem as classes desbalanceadas, pois esses métricas dependem de classes balanceadas para retornarem um resultado coerente.
F1 Score, precisão e recall, calculam a qualidade do modelo tendo como base o verdadeiro positivo. São meios assimétricos para o direcionamento da avaliação do modelo, ou seja, o profissional pode arbitrar qual classe é o verdadeiro positivo.
A curva ROC, também foi apontada como uma boa métrica de avaliação, para medir a qualdiade de um modelo, tendo em vista a presença de classes desbalanceadas.
# Reamostragem
 Consiste em alterar a distribuição dos dados utilizados para treinar o modelo, visando facilitar sua execução. Nisso há dois caminho, o oversampling, voltado a aumentar o quantitativo de classes minoritárias e o undersampling que remove elementos vinculados a classes majoritárias.
Nivel de algorítimo: Visa otimizar a formatação do código para abordar de forma adequada o trabalho com classes desbalanceadas.
# Data Augmentation
Conjunto de técnicas para ampliar a quantidade de dados de treinamento.
Transformação simples de preservação de rótulos
Consiste em aumentar o número de dados, modificando dados pré-existentes sem mudar o contexto da informação, e ainda sendo capaz de manter os rótulos.
# Pertubação
Adicionar amostras ruidosas aos dados, induzindo o modelo ao erro. É útil para testar falhas no modelo, proporcionando a resolução de eventuais problemas.
Síntese de dados, consiste em sintetizar a base de dados para otimizar o trabalho imposto ao modelo.

O capítulo 4, compila uma série de mecanismos e etapas que nos ajudam a compreender como é possível desenvolver uma trilha adequada para o desenvolvimento de um modelo de Machine Learning. Tópicos como Pertubação e Data Augmentation, apontam formas interessantes de se adaptar o processo de condução de um projeto, abrindo portas para o teste de vulnerabilidades no modelo e aumento artificial do volume de dados para aprimorar o nível de aprendizado. Além disso, propostas para rotulagem de dados, são sempre bem vindas para buscar o melhor valor na aplicação do modelo. Tudo isso somado, constitui um conjunto de algumas das boas práticas para a produção de um modelo de machine learning resiliente.
