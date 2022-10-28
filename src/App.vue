<template>
  <div id="header">
    <img  id="header" src = "@/assets/img_logo_dtt.png" >
    <span id="span">
      <nav id="header">
        <router-link id="header" to="/">Home</router-link>
        <router-link id="header" to="/about">About</router-link>
      </nav>
    </span>
  </div>
  <router-view></router-view>
</template>

<script>
export default {
  name: 'App',
  components: {
},
  data() {
    return {
    }
  },
  computed: {
  },
    methods:{
       goToAbout(){
         this.$router.push('/about')
       }
  }
}
</script>

<style>
body {
  background: rgb(232, 232, 232);
  padding: 20px;
  font-family:'Open Sans';
}
#app {
  font-family: 'Open Sans';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 0px;
  border-radius: 4px;
  padding: 20px;
}
#listings-container {
  display: flex;
  flex-wrap: wrap;
  padding: 1%;
}
#menu{
  height: 20px;
}
#nav {
  padding: 30px;
}
#nav a{
  font-weight: bold;
  color: #2c3e2c;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
#header{
  background-color:#ffffff;
  vertical-align: center;
  margin-right: 50px;
  display: flex;
}
#span{
  display: flex;
  justify-content: center;
  align-items: center;
}
#span {
  top:50%;
  vertical-align:middle;
  text-align: center;
}

</style>

   