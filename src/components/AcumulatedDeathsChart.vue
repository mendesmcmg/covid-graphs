<script>
import { Line } from "vue-chartjs";
import axios from "axios";

export default {
  extends: Line,
  mounted() {
    axios
      .get(
        "https://xx9p7hp1p7.execute-api.us-east-1.amazonaws.com/prod/PortalCasos"
      )
      .then((response) => {
        console.log(response);
        this.renderChart(
        {
            labels: response.data.semana.map((d, i)=> i),
            datasets: [
            {
                label: "Óbitos Acumulados",
                data: response.data.semana.map((d)=> d.obitosAcumulado),
                backgroundColor: "transparent",
                borderColor: "rgba(1, 116, 188, 0.50)",
                pointBackgroundColor: "rgba(171, 71, 188, 1)"
            }
            ]
        },
        {
            responsive: true,
            maintainAspectRatio: false,
            title: {
            display: true,
            text: "Óbitos Acumulados"
            }
        }
        );
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  }
}
</script>