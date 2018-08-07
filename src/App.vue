<template>
  <div id="app">
    <img src="./assets/logo.png" @click="click">
    <h1 v-bind:style="{fontSize:fontSize+'px'}">{{message}}</h1>
    <router-view class="view1" ref="usernameInput" />
    <!--<hello-vue  v-for="post in posts" v-on:enlargeText="fontSize=fontSize+$event" v-bind:post="post" v-bind:key="post.id"  class="view2"></hello-vue>-->
    <hello-vue  v-for="post in posts" v-on:enlargeText="onEnlargeText" v-bind:post="post" v-bind:key="post.id"  class="view2">
      我是子组件包含的内容
    </hello-vue>
    <button v-for="btn in buttons" :style="{marginLeft:0+'px',marginTop:20+'px'}" :key="btn" :class="['tab-button',{active:currentTab == btn}]" @click="currentTab = btn">{{btn}}</button>
    <transition name="component-fade" mode="out-in">
      <keep-alive>
        <component :is="currentTabComponent" class="tab"  >

        </component>
      </keep-alive>
    </transition>

    <p>
      <transition name="fade" mode="in-out">
        <span v-if="show">我是带有动画的</span>
      </transition>
      <button v-on:click="show = !show">Click Me</button>
    </p>


    <div :style="{border:'1px solid red' }">
      <button v-on:click="Add">Add</button>
      <button v-on:click="Remove">Remove</button>
      <button v-on:click="shuffle">Shuffle</button>
      <transition-group name="list-complete" tag="p">
          <span v-for="item in items" v-bind:key="item" class="list-complete-item">
            {{item}}
          </span>
      </transition-group>
    </div>

  </div>
</template>

<script>
import HelloVue from '@/components/HelloVue'
import tabs from '@/components/Tabs'
import archive from '@/components/archive'
export default {
  name: 'App',
  components:{'hello-vue':HelloVue,
    'tabs':tabs,
    'archive':archive
  },
  data(){
    return{
      message:'这是一个自定  义的信息',
      fontSize:12,
      buttons:['tabs','archive'],
      currentTab: 'tabs',
      show:true,
      posts: [
        { id: 1, title: 'My journey with Vue' },
        { id: 2, title: 'Blogging with Vue' },
        { id: 3, title: 'Why Vue is so fun' }
      ],
      items:[1,2,3,4,5,6],
      nextNum: 10
    }

  },
  methods:{
    onEnlargeText:function(enlargeAmount){
      this.fontSize += enlargeAmount;
    },
    click:function(){
      this.$refs.usernameInput.$refs.input.focus()
    },
    randomIndex: function () {
      return Math.floor(Math.random() * this.items.length)
    },
    Add:function(){
      this.items.splice(this.randomIndex(), 0, this.nextNum++)
    },
    Remove:function(){
      this.items.splice(this.randomIndex(), 1)
    },
    shuffle: function () {
      this.items = _.shuffle(this.items)
    }
  },
  computed:{
    currentTabComponent:function(){
      return this.currentTab
    }
  }

}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.view1{
  border:1px solid red
}
.view2{
  border:1px solid blue;
  margin-top:20px
}
.tab-button {
  padding: 6px 10px;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
  border: 1px solid #ccc;
  cursor: pointer;
  background: #f0f0f0;
  margin-bottom: -1px;
  margin-right: -1px;
}
.tab-button:hover {
  background: #e0e0e0;
}
.tab-button.active {
  background: #e0e0e0;
}
.tab {
  border: 1px solid #ccc;
  padding: 10px;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.component-fade-enter-active, .component-fade-leave-active {
  transition: opacity .3s ease;
}
.component-fade-enter, .component-fade-leave-to
  /* .component-fade-leave-active for below version 2.1.8 */ {
  opacity: 0;
}

.list-complete-item {
  transition: all 1s;
  display: inline-block;
  margin-right: 10px;
}
.list-complete-enter, .list-complete-leave-to
  /* .list-complete-leave-active for below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
.list-complete-leave-active {
  position: absolute;
}
</style>
