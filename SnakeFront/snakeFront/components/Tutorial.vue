<template>
<div  class="content" id="websocket">
  <div>&nbsp;</div>
  <div class="row " >
     <div class="col">
     
    </div>
    <div class="col ">
    <div class="row">
      <button id="asd" class="btn col btn-sm btn-info" @click="connect">Create connection</button>
      <button class="btn btn-sm col btn-success" @click="startTask">Start Task</button>
      <button class="btn btn-sm col btn-danger" @click="stopTask">Stop Task</button>
      <button class="btn btn-sm col  btn-primary" @click="disconnect">Close connection</button>
      </div>
      <canvas class="conteiner" width="800" height="800" id="gameCanva"   ></canvas>
    </div>
     <div class="col">
      
    </div>
  </div>
<div class="row">
 
 
 

    
  

</div>
  
 
</div>
</template>
<script src="/socket.io.js">  </script>
<script>





export default {

head(){
return{
script:[
  {hid:"io"
  ,
  src: "/socket.io.js"},
    {hid:"ios"
  ,
  src: "/moment.min.js"}
,  {
        src: "https://code.jquery.com/jquery-3.3.1.slim.min.js",
        type: "text/javascript"
      },
      {
        src:
          "https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js",
        type: "text/javascript"
      },


]

}

},
  
 data() {

   
  return {
    cookieName: 0,
    socket  : null,
    gameCanva : null,
    player : null
              }
        },
        beforeMount () {
          console.log("antes")
        


        },
        mounted(){
          this.configureCanva()
          console.log(this)
          this.socket  = io.connect('http://10.205.30.60:9094')
          this.socket.on('chatevent',function(...args){
            console.log("asd")

          });
            this.socket.on('initilize',this.initialize);

           this.socket.on('update',this.update);        
        },
        methods: {
          drawPixel:function(player,color){
            var context =  this.gameCanva.getContext("2d")
            console.log("asd")
            console.log(player)
            context.beginPath();
            context.fillStyle = color || '#000';
      	    context.fillRect(player.x, player.y, 5, 5);
            context.fill();
           
          },
          update:function(args){
            
            console.log(args)
              for( var i in  args){
                console.log(i, this.cookieName)
              if(i == this.cookieName ){
                this.drawPixel(args[i],"red")
              }else
              this.drawPixel(args[i],"#000")

            }
          },
          initialize:function(args){
             console.log(args)
             this.cookieName = args.coockie;
             this.player = args.player
            console.log(this)
             this.drawPixel(args.player,"#000")

          },
          configureCanva:function(){            
            this.gameCanva = $('#gameCanva').get(0);
            var canvaContext =   this.gameCanva.getContext("2d")
           canvaContext.fillStyle = "rgb(220,220,220)";
           canvaContext.fillRect(0, 0, this.gameCanva.width, this.gameCanva.height);
          
           
          },

           connect: function(){
            

              var jsonObject = {userName: "asd",message: "message"};    

              this.socket.emit('chatevent', jsonObject);
            console.log(this.socket)
          
      },
            disconnect: function(){
               
            },
            startTask: function(){
              
            },
            stopTask: function(){
               
            },
         
        }} 

</script>

<style>
html {
  height: 100%;
}
body {
  min-height: 100%;
  background-color: rgb(128,128,128);
}
.conteiner {
    
    display: flex;
    justify-content: center;
    align-items: center;
}

</style>