<!--<template >-->
  <!--<div>-->
    <!--<h1>{{title}}</h1>-->
    <!--<h1 v-bind:class="{red:isRed}" >{{post.id}}</h1>-->
    <!--<h1 v-bind:style="{color:'green' }" >{{post.title}}</h1>-->
  <!--</div>-->
<!--</template>-->

<script>
    export default {
        name: "HelloVue",
        props:['post'],
        data(){
          return{
            title:'我是组件2',
            message:'我有class',
            message2:'我有style',
            isRed:true

          }
        },
      template:
      '    <div>\n' +
        '<slot></slot>\n'+
      '    <h1 v-bind:class="{red:isRed}">{{post.id}}</h1>\n' +
      '<button @click="$emit(\'enlargeText\',1)">enlargeText</button>\n'+
      '    <h1 v-bind:style="{color:\'green\' }" >{{post.title}}</h1>\n'+
      '</div>'
    }
</script>

<style scoped>
.red{
  color:red
}
</style>
