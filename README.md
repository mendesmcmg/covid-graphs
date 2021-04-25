# :chart_with_upwards_trend: covid-graphs

## :page_with_curl: Descrição
Projeto desenvolvido usando Vue.js para apresentar gráficos sobre os números de Covid no Brasil. Por não possuir a possibilidade de dedicar muito tempo ao desenvolvimento de uma API no back-end, as requisições foram feitas no front diretamente para API's externas. 

## :books: Bibliotecas utilizadas
Para a construção dos gráficos, foram utilizadas as bibliotecas [Chart.js](https://www.chartjs.org) e [vue-chartjs](https://vue-chartjs.org).

## :game_die: API's utilizadas
[Dados gerais] (https://xx9p7hp1p7.execute-api.us-east-1.amazonaws.com/prod/PortalGeralApi)
[Dados estaduais] (https://xx9p7hp1p7.execute-api.us-east-1.amazonaws.com/prod/PortalEstadoRegiao)
[Dados temporais] (https://xx9p7hp1p7.execute-api.us-east-1.amazonaws.com/prod/PortalCasos)

## :wrench: Configuração do Projeto

```
yarn install
```

### Compila e faz hot-reloads para desenvolvimento
```
yarn serve
```

### Compila e minimiza para produção
```
yarn build
```

### Encarrega lint e conserta arquivos
```
yarn lint
```

### Customizar configurações
Ver [Configuration Reference](https://cli.vuejs.org/config/).
