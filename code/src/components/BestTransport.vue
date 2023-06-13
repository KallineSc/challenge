<template>
  <div>
    <div class="title">
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand class="ml-2">
          <b>{{ appName }}</b>
        </b-navbar-brand>
      </b-navbar>
    </div>
    <b-form ref="formulario" @submit.prevent="onSubmit" @reset="onReset" v-if="show">
      <div class="d-flex m container">
        <DivDestinoPeso ref="divDestinoPeso"/>

        <div class="m-auto" v-if="exibirComponente">
          <p class="my-0 mx-3">Estas são as melhores alternativas de frete que encontramos para você.</p>
          <div class="d-flex">
            <div class="m">
              <CartaoInfoFrete 
                :titulo="'Frete com o menor valor'" 
                :transportadora="transportadoraFretePrecoMenor" 
                :tempo="tempoFretePrecoMenor" 
                :corDivImagem="'#bdd1d8'" 
                :corDivTexto="'#dedede'" 
                :imagem="'img-frete1.jpg'" 
              />
              <CartaoInfoFrete 
                :titulo="'Frete mais rápido'" 
                :transportadora="transportadoraFreteMaisRapido" 
                :tempo="tempoFreteMaisRapido" 
                :corDivImagem="'#95b6c7'"
                :corDivTexto="'#ededec'" 
                :imagem="'img-frete2.jpg'" 
              />
            </div>
            <div class="m">
              <div class="div-info-preco" style="background-color: #dedede;">
                <h6>Preço</h6>
                <p>R$: {{ fretePrecoMenor }}</p>
              </div>
              <div class="div-info-preco" style="background-color: #ededec;">
                <h6>Preço</h6>
                <p>R$: {{ fretePrecoMaisRapido }}</p>
              </div>
            </div>
          </div>
          <div class="d-flex justify-content-end">
            <BotaoGenerico titulo="Limpar" type="reset"/>
          </div>
        </div>

        <div class="m-auto" v-else>
          <h5 class="text-muted">Nenhum dado selecionado.</h5>
        </div>
        
      </div>
    </b-form>
  </div>
</template>

<script>
import CartaoInfoFrete from '../components/CartaoInfoFrete.vue';
import DivDestinoPeso from '../components/DivDestinoPeso.vue';
import BotaoGenerico from '../components/BotaoGenerico.vue';
import Swal from 'sweetalert2';
import axios from 'axios';

import {
  BNavbar,
  BNavbarBrand,
} from 'bootstrap-vue'

export default {
  components: {
    DivDestinoPeso,
    CartaoInfoFrete,
    BotaoGenerico,
    BNavbar,
    BNavbarBrand,
  },
  data() {
    return {
      appName: '',
      form: {
        peso: '',
        destino: null,
      },
      fretePrecoMenor: '',
      fretePrecoMaisRapido: '',
      transportadoraFretePrecoMenor: '',
      tempoFretePrecoMenor: '',
      transportadoraFreteMaisRapido: '',
      tempoFreteMaisRapido: '',
      exibirComponente: false,
      options: [],
      show: true
    }
  },
  created() {
   
    this.appName = 'Melhor Frete'
  },
  methods: {
    async getData() {
      try {
        const response = await axios.get("http://localhost:3000/transport");
        this.data = response.data;
      } catch (error) {
        console.log(error);
      }
    },
    async calcularFreteMenorPreco() {
      await this.getData();

      const destino = this.form.destino;
      const peso = this.form.peso;

      let menorValor = null;
      const response = this.data;

      for (const key in response) {
        if (Object.prototype.hasOwnProperty.call(response, key)) {
          const element = response[key];
          if (element.city === destino) {
            let valor;
            if (peso >= 700) {
              valor = parseFloat(element.cost_transport_heavy.replace("R$", "").replace(",", "."));
            } else {
              valor = parseFloat(element.cost_transport_light.replace("R$", "").replace(",", "."));
            }

            const preco = peso * valor;

            if (menorValor === null || preco < menorValor) {
              menorValor = preco;
              this.transportadoraFretePrecoMenor = element.name;
              this.tempoFretePrecoMenor = element.lead_time;
            }
          }
        }
      }

      this.fretePrecoMenor = menorValor.toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: 2 });

    },
    async calcularFreteMaisRapido() {
      await this.getData();

      const destino = this.form.destino;
      const peso = this.form.peso;

      let maisRapido = null;
      const response = this.data;

      for (const key in response) {
        if (Object.prototype.hasOwnProperty.call(response, key)) {
          const element = response[key];
          if (element.city === destino) {
            let valor;
            if (peso >= 700) {
              valor = parseFloat(element.cost_transport_heavy.replace("R$", "").replace(",", "."));
            } else {
              valor = parseFloat(element.cost_transport_light.replace("R$", "").replace(",", "."));
            }

            let preco = '';

            const tempoString = element.lead_time;
            const tempo = parseInt(tempoString.replace("h", ""), 10);

            if (maisRapido === null || tempo < maisRapido) {
              maisRapido = tempo;
              this.transportadoraFreteMaisRapido = element.name;
              this.tempoFreteMaisRapido = element.lead_time;
              preco = peso * valor;
              this.fretePrecoMaisRapido = preco.toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
            }
            
          }
        }
      }

      

    },
    onSubmit() {
      const destino = this.$refs.divDestinoPeso.form.destino;
      const peso = this.$refs.divDestinoPeso.form.peso;
      this.form.peso = peso;
      this.form.destino = destino;
      if (peso && destino != null) {
        this.$nextTick(() => {
          this.exibirComponente = true;
          this.calcularFreteMenorPreco();
          this.calcularFreteMaisRapido();
        });
      } else {
        this.$nextTick(() => {
          Swal.fire({
            text: 'Insira os valores para realizar a análise.',
            icon: 'warning',
            iconColor: '#34626a',
            showCloseButton: false,
            showCancelButton: false,
            showConfirmButton: true,
            confirmButtonText: 'Fechar',
            confirmButtonColor: '#93b6c5',
            color: '#313131',
          });
        });
      }
    },
    onReset(event) {
      event.preventDefault()
      this.form.peso = ''
      this.form.destino = null
      this.exibirComponente = false
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  },
}
</script>

<style scoped>
.title .navbar {
  background-color: #95b6c7 !important;
  color: #313131;
}

.title .navbar-brand {

  color: #313131;
  margin-left: 20px;
}
.m > * {
  margin: 1rem 0 1rem 1rem;
}
.div-info-preco {
  padding: 0.75rem 1.7rem;
  height: 6rem;
  border-radius: 0.5rem;
}
p {
  max-width: 20rem;
}
</style>
