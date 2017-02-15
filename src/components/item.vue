<template>
	<div id="item">
		<li>
		    <div>
			    <span @click="toggle2">
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
		      allSelect:[],
		      allSelect2:[]
		    }
		  },
		  computed: {
		    isFolder: function () {
		      return this.model.children 
		    }
		  },
		  methods: {
		  	xxx:function(object){
		  		let self = this
		  		object.isSelect = !object.isSelect
		    	if (object.children) {
		    		object.isSelect = !object.isSelect
		    		object.children.forEach(function(item,index){
		    			item.isSelect =  object.isSelect
		    			if(item.children){
		    				self.xxx(item)  
		    				return true;
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
		    toggle2:function(){   //选择功能
		    	let self = this
		    	self.model.isSelect = !self.model.isSelect
			    this.xxx(self.model) 
			    // self.allSelect=[]
			   //  if (self.isFolder) {
			   //  	let len = self.isFolder.length;
			   //  	self.isFolder.forEach(function(item,index){
			    		
			   //  		if (item.isSelect) {
			   //  			self.allSelect.push(item.isSelect)
			   //  		}
			   //  		self.model.isSelect ? len == self.allSelect.length : false
						// console.log(self.model.isSelect+':'+self.model.name) 
			   //  	})

			   //  }
			    
		    }
		  }
	}
</script>