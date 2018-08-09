<template>
 
      <input id="search" name="search" :class="{ dark }" :value="value" @input="handleChange"/>
    
</template>

<script>
export default {
  name: "SearchInput",
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    }
  }
};
</script>
<style lang="scss" scoped>
/*.searchWrapper {
  margin-top: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 250px;
}*/
input {
  margin-top: 50px;
  height: 30px;
  border: 0;
  border-bottom: 1px solid #fff;
  outline: none;
  background: none;
  color: #fff;
  text-align: center;
  font-size: 18px;
  font-weight: 300;
  &:focus {
    outline: none;
    box-shadow: 0 10x 20px -8px rgba(255,255,255, .5);
  }
}
.dark{
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;
   &:focus {
    outline: none;
    box-shadow: 0 10x 20px -8px rgba(#1e3d4a, 0.5);
  }
}
</style>
