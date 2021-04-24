<template>
  <div class="home">
    <h1>Covid Graphs</h1>
    <p>Esta é uma página para mostrar dados de COVID-19 no Brasil</p>

    <section>
      <div class="data-container">
        <div class="vertical-container">
          <h3>Total de casos</h3>
          <p>{{ info && info.confirmados.total }}</p>
        </div>

        <div class="vertical-container">
          <h3>Total de óbitos</h3>
          <p>{{ info && info.obitos.total }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      info: null,
      loading: true,
      errored: false,
    };
  },
  mounted() {
    console.log("a");
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
  margin-top: 2rem;
  width: 15rem;
  border-radius: 40px;
  border-radius: 34px;
  background: #f8f7f7;
  box-shadow: 10px 10px 31px #e7e6e6, -10px -10px 31px #ffffff;
}
</style>
