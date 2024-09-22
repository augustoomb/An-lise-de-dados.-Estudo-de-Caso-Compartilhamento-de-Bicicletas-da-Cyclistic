# Estudo de Caso: Compartilhamento de Bicicletas da Cyclistic

## Introdução

Neste estudo de caso, analisamos o uso de bicicletas da Cyclistic, uma empresa fictícia de compartilhamento de bicicletas em Chicago, com o objetivo de entender como os ciclistas casuais e os membros anuais utilizam o serviço de forma diferente. Este insight ajudará a desenvolver estratégias para converter ciclistas casuais em membros anuais, aumentando a lucratividade da empresa.

## Declaração da Tarefa de Negócio

A Cyclistic quer maximizar o número de assinaturas anuais, pois os membros anuais são mais lucrativos que os ciclistas casuais. O objetivo do estudo é identificar diferenças no comportamento entre ciclistas casuais e membros anuais para informar estratégias de marketing que possam converter ciclistas casuais em membros.

## Fontes de Dados

Os dados utilizados neste estudo de caso são históricos dos trajetos de bicicleta da Cyclistic, cobrindo os últimos 12 meses. Esses dados incluem informações como:

- Identificadores de viagem
- Hora de início e fim do trajeto
- Estação de partida e de chegada
- Duração da viagem
- Tipo de bicicleta (tradicional, reclinável, triciclo, etc.)
- Categoria do usuário (casual ou membro anual)

**Observação**: Os dados foram fornecidos pela Motivate International Inc. sob licença pública e foram anonimizados para evitar a identificação dos usuários.

## Limpeza e Manipulação de Dados

Os seguintes passos foram seguidos para preparar os dados para análise:

1. **Importação e Unificação dos Dados**: Unificamos os dados dos diferentes arquivos .csv em um único DataFrame.
2. **Cálculo da Duração da Viagem**: Subtraímos a `hora_começo` da `hora_finalização` para calcular a duração de cada trajeto.
3. **Classificação por Dia da Semana**: Criamos uma coluna `dia_da_semana` para identificar em qual dia cada trajeto ocorreu.
4. **Remoção de Valores Inválidos**: Filtramos viagens com duração menor ou igual a 0 minutos.
5. **Formatação**: Padronizamos os dados em colunas, renomeando as colunas e formatando a duração em HH:MM:SS.

## Análise

A análise foi realizada para responder à pergunta: **Como os membros anuais e os ciclistas casuais utilizam as bicicletas da Cyclistic de forma diferente?**

### Principais Descobertas

1. **Diferenças na Duração da Viagem**: Os ciclistas casuais tendem a fazer viagens mais longas (média de 45 minutos) comparado aos membros anuais (média de 12 minutos). Isso sugere que os ciclistas casuais estão mais inclinados a utilizar as bicicletas para lazer, enquanto os membros anuais usam as bicicletas em trajetos diários mais curtos, como para o trabalho.
   
2. **Padrões de Uso ao Longo da Semana**: Ciclistas casuais mostram um aumento significativo de uso nos finais de semana, enquanto membros anuais têm um uso mais distribuído durante os dias úteis. Isso reforça a ideia de que ciclistas casuais utilizam mais as bicicletas para lazer.
   
3. **Tipo de Bicicleta Preferido**: A maioria dos ciclistas casuais prefere bicicletas tradicionais, enquanto os membros anuais têm maior probabilidade de utilizar bicicletas assistivas, como triciclos manuais. Este dado pode ser explorado para campanhas focadas na conveniência do uso diário.

## Visualizações

### Duração Média da Viagem por Tipo de Usuário

