<template>
  <span ref="integerGrow">{{showVal}}</span>
</template>

<script>
export default {
  name: 'IntegerGrow',
  props: {
    value: {
      type:Number,
      default:0
    },
    floatNum:{
      type:Boolean,//是否显示三位加逗号
      default:false
    },
    time:{//时间，数字滚动的快慢
      type:Number,
      default:3
    }
  },
  data () {
    return {
      growTimer: null,
      showVal:0
    }
  },
  watch: {
    value : {
      handler : function(obj){
        window.clearInterval(this.growTimer);
        this.showVal = 0;
        this.numberGrow();
      },
      deep : true
    },
    time : {
      handler : function(obj){},
      deep : true
    }
  },
  created(){},
  mounted(){
    this.numberGrow();
  },
  methods:{
    numberGrow(ele){
      // 判断是否非数字
      if(!isNaN(ele)){
        this.showVal = ele;
        return;
      }
      // 如果传入值是0，直接展示
      if(this.value == 0){
        this.showVal = 0;
        return;
      }
      // 判断是否有小数点
      let isFloat = false;
      if(this.value.toString().indexOf('.') !== -1){
        isFloat = true;
      }
      let that = this;
      let step = (this.value*10)/500;
      let current = 0,start = 0;
      this.growTimer = window.setInterval(()=>{
        start +=step;
        if(start > this.value){
          window.clearInterval(this.growTimer);
          start = this.value;
          this.growTimer = null;
        }
        if(current == start)return;
        current = start;
        let returnVal = isFloat ? current.toFixed(1) : parseInt(current);
        this.showVal = !this.floatNum ? returnVal : returnVal.toString().replace(/(\d)(?=(?:\d{3}[+]?)+$)/g,'$1,');
      },this.time)
    }
  },
  beforeDestroy(){
    window.clearInterval(this.growTimer)
  }
}
</script>
<style scoped>

</style>
