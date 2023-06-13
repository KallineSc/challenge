<template>
  
    <div class="div-externa">
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
            type="number"
            placeholder="Peso da carga em kg"
          ></b-form-input>
        </b-form-group>

        <div class="d-flex justify-content-center">
          <BotaoGenerico titulo="Analisar" type="submit"/>
        </div>
    </div>
  </template>
  <script>
  import axios from 'axios';
  import BotaoGenerico from './BotaoGenerico.vue';

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
        getTransports(){
          axios
            .get("http://localhost:3000/transport")
            .then((res) => {
              this.options = res.data;
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