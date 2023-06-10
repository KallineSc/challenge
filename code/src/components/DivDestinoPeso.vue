<template>

    <div class="div-externa">
      <b-form @submit="onSubmit" @reset="onReset" v-if="show">
        <div class="d-flex justify-content-start">
          <b-img src="../assets/logo.png" alt="Responsive image"></b-img>
          <h3>Insira o destino e o preço</h3>
        </div>
  
        <b-form-group class="mt-3" id="input-group-1" label="Destino:" label-for="input-1">
            <b-form-select class="form-control"
                id="input-1"
                v-model="form.destino"
                :options="options"
                required
            ></b-form-select>
        </b-form-group>

        <b-form-group class="mt-3" id="input-group-2" label="Peso:" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="form.peso"
            placeholder="Peso da carga em kg"
            required
          ></b-form-input>
        </b-form-group>
        <div class="d-flex justify-content-center">
          <ButtonGenerico titulo="Analisar" type="submit"/>
        </div>

      </b-form>

    </div>
  </template>
  
  <script>
  import ButtonGenerico from './ButtonGenerico.vue';

    export default {
      components: {
        ButtonGenerico
      },
      data() {
        return {
          form: {
            peso: '',
            destino: null,
          },
          options: [
            { text: 'Selecione o destino', value: null }, 
            'Carrots', 
            'Beans', 
            'Tomatoes', 
            'Corn'
          ],
          show: true
        }
      },
      methods: {
        onSubmit(event) {
          event.preventDefault()
          alert(JSON.stringify(this.form))
        },
        onReset(event) {
          event.preventDefault()
          // Reset our form values
          this.form.peso = ''
          this.form.destino = null
          // Trick to reset/clear native browser form validation state
          this.show = false
          this.$nextTick(() => {
            this.show = true
          })
        }
      }
    }
  </script>

  <style scoped>
  .div-externa {
    max-width: 30rem;
    height: 35rem;
    padding: 2rem;
    background-color: #f2f2f2 !important;
    border-radius: 0.5rem;
  }
  /* color: #7e7e80; */
  /* #93b6c5 */
  .d-block {
    color: pink;
  }
  .button-submit {
    background-color: #93b6c5;
  }
  </style>