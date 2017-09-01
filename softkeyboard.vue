<template>
	<div>
	    	 <x-dialog v-model="showpay" hide-on-blur>
    	 	<div style="text-align: center;background-color:white;font-family: '宋体';position: relative;">
    	 		<div style="border-bottom: 1px gainsboro solid;font-size: 1.2em;padding-left:5%;padding-top: 5%;color:limegreen;text-align: left;"><img :src="headurl" style="width: 10%;height: 1.2em;vertical-align: middle;padding-bottom: 1%;"><span style="padding-left: 3%;">请输入支付密码</span></div>
    	 		
    	 		<div  style="font-weight: bold;"><span style="font-size: 0.8em;">&#65509;</span>{{totalprice}}</div>
    	 		<div class="input">
				  
				    	
				    
				    		
			    		<span ><img src="http://120.24.249.13:38080/userfiles/paspot.png" style="vertical-align: middle;" id="0"></span>
		    			<span ><img src="http://120.24.249.13:38080/userfiles/paspot.png" style="vertical-align: middle;" id="1"></span>
		    			<span ><img src="http://120.24.249.13:38080/userfiles/paspot.png" style="vertical-align: middle;" id="2"></span>
		    			<span ><img src="http://120.24.249.13:38080/userfiles/paspot.png" style="vertical-align: middle;" id="3"></span>
		    			<span ><img src="http://120.24.249.13:38080/userfiles/paspot.png" style="vertical-align: middle;" id="4"></span>
		    			<span style="border-right: none;" ><img src="http://120.24.249.13:38080/userfiles/paspot.png" style="vertical-align: middle;" id="5"></span>
	    		
				    
				    
				    	
          </div>
          <br />
    	 	</div>
    	 	<div @click="keyclick">
    	 		 <grid :rows="3" style="background-color: white;">
		      <grid-item v-for="i in 12" :key="i">
		        <span class="grid-center" v-if="i!=10&&i!=11&&i!=12">{{i}}</span>
		       <div class="grid-center" v-if="i==10">.</div> 
		       <span class="grid-center" v-if="i==11">0</span>
		       <span class="grid-center1" v-if="i==12" id="del">&times;</span>
		      </grid-item>
		      
            </grid>
    	 	</div>
    	 </x-dialog>
    	 </div>
</template>

<script>
	import { XDialog,Grid, GridItem} from 'vux'
	
	import { TransferDomDirective as TransferDom } from 'vux'
	export default{
		 directives: {
    TransferDom
  },
   
		components:{
			XDialog,Grid, GridItem
		},
		data(){
			return{
				showpay:false,
				actived:0,//密码数字个数统计
				password:[],//存储用户输入密码
				
				paytype:0,
				totalprice:0,//传入参数的价格
				headurl:'',//传入头像url
				
			}
		},
		methods:{
			 show(){
         this.showpay=true;

     },
     keyclick(){//键盘点击函数
     	var _this=this;
     	window.name="paypage";
     	 window.onclick=function(e){ 
				var evt=e||window.event; 
				var tar=evt.target||evt.srcElement; 
				

				
				if( ((tar.tagName.toLowerCase()=="span")&&window.name=="paypage"&&tar.className=='grid-center'&&tar.id=='')||(tar.tagName.toLowerCase()=="a"&&tar.className=='weui-grid'&&tar.children[0].id=='')){
					
								if(_this.actived<6){	
									var pass=document.getElementById(_this.actived);
								pass.style.display='block';
								_this.actived=_this.actived+1;
								if(tar.tagName.toLowerCase()=="span"){
									_this.password.push(tar.innerHTML);
									
								}
								if(tar.tagName=="A"){
									_this.password.push(tar.children[0].innerHTML);
									
								}
						  //当密码点达到6个时触发接口		
			          if(_this.actived==6&&_this.paytype==0)
			          {
			          	alert('在此处触发接口');
			          
			          
			          }
			          
			          
			          
			        
								
								
								
								
								}
					
			    	 
			    }
				if(tar.id!=''){//回删操作
					if( ((tar.id=="del")&&window.name=="paypage")||(tar.children[0].id=='del'&&window.name=="paypage")){
						
			    	 		if(_this.actived>0){
			    	 			_this.actived=_this.actived-1;
			    	 			var pass1=document.getElementById(_this.actived);
						        _this.password.pop();
						        
									pass1.style.display="none";
									
								
			    	 		}
					     
				}
				}
				}
     	 
     	  
     },
     show(){
     	this.showpay=true;

     },
    
		}
}	
</script>

<style>
	.input {
margin-left: 4.5%;	
text-align: center;
width: 90%;
height: 2.5em;
border: 1px solid gainsboro;
border-radius: 0.2em;
  	margin-top:2% ;
}
.input span{
float:left;
	width: 16.3%;
	height: 2.5em;
	text-align: center;
	border-right: 1px gainsboro solid;
}
.input img{
	display: none;
	padding-left: 40%;
	padding-top:35%;
}

.grid-center, .grid-center1{
  display: block;
  text-align: center;
  color: black;
 
 
}
</style>