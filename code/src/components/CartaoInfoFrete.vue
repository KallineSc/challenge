<template>
  <div class="div-externa d-flex">
    <div class="div-imagem" :style="{ backgroundColor: corDivImagem }"><img :src="require('@/assets/' + imagem + '')" alt=""></div>
    <div class="div-texto" :style="{ backgroundColor: corDivTexto }">
      <h6>{{ titulo }}</h6>
      <p>Transportadora: {{ transportadora }}</p>
      <p>Tempo estimado: {{ tempo }}</p>
    </div>
    
  </div>
</template>
  <script>

    export default {
      props: {
        imagem: {
          type: String,
          required: true
        },
        titulo: {
          type: String,
          required: true
        }, 
        transportadora: {
          type: String,
          required: true
        },
        tempo: {
          type: String,
          required: true
        },
        corDivImagem: {
          type: String,
          required: true
        },
        corDivTexto: {
          type: String,
          required: true
        },
      },
      components: {
      },
      data() {
        return {
          show: true
        }
      },
      created() {
      },
      methods: {
      }
    }
  </script>

  <style scoped>
  .div-externa {
    margin-left: 0rem;
    height: 6rem;
    border-radius: 0.5rem;
  }
  .div-imagem {
    width: 5rem;
    border-top-left-radius: 0.5rem;
    border-bottom-left-radius: 0.5rem;
    display: flex;
    align-items: center; 
    justify-content: center;
  }
  .div-texto {
    width: 22rem;
    padding: 0.75rem 1.7rem;
    border-top-right-radius: 0.5rem;
    border-bottom-right-radius: 0.5rem;
  }
  .img{
    width: 3rem;
    height: 3rem;
    margin-right: 1rem;
  }
  p, h6 {
    margin: 0rem;
  }
  </style>