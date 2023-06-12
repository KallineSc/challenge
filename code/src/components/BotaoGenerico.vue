  <template>
    <button class=" button-submit mt-5" :type="type" >{{titulo}}</button>
  </template>
    
  <script>
    export default {
      props: {
        titulo: String,
        type: String
      }
    }
  </script>

  <style scoped>
  .button-submit {
    color: #313131;
    font-weight: bolder;
    border-style: solid;
    width: 180px;
    height: 35px;
    border-color: #93b6c5;
    border-radius: 0.3rem;
    background-color: #93b6c5;
  }
  </style>