<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button :disabled="isActive" type="button" @click="sdk.open()">liveness</button>
    <p>{{error}}</p>
    <p>{{ result.sessionId }}</p>
    <img :src="`data:image/png;base64,${result.image}`"/>
  </div>
</template>

<script setup lang="ts">
import * as CSLiveness from '@studio/csliveness';
let msg = "Click Abaixo para iniciar."
let isActive = false
let error = ""
let result = {"sessionId": "", image: ""}

let sdk = new CSLiveness.Instance("smu-investimentos",
                                   "kzmgUVbw1HmDLuktW0vsFZudY7IinbrY",
                                   '/dist/core-sdk')

sdk.on('onReady', () => {
   console.log("Ready")
   isActive = true
})

sdk.on('onCompleted', (successResult: object) => {
    //Neste callback será enviado a imagem capturada e o sessionId 
    //que deverá ser armazenado para futura consulta da imagem capturada.
    console.log(successResult)
    result = successResult
})
sdk.on('onError', (tipo: string) => {
    error = tipo
})

sdk.initialize()
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
