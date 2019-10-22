<template>
  <div
    class="select-component"
    @mouseleave="inputChange('close')"
  >
    <label
      :for="className+'_input'"
      :class="{'focus' : inputActive}"
    >{{ label }}</label>
    <input
      :id="className+'_input'"
      v-model="valueInput"
      :name="className+'_input'"
      type="text"
      :placeholder="placeholder"
      @click="inputChange('open')"
    >
    <ul :class="{'active': inputActive}">
      <li v-if="!searchValue(options).length">
        {{ emptyMessage }}
      </li>
      <li
        v-for="opt in searchValue(options)"
        :key="opt"
      >
        <button>{{ opt }}</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Select',
  props: {
    placeholder: {
      type: String,
      default: 'Digite...'
    },
    name: {
      type: String,
      default: 'inputSelect'
    },
    label: {
      type: String,
      default: 'Input Label'
    },
    emptyMessage: {
      type: String,
      default: 'Ops.. Parece que você não tem essa opção'
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  data: () => {
    return {
      className: '',
      inputActive: false,
      valueInput: ''
    }
  },
  watch: {
    valueInput (e) {
      this.inputChange('change')
      this.$emit('input', e)
    }
  },
  mounted () {
    this.hash(this.name)
  },
  methods: {
    hash (string) {
      let hash = 0
      for (let i = 0; i < string.length; i++) {
        let char = string.charCodeAt(i)
        hash = ((hash << 5) - hash) + char
        hash = hash & hash
      }
      this.className = this.name + '_' + Math.abs(hash)
    },
    inputChange (event) {
      if (event === 'open') {
        if (!this.inputActive) this.inputActive = true
      }
      if (event === 'close') {
        if (!this.valueInput) this.inputActive = false
      }
    },
    searchValue (options) {
      var app = this
      return options.filter((preset) => {
        return preset.toLowerCase().indexOf(app.valueInput.toLowerCase()) > -1
      })
    }
  }
}
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Nunito:200,200i,300,300i,400,400i,600,600i,700,700i,800,800i,900,900i&display=swap');
$family: 'Nunito', sans-serif;
$color-principal: #f44336;
$color-secundario: #000000;
$color-simples: #999999;
.select-component{
  position: relative; padding: 10px 0;
  *{transition: ease-in .2s;}
  label{
    text-align: left; position: absolute; top: 35px; left: 15px; transform: scale(1) translate(0px, -50%); transition: ease-in .2s; padding: 0 10px; margin: 0;
    &.focus{top: 10px; transform: scale(.8) translate(0px, -50%); background: #ffffff; transition: ease-in .2s; transform-origin: 0 0;}
  }
  input{
    width: 100%; height: 48px; line-height: 48px; padding: 0 20px; border: 2px solid $color-simples; border-radius: 5px; outline: none; display: block;
    &::placeholder{color: transparent;}
  }
  ul{
    background: #FFFFFF; border: 2px solid $color-simples; position: absolute; width: 100%; border-radius: 5px; margin: 0; padding:0; top: 0; opacity: 0; pointer-events: none;
    &.active{top: 56px; opacity: 1; pointer-events: auto;}
    li{
      list-style: none; margin: 0; padding: 0; display: block;
      button{
        display: block; width: 100%; padding: 0 20px; text-align: left; line-height: 35px; height: 35px; background: #FFFFFF; outline: none; border: 0;
        &:focus, &:hover{background: #eeeeee;}
      }
    }
  }
}
</style>
