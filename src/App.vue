<template>
  <div class="container flex mx-auto h-screen pt-9 pr-4 pl-4">

    <div class="w-80 bg-white">
    
      <div class="flex items-center bg-[#EDEDED] h-14 pl-6"></div>
    
      <div 
        v-for="(conversa, index) in conversas"
        v-on:click="indiceAtivo = index"
        class="py-4 px-8 border-b border-[#F2F2F2] hover:bg-[#F5F5F5] cursor-pointer" 
        v-bind:key="index"
        >
    
        <div> {{ conversa.usuario }}</div>
    
        <div>Ultima mensagem...</div>
    
      </div>
    </div>
    
    <div class="flex-1 bg-[#E5DDD5] flex flex-col">
    
      <div class="flex items-center bg-[#EDEDED] border-l-2 border-[#E1E1E1] h-14 pl-6">
    
        <span>{{ conversas[indiceAtivo].usuario }}</span>
    
      </div>

      <div class="flex-1 flex flex-col justify-end">
    
        <MensagemUsuario
          v-for="(mensagem, index) in conversas[indiceAtivo].mensagens"
          :conteudo="mensagem.conteudo"
          :horario="mensagem.horario"
          :verde="mensagem.verde"
          v-bind:key="index"
        />
    
      </div>

      <div class="p-3 bg-[#f0f0f0]">
    
        <input 
          v-model="conteudoNovaMensagem"
          v-on:keyup.enter="enviarMensagem"
          type="text" 
          placeholder="Insira sua mensagem"
          class="input w-full text-base rounded-xl p-2" 
          />
      
      </div>
    
    </div>
  
  </div>
</template>

<script>    
  import conversasIniciais from "./data/dados.js";
  
  import MensagemUsuario from "./components/MensagemUsuario.vue";
  
  export default {
    data: function(){
      return {
        conversas: conversasIniciais,
        indiceAtivo: 0,
        conteudoNovaMensagem: ""
      }
    },
    components: {
      MensagemUsuario
    },
    methods:{
      enviarMensagem: function(){
        let horarioAtual = new Date().getHours() + ":" + new Date().getMinutes();

        let novaMensagem = {
          horario: horarioAtual,
          conteudo: this.conteudoNovaMensagem,
          verde: true
        };

        this.conversas[this.indiceAtivo]
          .mensagens
          .push(novaMensagem)

        this.conteudoNovaMensagem = ""
      } 
    }
  }

</script>