<template>
  <div class="home">
    <h1>Números da Covid no Brasil</h1>

    <section>
      <div class="data-container">
        <div class="vertical-container">
          <h3>Total de casos</h3>
          <p>
            {{
              info &&
              new Intl.NumberFormat("pt-BR").format(info.confirmados.total)
            }}
          </p>
        </div>

        <div class="vertical-container">
          <h3>Total de óbitos</h3>
          <p>
            {{
              info && new Intl.NumberFormat("pt-BR").format(info.obitos.total)
            }}
          </p>
        </div>

        <div class="vertical-container">
          <h3>Casos novos</h3>
          <p>
            {{
              info && new Intl.NumberFormat("pt-BR").format(info.confirmados.novos)
            }}
          </p>
        </div>

        <div class="vertical-container">
          <h3>Óbitos novos</h3>
          <p>
            {{
              info && new Intl.NumberFormat("pt-BR").format(info.obitos.novos)
            }}
          </p>
        </div>
      </div>

      <div class="chart-container">
        <AcumulatedCasesChart />
        <AcumulatedDeathsChart />
      </div>

      <h4>Selecione a UF</h4>
      <select v-model="selectedUf">
        <option v-for="(item, key) in infoState" :value="item._id" :key="key">
          {{ item._id }}
        </option>
      </select>
      <p>Selecionado {{ selectedUf }}</p>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import AcumulatedCasesChart from "./AcumulatedCasesChart";
import AcumulatedDeathsChart from "./AcumulatedDeathsChart";

export default {
  name: "Home",
  components: {
    AcumulatedCasesChart,
    AcumulatedDeathsChart,
  },
  data() {
    return {
      info: null,
      infoState: null,
      selectedUf: "",
      loading: true,
      errored: false,
    };
  },
  mounted() {
    console.log("oiini");
    axios
      .get(
        "https://xx9p7hp1p7.execute-api.us-east-1.amazonaws.com/prod/PortalGeralApi"
      )
      .then((response) => {
        this.info = response.data;
        console.log(response);
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));

    axios
      .get(
        "https://xx9p7hp1p7.execute-api.us-east-1.amazonaws.com/prod/PortalEstadoRegiao"
      )
      .then((response) => {
        this.infoState = response.data;
        console.log(response);
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.data-container {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

.vertical-container {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  margin: 1rem 0;
  width: 10rem;
  height: 5rem;
  border-radius: 40px;
  border-radius: 34px;
  background: #23897f;
  font-size: 18px;
  padding: 0.5rem;
  color: #fff;
  box-shadow: 10px 10px 31px #e7e6e6, -10px -10px 31px #ffffff;
}

h4 {
  color: #2c3e50;
  font-size: 20px;
}

select,
option {
  font-size: 20px;
  margin: 0;
}

.chart-container {
  display: flex;
  justify-content: space-evenly;
  margin: 1rem;
  padding: 1rem;
}
</style>
