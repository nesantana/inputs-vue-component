<template>
  <div class="text-area-component">
    <label
      :for="className+'_input'"
      :class="{'focus' : inputActive}"
    >{{ label }}</label>
    <textarea
      :id="className+'_input'"
      v-model="valueInput"
      :name="className+'_input'"
      type="text"
      :placeholder="placeholder"
      @focus="inputChange($event.type)"
      @blur="inputChange($event.type)"
    />
  </div>
</template>

<script>
export default {
  name: 'TextArea',
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
      if (event === 'focus') {
        if (!this.inputActive) this.inputActive = true
      }
      if (event === 'blur') {
        if (!this.valueInput) this.inputActive = false
      }
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
.text-area-component{
  position: relative; padding: 10px 0; margin: 0;
  *{transition: ease-in .2s; margin: 0;}
  label{
    text-align: left; position: absolute; top: 20px; left: 15px; transform: scale(1) translate(0px, 0px); padding: 0 10px; margin: 0;
    &.focus{top: 10px; transform: scale(.8) translate(0px, -50%); background: #ffffff; transform-origin: 0 0;}
  }
  textarea{
    width: 100%; height: 150px; line-height: 140%; padding: 20px; border: 2px solid $color-simples; border-radius: 5px; outline: none; display: block;
    &::placeholder{font: normal 15px $family; color: transparent; transition: ease-in .2s;}
    &:focus::placeholder{color: $color-simples;}
  }
}
</style>
