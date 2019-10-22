<template>
  <div class="home">
    <div class="container">
      <div class="col-lg-6 col-md-12 offset-md-3">
        <div class="mt60" />
        <input-component
          v-model="nome"
          name="nome"
          placeholder="Preencha com seu ome completo"
          label="Component de input simples"
        />
        <text-area-component
          v-model="mensagem"
          name="mensagem"
          placeholder="Preencha com seu ome completo"
          label="Component de input simples"
        />
        <select-component
          v-model="assunto"
          name="assunto"
          placeholder="Preencha com seu ome completo"
          label="Component de input simples"
          empty-message="Eita... Parece que não temos essa opção"
          :options="assuntos"
        />
      </div>
    </div>
  </div>
</template>

<script>
import InputComponent from '@/components/InputComponent.vue'
import TextAreaComponent from '@/components/TextAreaComponent.vue'
import SelectComponent from '@/components/SelectComponent.vue'

export default {
  name: 'Home',
  components: {
    InputComponent,
    TextAreaComponent,
    SelectComponent
  },
  data: () => {
    return {
      nome: '',
      mensagem: '',
      assunto: '',
      assuntos: ['Assunto 01', 'Assunto 02', 'Assunto 03', 'Assunto 04']
    }
  },
  watch: {
    nome (e) {
      console.log('nome', e)
    },
    mensagem (e) {
      console.log('mensagem', e)
    }
  }
}
</script>
