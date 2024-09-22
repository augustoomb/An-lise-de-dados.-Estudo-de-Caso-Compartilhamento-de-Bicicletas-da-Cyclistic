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

![Gráfico de Duração da Viagem](link_da_imagem)

**Justificativa**: Este gráfico mostra claramente a diferença na duração média das viagens entre ciclistas casuais e membros anuais, o que ajuda a reforçar que os usuários casuais fazem viagens mais longas e esporádicas, enquanto os membros anuais utilizam as bicicletas para deslocamentos rápidos.

### Uso de Bicicletas por Dia da Semana

![Gráfico de Uso por Dia da Semana](link_da_imagem)

**Justificativa**: Esta visualização mostra a diferença de uso entre os dois grupos ao longo dos dias da semana, evidenciando que o pico de uso de ciclistas casuais é durante os finais de semana.

## Recomendações

Com base nos insights extraídos dos dados, as seguintes recomendações são propostas para maximizar o número de assinaturas anuais:

1. **Campanhas Focadas em Benefícios Diários**: Criar campanhas que mostrem como a assinatura anual pode beneficiar o ciclista casual no dia a dia, destacando economia e conveniência em viagens mais curtas.
   
2. **Promoções nos Finais de Semana**: Oferecer descontos ou benefícios exclusivos para ciclistas casuais que usarem a bicicleta nos finais de semana, incentivando-os a experimentar o uso regular durante a semana.

3. **Engajamento Digital**: Usar plataformas de mídia digital para mostrar depoimentos de ciclistas que se tornaram membros anuais, explicando como essa escolha melhorou seu deslocamento diário e ajudou a economizar dinheiro.

## Conclusão

Este estudo mostrou diferenças significativas no comportamento de uso entre ciclistas casuais e membros anuais da Cyclistic. Essas diferenças podem ser utilizadas para criar campanhas direcionadas que incentivem ciclistas casuais a se tornarem membros anuais, aumentando a lucratividade da empresa.

---

**Autor**: Augusto Barbosa 
**Data**: 20/09/24  
