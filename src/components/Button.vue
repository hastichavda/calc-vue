<template>
  <div>
    <div class="btn" @click="onClick(val)">{{val}}</div>
  </div>
</template>

<script>
export default {
  props:['val'],
  data () {
  },
  methods: {
    onClick (val) {
      this.$emit('append', val)
    }
  }
}
</script>
<style> 
.btn {
            background-color: #F2F2F2;
            border: 1px solid #999;
     }

</style>
 