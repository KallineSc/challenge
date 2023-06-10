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
    border-style: solid;
    width: 180px;
    height: 35px;
    color: black;
    border-color: #79919b;
    border-radius: 0.3rem;
    background-color: #93b6c5;
  }
  </style>