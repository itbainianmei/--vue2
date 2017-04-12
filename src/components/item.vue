<template>
	<div  >
		<li>
		    <div>
			    <span class="icon-box" @click="choose">
			    	<img v-if="model.isSelect" src="../../static/images/selected.png" height="14" width="18" alt="">
			    	<img v-if="!model.isSelect" src="../../static/images/del.png" height="14" width="18" alt="">
			    </span>
			    {{model.name}}
		        <span v-if="isFolder" @click="toggle">[{{open ? '-' : '+'}}]</span>
		    </div>
		    <ul v-show="open" v-if="isFolder">
		      <item
		        v-for="item in model.children"
		        :model="item" :parent="model" @check="check">
		      </item>
		    </ul>
		</li>
	</div>
</template>
<script>
	export default {
		name:'item',
		props: {
		    model: Object,
		    parent:Object
		 },
		 data: function () {
		    return {
		      open: false,
		      allSelect:[]
		    }
		  },
		  computed: {
		    isFolder: function () {
		      return this.model.children && this.model.children.length
		    }
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
		  	check:function(){
		  		let self = this
		  		if (this.parent) { 
			    	var flag = this.parent.children.some((value,i) => {
			    		return value.isSelect === false
			    	})
			    	if (flag) {
			    		this.parent.isSelect = false
			    	}else{
			    		this.parent.isSelect = true
			    	}
			    }
			    this.$emit('check') 
		  	},
		  	checkChild:function(data,flag){
		  		let self = this
		  		data.children.forEach(function(value,i){
		  			value.isSelect = flag
		  			if (value.children && value.children.length) {
		  				self.checkChild(value,flag)
		  			}
		  		})
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
			    self.check()   //子级->父级
			    // if (self.isFolder) {
			    // 	self.checkChild(self.model,self.model.isSelect)
			    // }
		    }
		  }
	}
</script>
