<template>
 <div>
   <!-- <transition-group name="mcap1" appear>
    <div class="art" v-for="b in article" :key="b.slug">
      <nuxt-link :to="'/'+ b.slug">{{b.title}} {{b.date}}</nuxt-link>
    </div>
   </transition-group> -->
   <div>
     <p>モード</p>
     <div id="modea" @click="mode = false" >aaa</div>
     <div id="modeb" @click="mode = true" >bbb</div>
     <p>次前</p>
     <div id="amounta" @click="prev()" >prev</div>
     <div id="amountb" @click="next()" >next</div>
   </div>
   <div id="articlelist" :class="{'listp' : mode == true}">
    <transition-group name="mcap1" appear id="spp" mode="in-out">
      <div class="art" :class="{'list' : mode == true}" v-for="articles in articles.slice(a,b+c)" :key="articles.slug">
        <nuxt-link :to="'/'+ articles.slug">{{articles.title}}</nuxt-link>
        <p>{{articles.year}}{{articles.month}}{{articles.date}}</p>
      </div>
    </transition-group>
    </div>
 </div>
</template>
<script>
export default {
 data(){
   return{
     mode:false,
     a:0,
     b:10,
     c:0,
   };
 },
 async asyncData ({ $content, params }) {
   //const query = await $content('article' || 'index').limit(10)
   const query = await $content('article' || 'index')
   const article = await query.fetch()
   return { article }
 },
 methods:{
   prev(){
     if(this.a!=0){
       this.a -= 10;
       this.b -= 10;
     }
   },
   next(){
     if(this.b < this.article.length){
       this.a += 10;
       this.b += 10;
     }
   }
 },
 computed: {
    // 配列の要素順番を逆順にする
    articles() {
        return this.article.slice().reverse();
    },
  }
}
</script>

<style lang="scss"scoped>
$white1: #f0f0f0;
$gray1:#333;
.art{
  background-color: $gray1;
  border-radius: 1vw;
  padding: 1.25em;
  margin: 0.5em;
  overflow:hidden;
  a{
    color: $white1;
  }
  p{
    color: #f1f1f1;
  }
  
}
#articlelist{
  max-width: 1400px;
  width: 90%;
  margin: 0 auto;
  overflow-x: hidden;
}
.listp{
  transition: 0.4s;
  #spp{
    display: grid;
  justify-content: center;
    @media screen and (max-width:380px) {
    grid-template-columns: 1fr;
    }
    @media screen and (min-width:380px) {
    grid-template-columns: 1fr 1fr;
    }
    @media screen and (min-width:450px) {
    grid-template-columns: 1fr 1fr 1fr;
    }
    @media screen and (min-width:1024px) {
    grid-template-columns: 1fr 1fr 1fr 1fr;
    }
  .art{
    display: inline-block;
    @media screen and (max-width:450px) {
    height: 22.5vw;
    font-size: 1em;
    }
    @media screen and (min-width:450px) {
    height: 15vw;
    }
    @media screen and (min-width:750px) {
    height: 15vw;
    font-size: 1.5em;
    }
    @media screen and (min-width:1024px) {
    height: 12.5vw;
    font-size: 1.75em;
    }
    @media screen and (min-width:1400px) {
    height: 165px;
    }
  }
  }
  
}
  .mcap1-enter-active{
    transition: all 1s;
    overflow-x: hidden;
    }
  .mcap1-leave-active{
    transition: all 1.5s;
    overflow-x: hidden;
    }
    .mcap1-enter, .mcap1-leave {
      opacity: 0;
     transform: (translateX(350px) rotateX(90deg));
    }
    @for $i from 1 through 25 {
        #spp .mcap1-enter-active:nth-child(#{$i}),
        #spp .mcap1-enter:nth-child(#{$i}){ 
            transition: all 0.8s 0.04 * $i - 0.04s; 
        }
        
    }
</style>