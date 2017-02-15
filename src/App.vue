<template>
  <div id="app">
     <ul id="demo">
      <item
        class="item"
        :model="data">
      </item>
    </ul>

  </div>
</template>

<script>
import Item from './components/item.vue'
export default {
  name: 'app',
  data (){
    return {
      data:{
        name: 'My Tree',
        isSelect: false,
        children: [
          { name: 'hello',isSelect: true },
          { name: 'wat',isSelect: false },
          {
            name: 'child folder',
            isSelect: false,
            children: [
              {
                name: 'child folder777',
                isSelect: false,
                children: [
                  { name: 'hello' ,isSelect: false},
                  { name: 'wat' ,isSelect: false}
                ]
              },
              { name: 'hello' ,isSelect: false},
              { name: 'wat',isSelect: false },
              {
                name: 'child folder666',
                isSelect: false,
                children: [
                  { name: 'hello',isSelect: false },
                  { name: 'wat',isSelect: false }
                ]
              }
            ]
          }
        ]
      }
    }
  },
  watch :{
    data: {
      handler:function(val,oldVal){
        console.log(oldVal)
      },
      deep:true
    }
  },
  methods:{
     
  },
  components:{
    Item
  }
}

</script>

 