![Gráfico de Duração da Viagem](https://github.com/augustoomb/An-lise-de-dados.-Estudo-de-Caso-Compartilhamento-de-Bicicletas-da-Cyclistic/blob/main/dura%C3%A7%C3%A3o%20m%C3%A9dia.png?raw=true)

**Justificativa**: Este gráfico mostra claramente a diferença na duração média das viagens entre ciclistas casuais e membros anuais, o que ajuda a reforçar que os usuários casuais fazem viagens mais longas e esporádicas, enquanto os membros anuais utilizam as bicicletas para deslocamentos rápidos.

### Uso de Bicicletas por Dia da Semana

![Gráfico de Uso por Dia da Semana](https://github.com/augustoomb/An-lise-de-dados.-Estudo-de-Caso-Compartilhamento-de-Bicicletas-da-Cyclistic/blob/main/n%C3%BAmero%20de%20viagens%20por%20tipo%20de%20passageiro.png?raw=true)

**Justificativa**: Esta visualização mostra a diferença de uso entre os dois grupos ao longo dos dias da semana, evidenciando que o pico de uso de ciclistas casuais é durante os finais de semana.

## Recomendações

Com base nos insights extraídos dos dados, as seguintes recomendações são propostas para maximizar o número de assinaturas anuais:

1. **Campanhas Focadas em Benefícios Diários**: Criar campanhas que mostrem como a assinatura anual pode beneficiar o ciclista casual no dia a dia, destacando economia e conveniência em viagens mais curtas.
   
2. **Promoções nos Finais de Semana**: Oferecer descontos ou benefícios exclusivos para ciclistas casuais que usarem a bicicleta nos finais de semana, incentivando-os a experimentar o uso regular durante a semana.

3. **Engajamento Digital**: Usar plataformas de mídia digital para mostrar depoimentos de ciclistas que se tornaram membros anuais, explicando como essa escolha melhorou seu deslocamento diário e ajudou a economizar dinheiro.

## Conclusão

Este estudo mostrou diferenças significativas no comportamento de uso entre ciclistas casuais e membros anuais da Cyclistic. Essas diferenças podem ser utilizadas para criar campanhas direcionadas que incentivem ciclistas casuais a se tornarem membros anuais, aumentando a lucratividade da empresa.

Script R:
```r
# # # # # # # # # # # # # # # # # # # # # # # 
# Instalar pacotes necessários
# tidyverse para importação de dados e wrangling
# lubridate para funções de data
# ggplot para visualização
# # # # # # # # # # # # # # # # # # # # # # #  

library(tidyverse)  #helps wrangle data
library(lubridate)  #helps wrangle date attributes
library(ggplot2)  #helps visualize data
getwd() #exibe seu diretório de trabalho
setwd("/home/augusto/Documentos/projeto-final-dados") #sets your working directory to simplify calls to data ... make sure to use your OWN username instead of mine ;)

#=====================
# PASSO 1: COLETAR DADOS
#=====================
# Upload Divvy datasets (csv files) aqui
q01_2021 <- read_csv("202101-divvy-tripdata.csv")
q02_2021 <- read_csv("202102-divvy-tripdata.csv")
q03_2021 <- read_csv("202103-divvy-tripdata.csv")
q04_2021 <- read_csv("202104-divvy-tripdata.csv")
q05_2021 <- read_csv("202105-divvy-tripdata.csv")
q06_2021 <- read_csv("202106-divvy-tripdata.csv")
q07_2021 <- read_csv("202107-divvy-tripdata.csv")
q08_2021 <- read_csv("202108-divvy-tripdata.csv")
q09_2021 <- read_csv("202109-divvy-tripdata.csv")
q10_2021 <- read_csv("202110-divvy-tripdata.csv")
q11_2021 <- read_csv("202111-divvy-tripdata.csv")
q12_2021 <- read_csv("202112-divvy-tripdata.csv")

#====================================================
# PASSO 2: CONVERTER OS DADOS E COMBINE-OS EM UM ÚNICO ARQUIVO
#====================================================
# Comparar nomes de colunas de cada um dos arquivos
# Embora os nomes não precisem estar na mesma ordem, eles PRECISAM corresponder perfeitamente antes que possamos usar um comando para juntá-los em um arquivo
colnames(q01_2021)
colnames(q02_2021)
colnames(q03_2021)
colnames(q04_2021)
colnames(q05_2021)
colnames(q06_2021)
colnames(q07_2021)
colnames(q08_2021)
colnames(q09_2021)
colnames(q10_2021)
colnames(q11_2021)
colnames(q12_2021)

# Inspecione os dataframes e procure por incongruências
str(q01_2021)
str(q02_2021)
str(q03_2021)
str(q04_2021)
str(q05_2021)
str(q06_2021)
str(q07_2021)
str(q08_2021)
str(q09_2021)
str(q10_2021)
str(q11_2021)
str(q12_2021)

# Converter ride_id and rideable_type para as.character (texto)
q01_2021 <-  mutate(q01_2021, ride_id = as.character(ride_id)
                   ,rideable_type = as.character(rideable_type)) 
q02_2021 <-  mutate(q02_2021, ride_id = as.character(ride_id)
                   ,rideable_type = as.character(rideable_type))
q03_2021 <-  mutate(q03_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q04_2021 <-  mutate(q04_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q05_2021 <-  mutate(q05_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q06_2021 <-  mutate(q06_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q07_2021 <-  mutate(q07_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q08_2021 <-  mutate(q08_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q09_2021 <-  mutate(q09_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q10_2021 <-  mutate(q10_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q11_2021 <-  mutate(q11_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 
q12_2021 <-  mutate(q12_2021, ride_id = as.character(ride_id)
                    ,rideable_type = as.character(rideable_type)) 

# Juntar dados individuais em um único data frame
all_trips <- bind_rows(q01_2021, q02_2021, q03_2021, q04_2021, q05_2021, q06_2021, q07_2021, q08_2021, q09_2021, q10_2021, q11_2021, q12_2021)


#======================================================
# PASSO 3: LIMPE E ADICIONE DADOS PARA PREPARAR PARA ANÁLISE
#======================================================
# Inspecione a nova tabela que foi criada
colnames(all_trips) #Lista de nomes de colunas
nrow(all_trips) #Quantas linhas há no data frame?
dim(all_trips) #Dimensões do data frame?
head(all_trips) #Veja as primeiras 6 linhas do data frame. Também tail(all_trips)
str(all_trips) #Veja a lista de colunas e tipos de dados (numérico, caractere, etc.)
summary(all_trips) #Resumo estatístico de dados. Principalmente para numéricos

# Há alguns problemas que precisaremos corrigir:
# (2) Os dados só podem ser agregados no nível do passeio, o que é muito granular. Queremos adicionar algumas colunas adicionais de dados — como dia, mês, ano — que fornecem oportunidades adicionais para agregar os dados.
# (3) Queremos adicionar um campo calculado para a duração do passeio, já que os dados do 1º trimestre de 2020 não tinham a coluna "tripduration". Adicionaremos "ride_length" a todo o dataframe para consistência.
# (4) Há alguns passeios em que a duração do passeio aparece como negativa, incluindo várias centenas de passeios em que a Divvy tirou as bicicletas de circulação por motivos de controle de qualidade. Queremos excluir esses passeios.



# Adicione colunas que listem a data, mês, dia e ano de cada viagem

# Isso nos permitirá agregar dados de viagem para cada mês, dia ou ano... antes de concluir essas operações, só podíamos agregar no nível da viagem

all_trips$date <- as.Date(all_trips$started_at) # as.Date() vai extrair apenas a parte da data (formato padrão é yyyy-mm-dd) e colocar numa nova coluna
all_trips$month <- format(as.Date(all_trips$date), "%m")
all_trips$day <- format(as.Date(all_trips$date), "%d")
all_trips$year <- format(as.Date(all_trips$date), "%Y")
all_trips$day_of_week <- format(as.Date(all_trips$date), "%A")

# difftime() calcula a diferença entre dois momentos no tempo (in seconds)
all_trips$ride_length <- difftime(all_trips$ended_at,all_trips$started_at)

# Inspecione a estrutura das colunas
str(all_trips)

# Converter "ride_length" de Factor para numérico para que possamos executar cálculos nos dados
# Factors em R são usados para representar dados categóricos, mas podem armazenar valores numéricos como rótulos, dificultando operações matemáticas.
is.factor(all_trips$ride_length) # verificando se a coluna ride_length é um factor.Retorna TRUE se ride_length for um factor, e FALSE caso contrário.

# Converte o factor ride_length em uma string (caractere). Isso é necessário porque factors são armazenados como níveis internos e precisam ser convertidos para texto antes de serem transformados em números.
# Factors podem apresentar níveis que não correspondem diretamente ao valor numérico subjacente, por isso essa etapa de conversão é importante.
all_trips$ride_length <- as.numeric(as.character(all_trips$ride_length))

# verifica se a coluna ride_length agora é numérica.
is.numeric(all_trips$ride_length)



# Remover dados "ruins"
# O dataframe inclui algumas centenas de entradas quando as bicicletas foram retiradas das docas e verificadas quanto à qualidade pelo Divvy ou ride_length era negativo
# Criaremos uma nova versão do dataframe (v2), pois os dados estão sendo removidos

#Joga para dentro do novo data frame(all_trips_v2) todos os dados de all_trips, exceto se:
# - a coluna start_station_name for diferente de "HQ QR" e ride_length for menor que zero
all_trips_v2 <- all_trips[!(all_trips$start_station_name == "HQ QR" | all_trips$ride_length<0),]

#=====================================
# PASSO 4: REALIZAR ANÁLISE DESCRITIVA
#=====================================
# Análise descritiva em ride_length (todos os valores em segundos)
mean(all_trips_v2$ride_length) #Calcular média (total ride length / rides)
median(all_trips_v2$ride_length) #mediana
max(all_trips_v2$ride_length) #viagem mais longa
min(all_trips_v2$ride_length) #viagem mais curta

# Você pode condensar as quatro linhas acima em uma linha usando summary() no atributo específico
summary(all_trips_v2$ride_length)

# Comparar membros Vs. usuários casuais
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = mean)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = median)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = max)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = min)

# Veja o tempo médio de viagem por dia para membros em comparação com usuários casuais
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)

# Observe que os dias da semana estão fora de ordem. Vamos consertar isso.
all_trips_v2$day_of_week <- ordered(all_trips_v2$day_of_week, levels=c("domingo", "segunda", "terça", "quarta", "quinta", "sexta", "sábado"))

# Novamente, vamos calcular o tempo médio de viagem por dia para membros versus usuários casuais
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)



# analisar dados de passageiros por tipo e dia da semana
all_trips_v2 %>% 
  
  mutate(weekday = wday(started_at, label = TRUE)) %>%  # Adiciona uma nova coluna weekday que contém o dia da semana derivado da coluna started_at. O argumento label = TRUE garante que o dia seja mostrado como nome (e.g., "Mon", "Tue"), e não como número.
  
  group_by(member_casual, weekday) %>%  #Agrupa os dados por tipo de usuário (coluna member_casual) e dia da semana (weekday), para que as operações de sumarização sejam aplicadas separadamente para cada grupo.
  
  summarise(number_of_rides = n()  # conta o número de linhas (número de corridas) dentro de cada grupo.
            ,average_duration = mean(ride_length)) %>% 		# calcula a duração média das corridas para cada grupo
  arrange(member_casual, weekday)								# Ordena os resultados de acordo com o tipo de usuário e o dia da semana.



# Visualizar o número de viagens por tipo de passageiro
all_trips_v2 %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>% 
  group_by(member_casual, weekday) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(member_casual, weekday)  %>% 
  ggplot(aes(x = weekday, y = number_of_rides, fill = member_casual)) +
  geom_col(position = "dodge")

# Vamos criar uma visualização para duração média
all_trips_v2 %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>% 
  group_by(member_casual, weekday) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(member_casual, weekday)  %>% 
  ggplot(aes(x = weekday, y = average_duration, fill = member_casual)) +
  geom_col(position = "dodge")

#=================================================
# PASSO 5: EXPORTAR ARQUIVO DE RESUMO PARA ANÁLISE ADICIONAL
#=================================================
# Crie um arquivo csv que visualizaremos no Excel, Tableau ou no meu software de apresentação. 
counts <- aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)
write.csv(counts, file = '/home/augusto/Documentos/projeto-final-dados/avg_ride_length.csv')

---

**Autor**: Augusto Barbosa 
**Data**: 20/09/24  
