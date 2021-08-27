<template>
<div class="content" id="websocket">
  <div>&nbsp;</div>
  <div class="row" >
    <div class="col">
      <button class="btn btn-sm btn-info" @click="connect">Create connection</button>
      <button class="btn btn-sm btn-success" @click="startTask">Start Task</button>
      <button class="btn btn-sm btn-danger" @click="stopTask">Stop Task</button>
      <button class="btn btn-sm btn-primary" @click="disconnect">Close connection</button>
    </div>
  </div>
  <div>&nbsp;</div>
  <div class="row">
    <div class="col">
      <ul class="list-group" style="height: 500px; overflow:scroll;">
        <li class="list-group-item d-flex justify-content-between align-items-center"
            v-for="(m,idx) in messages" :key="'m-'+idx">
          {{m}}
        </li>
      </ul>
    </div>
  </div>
</div>
</template>

<script>
import io from 'socket.io-client'


export default {
 data() {
            return {
              stompClient: null,
              messages : []}
        },
        methods: {
           connect: function(){
           var socket = io('http://localhost:9092/chat'
    );

                
                 
            
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

</style>