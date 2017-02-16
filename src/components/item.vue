<template>
	<div id="item">
		<li>
		    <div>
			    <span @click="choose">
			    	<img v-if="model.isSelect" src="../../static/images/selected.png" height="14" width="18" alt="">
			    	<img v-if="!model.isSelect" src="../../static/images/del.png" height="14" width="18" alt="">
			    </span>
			    {{model.name}}
		        <span v-if="isFolder" @click="toggle">[{{open ? '-' : '+'}}]</span>
		    </div>
		    <ul v-show="open" v-if="isFolder">
		      <item
		        class="item"
		        v-for="model in model.children"
		        :model="model">
		      </item>
		    </ul>
		  </li>
	</div>
</template>
<script>
	export default {
		name:'item',
		props: {
		    model: Object
		 },
		 data: function () {
		    return {
		      open: false,
		      allSelect:[]
		    }
		  },
		  computed: {
		    isFolder: function () {
		      return this.model.children 
		    }
		  },
		  watch:{
		  	
		  },
		  methods: {
		  	isChoose:function(object){
		  		let self = this
		  		object.isSelect = !object.isSelect
		    	if (object.children) {
		    		object.isSelect = !object.isSelect
		    		object.children.forEach(function(item,index){
		    			item.isSelect =  object.isSelect
		    			if(item.children){
		    				self.isChoose(item)  
		    				return true
		    			}
		    		})
			    }else{
		  			object.isSelect = !object.isSelect
			    	return true
			    }
		  	},
		    toggle: function () {   //右侧是否收缩展示
		      if (this.isFolder) {
		        this.open = !this.open
		      }
		    },
		    choose:function(){   //选择功能
		    	let self = this
		    	self.model.isSelect = !self.model.isSelect
			    this.isChoose(self.model)
		    }
		  }
	}
</script>
