<template>

    <div class="div-externa">
      <b-form ref="formulario" @submit.prevent="onSubmit" @reset="onReset" v-if="show">
        <div class="d-flex">
          <img class="img" src="../assets/img-frete3.jpg" alt="Responsive image">
          <h4 class="my-0 mt-2">Insira o destino e o peso</h4>
        </div>
  
        <b-form-group class="mt-3 label" id="input-group-1" label="Destino:" label-for="input-1">
          <b-form-select class="form-control mt-2"
            id="input-1"
            v-model="form.destino"
          >
          <option class="option" v-for="option in options" :key="option.id" :value="option.city">
            {{ option.city }}
          </option>
          </b-form-select>
        </b-form-group>

        <b-form-group class="mt-3 label" id="input-group-2" label="Peso:" label-for="input-2">
          <b-form-input  class="mt-2"
            id="input-2"
            v-model="form.peso"
            placeholder="Peso da carga em kg"
          ></b-form-input>
        </b-form-group>

        <div class="d-flex justify-content-center">
          <BotaoGenerico titulo="Analisar" type="submit"/>
          <BotaoGenerico titulo="Limpar" type="reset"/>
        </div>

      </b-form>
    </div>
  </template>
  <script>
  import axios from 'axios';
  import BotaoGenerico from './BotaoGenerico.vue';
  import Swal from 'sweetalert2';

    export default {
      components: {
        BotaoGenerico
      },
      data() {
        return {
          form: {
            peso: '',
            destino: null,
          },
          options: [],
          show: true
        }
      },
      created() {
        this.getTransports();
      },
      methods: {
        onSubmit() {
          if (this.form.peso && this.form.destino != null) {
            this.$nextTick(() => {

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
          this.show = false
          this.$nextTick(() => {
            this.show = true
          })
        },
        getTransports(){
          axios
            .get("http://localhost:3000/transport")
            .then((res) => {
              this.options = res.data;
              console.log(res.data)
            })
            .catch((error) => {
              console.log(error);
            });

        }
      }
    }
  </script>

  <style scoped>

  .label {
    color: #313131;
    font-weight: bolder;
  }
  .div-externa {
    padding: 4rem 2rem;
    max-width: 25rem;
    height: 31rem;
    background-color: #f2f2f2 !important;
    border-radius: 0.5rem;
  }
  .option {
    width: 10px;
  }
  .img{
    width: 3rem;
    height: 3rem;
    margin-right: 1rem;
  }
  </style>