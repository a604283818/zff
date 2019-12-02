<template>
  <div class="hello">
    <IntegerGrow :value='num' :time='20'></IntegerGrow>
  </div>
</template>

<script>
import IntegerGrow from '@/components/IntegerGrow'
export default {
  name: 'HelloWorld',
  components: {
    IntegerGrow
  },
  data () {
    return {
      num:678
    }
  }
}
</script>
<style scoped>

</style>
