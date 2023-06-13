<template>
  <div id="app">
    <BestTransport/>
    <div class="d-flex div-info-transporte container">
      <DivDestinoPeso/>

      <div class="div-info-transporte">
        <p>Estas são as melhores alternativas de frete que encontramos para você.</p>
        <div class="d-flex mt-0">
          <div class="div-info-transporte">
            <CartaoInfoFrete 
              :titulo="'Frete com o menor valor'" 
              :transportadora="'transportadora'" 
              :tempo="'tempo'" 
              :corDivImagem="'#bdd1d8'" 
              :corDivTexto="'#dedede'" 
              :imagem="'img-frete1.jpg'" 
            />
            <CartaoInfoFrete 
              :titulo="'Frete mais rápido'" 
              :transportadora="'transportadora'" 
              :tempo="'tempo'" 
              :corDivImagem="'#95b6c7'"
              :corDivTexto="'#ededec'" 
              :imagem="'img-frete2.jpg'" 
            />
          </div>
          <div class="div-info-transporte">
            <div class="div-info-preco" style="background-color: #dedede;">
              <h6>Preço</h6>
              <p>R$: </p>
            </div>
            <div class="div-info-preco" style="background-color: #ededec;">
              <h6>Preço</h6>
              <p>R$: </p>
            </div>
          </div>
        </div>
        <div class="d-flex justify-content-end">
        </div>
      </div>
      
    </div>
  </div>
</template>

<script>
import BestTransport from './components/BestTransport.vue'
import CartaoInfoFrete from './components/CartaoInfoFrete.vue';
import DivDestinoPeso from './components/DivDestinoPeso.vue';

export default {
  name: 'App',
  components: {
    BestTransport,
    DivDestinoPeso,
    CartaoInfoFrete
  }
}
</script>

<style>
.div-info-transporte > * {
  margin: 1rem 1rem 0 1rem;
}
.div-info-transporte{
  margin: auto;
}
.div-info-preco {
  padding: 0.75rem 1.7rem;
  margin-left: 0rem;
  height: 6rem;
  border-radius: 0.5rem;
}
p {
  max-width: 20rem;
}
</style>
