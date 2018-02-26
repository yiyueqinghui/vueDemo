<template>
	<div>
		<h3 class="header">计  划  表</h3>
    <h4>添加任务:</h4>
    <p><input type="text" placeholder="例如：吃饭睡觉打豆豆" class="addText" @keydown.enter="add"/></p>
    <p class="nav-list">
    	<span>{{num}}个未完成任务</span>
    	<span @click="tasked" >已完成任务</span>
    	<span @click="tasking">未完成任务</span>
    	<span @click="taskAll">所有任务</span>
    </p>
    <h4>任务列表: </h4>
		<div class="listOne" v-for="(item,index) in msg" v-if="item['show']">
      <input type="checkbox"  v-model="item.bol" />
      <a class="con" :class={red:item.bol}>{{item.txt}}{{item.bol}}</a>
      <span class="del" @click="del(index)">删除</span>
    </div>
	</div>
</template>

<script>
export default {
  name: 'listOne',
  data () {
    return {
      msg:[
   	  	  {txt:'aaaaaa',bol:false,show:true},
   	  	  {txt:'bbbbbbb',bol:false,show:true},
   	  	  {txt:'ccccccc',bol:false,show:true}
   	  	 ],
   	  num:0
   	  
    }
  },
  methods:{
  	add:function(e){
   	 	 var _this = e.target,
   	 	     txt = _this.value;
   	 	 this.msg.push({txt:txt,bol:false,show:true});
   	 	 _this.value = "";
   	 	 
   	},
   	del:function(id){
   	 	  this.msg.splice(id,1);
   	},
// 	未完成任务
   	tasking:function(e){
    	 var _this = e.target;
   		$(_this).css('background','lightgray');
   		$(_this).siblings().css("background","none");
   		for(var i in this.msg){
   			var bol = this.msg[i]['bol'];
   			this.msg[i]['show'] = !bol;
   		}
   	},
// 	已经完成的任务
   	tasked:function(e){
   		var _this = e.target;
   		$(_this).css('background','lightgray');
   		$(_this).siblings().css("background","none");
   		for(var i in this.msg){
   			var bol = this.msg[i]['bol'];
   			this.msg[i]['show'] = bol;
   		}
   	},
   	taskAll:function(e){
   		var _this = e.target;
   		$(_this).css('background','lightgray');
   		$(_this).siblings().css("background","none");
   		for(var i in this.msg){
   			this.msg[i]['show'] = true;
   		}
   	}
   	
  },
  watch:{
//	深度监听
  	msg:{
//		vue 多操作数据,以数据控制dom结构,不要一味地去寻找dom节点,进行节点操作
  		handler:function(oldval,newval){
  			var nums = newval.length;
  			console.log(nums);
  			console.log(newval);
	  		for(var i in newval){
	  			var bol = newval[i]['bol'];
	  			if(bol){
	  				 nums=nums-1;
	  			}
	  		}
	  		this.num = nums;
  	  },
  	  deep:true
  }
 },
 mounted:function(){
 	 this.num = this.msg.length;
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.header{
	 padding:5px 0;
	 text-align: center;
	 background-color: red;
	 color: #ffffff;
	 font-weight: 700;
	 margin-bottom:8px;
}
h4{
	margin: 0;
}
.red{
	color: red;
}
.addText{
	width: 100%;
	padding:5px 8px;
	margin-top:10px;
	margin-bottom: 6px;
}
.nav-list{
	overflow: hidden;
}
.nav-list span{
	display: inline-block;
	padding:5px 8px;
	float: right;
}
.nav-list span:first-child{
	float: left;
}
.listOne{
	 width:100%;
	 padding:5px 15px 8px;
	 overflow: hidden;
	 border: 1px solid black;
   margin:4px 0;
}
.listOne input{
	 width:15px;
	 height:15px;
	 position:relative;
	 top:3px;
}
.del{
	float:right;
	display: inline-block;
}
</style>
