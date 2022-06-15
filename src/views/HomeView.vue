<template> 
  <div v-if="!create" id="info">
    <h1>
      Houses
    </h1>
    <button v-if="!showModal" @click="setCreate" id = "button">
      <img  src = "@/assets/ic_plus_white.png" >
      CREATE NEW
    </button>
  </div>
  <div id="sort-bar" v-if="!showModal">
    <div v-if="!create">
      <select name="sortBy" id="select" v-model="sortBy">
        <option value="alphabetically">Alphabetically</option>
        <option value="price">Price</option>
      </select>
      <button v-on:click="ascending = !ascending" class="sort-button">
        <i v-if="ascending" class="fa fa-sort-up"></i>
        <i v-else class="fa fa-sort-down"></i>
      </button>
      <input type="number" v-model="maxPrice" id="price-input">
      <input type="text" v-model="searchValue" placeholder="Search Listing" id="search-input">
      <i class="fa fa-search"></i>
    </div>
    <div id="container" >
      <div v-if="!create"> 
        <div v-if="filteredList==''" id="no-result">
          <img  src = "@/assets/img_empty_houses.png" >
          <p>
            No result found.
          </p>
          <p>
            Please try another keyword.
          </p>
        </div>
        <div v-else id="listings-container" >
          <HouseListing 
            v-for="post in filteredList"
            :key="post.id"
            :id="post.id"
            :name="post.name"
            :price="post.price"
            :postalCode="post.postalCode"
            :city="post.city"
            :bedrooms="post.bedrooms"
            :bathrooms="post.bathrooms"
            :size="post.size"
            :garage="post.garage"
            :constructionDate="post.constructionDate"
            :Description="post.Description"
            @click="showDetails(post)"
        ></HouseListing>
        </div>
      </div>
      <div v-else>
        <div id="menu" @onclick="hideDetails">
          <img alt="back" src="@/assets/ic_back_grey.png" v-on:click="hideDetails()">
          <span>Back to overview</span>
        </div>
        <FormPageV2 @add-information="addListing"
          v-model="houses[index]"
          :key="houses[index].id"
          v-model:id="houses[index].id"
          v-model:name="houses[index].name"
          v-model:price="houses[index].price"
          v-model:postalCode="houses[index].postalCode"
          v-model:city="houses[index].city"
          v-model:bedrooms="houses[index].bedrooms"
          v-model:bathrooms="houses[index].bathrooms"
          v-model:size="houses[index].size"
          v-model:garage="houses[index].garage"
          v-model:constructionDate="houses[index].constructionDate"
          v-model:Description="houses[index].Description"
          v-model:number="houses[index].number"
        ></FormPageV2>

      </div>
    </div>
  </div>
  <div v-else>
    <div id="menu" @onclick="hideDetails">
        <img alt="back" src="@/assets/ic_back_grey.png" v-on:click="hideDetails()">
        <span id="back">Back to overview</span>
    </div>
    <div class="house" id = "house">
      <HouseInformation @delete-House="deleteHouse" @edit-House="editHouse"
        :key="dani.id"
        v-model:id="dani.id"
        v-model:name="dani.name"
        v-model:price="dani.price"
        v-model:postalCode="dani.postalCode"
        v-model:city="dani.city"
        v-model:bedrooms="dani.bedrooms"
        v-model:bathrooms="dani.bathrooms"
        v-model:size="dani.size"
        v-model:garage="dani.garage"
        v-model:constructionDate="dani.constructionDate"
        v-model:Description="dani.Description"
        v-model:recomended = "list"
      ></HouseInformation>
      <div class="recomended">
            <HouseListing 
                v-for="post in recomended"
                :key="post.id"
                :id="post.id"
                :name="post.name"
                :price="post.price"
                :postalCode="post.postalCode"
                :city="post.city"
                :bedrooms="post.bedrooms"
                :bathrooms="post.bathrooms"
                :size="post.size"
                :garage="post.garage"
                :constructionDate="post.constructionDate"
                :Description="post.Description"
            ></HouseListing>
        </div>
    </div>
  </div>
</template>

<script>
import HouseListing from '@/components/HouseListing.vue';
import HouseInformation from '@/components/HouseInformation.vue';
import FormPageV2 from '@/components/FormPageV2.vue'
let id =0;
let cac = {
  id:0,
  name:"",
  price:0,
  postalCode:"",
  bedrooms:0,
  bathrooms:0,
  size:0,
  city:"",
  garage:false,
  constructionDate:0,
  Description:""
}
export default {
  name: 'App',
  components: {
    HouseListing,
    HouseInformation,
    FormPageV2
},
  data() {
    return {
      houses: [
        { id: id++, name: 'Mariagaardestraat 96' ,number:95, price:100000, postalCode:"6041 HM",bedrooms:3,bathrooms:3,size:10,city:"Roemond",garage:true,constructionDate:1979,Description:"LorempIpsum"},
        { id: id++, name: 'Lindengracht 204' ,number:95, price:120000, postalCode:"1015 KL",bedrooms:4,bathrooms:3,size:10,city:"Amsterdam",garage:false,constructionDate:1979,Description:"LorempIpsum"},
        { id: id++, name: 'Overtoom 572 ' ,number:95, price:190000, postalCode:"1054 LN",bedrooms:2,bathrooms:1,size:10,city:"Amsterdam",garage:false,constructionDate:1979,Description:"LorempIpsum"},
        { id: id++, name: 'Vliedlaan 66' ,number:95, price:210000, postalCode:"1741 RS",bedrooms:3,bathrooms:2,size:10,city:"Schagen",garage:false,constructionDate:1979,Description:"LorempIpsum"},
        { id: id++, name: 'gobiusstraat 2' ,number:95, price:172000, postalCode:"4501 DA",bedrooms:2,bathrooms:1,size:10,city:"ootsburg",garage:false,constructionDate:1979,Description:"LorempIpsum"},
      ],
      caca:-1,
      searchValue:'',
      showModal :false,
      current:[{id: -1, name: '' , price:0, postalCode:"",bedrooms:0,bathrooms:0,size:0,city:"",garage:false,constructionDate:0,Description:""}],
      dani:-1,
      list:-1,
      create:false,
      newInformation:-1,
            ascending: true,
      sortBy: 'alphabetically',
      maxPrice: null,
      toBeEdited:-1,
      index:-1,
      recomended:[
        { id: id++, name: 'Mariagaardestraat 96' , price:100000, postalCode:"6041 HM",bedrooms:3,bathrooms:3,size:10,city:"Roemond",garage:true,constructionDate:1979,Description:"LorempIpsum"},
        { id: id++, name: 'Lindengracht 204' , price:120000, postalCode:"1015 KL",bedrooms:4,bathrooms:3,size:10,city:"Amsterdam",garage:false,constructionDate:1979,Description:"LorempIpsum"},
        { id: id++, name: 'Overtoom 572 ' , price:190000, postalCode:"1054 LN",bedrooms:2,bathrooms:1,size:10,city:"Amsterdam",garage:false,constructionDate:1979,Description:"LorempIpsum"},
      ]
    }
  },
  computed: {
    filteredList() {
      let temp = this.houses
      if (this.searchValue != '' && this.searchValue) {
        temp = temp.filter((item) => {
          return item.name
            .toUpperCase()
            .includes(this.searchValue.toUpperCase())
        })
      }
      // Filter out by price
      if (this.maxPrice)
      temp = temp.filter((item) => {
        return (item.price <= this.maxPrice)
      })
      // Sort by alphabetical order
        temp = temp.sort((a, b) => {
            if (this.sortBy == 'alphabetically') {
                let fa = a.name.toLowerCase(), fb = b.name.toLowerCase()
          
              if (fa < fb) {
                return -1
              }
              if (fa > fb) {
                return 1 
              }
              return 0
              
              // Sort by price
            } else if (this.sortBy == 'price') {
              return a.price - b.price
        }
        })
        // Show sorted array in descending or ascending order
      if (!this.ascending) {
        temp.reverse()
      }

      return temp
    }
  },
    methods:{
      addListing(inf){
        this.newInformation = inf;
        this.create=false;
        console.log("inf",inf)
        console.log("change", this.houses[this.index])
        this.houses[this.index] = inf;
        this.index=-1;
        console.log(this.houses)
        // this.houses.push(inf);    
        // console.log(inf)
      },
       showDetails(post){
          this.dani = post;
          let i = this.houses.map(item => item.id).indexOf(this.dani.id) // find index of your object
          this.index = i
          this.getCurrent().id = post.id
          this.setCur(post)
          this.showModal = true;
          this.list = this.filteredList
          return this.showModal
       },
       hideDetails(){
        this.showModal = false;
        this.create = false;
        this.index=-1;
        this.dani=-1;
        return this.showModal
       },
       goToAbout(){
         this.$router.push('/about')
       },
       getCurrent(){
         return this.current
       },
       setCur(post){
          cac.id=post.id;
          cac.name = post.name;
          cac.price = post.price;
          cac.postalCode = post.postalCode;
          cac.bedrooms = post.bedrooms;
          cac.bathrooms = post.bathrooms;
          cac.size = post.size;
          cac.garage = post.garage;
          cac.constructionDate = post.constructionDate;
          cac.Description = post.Description
          this.current.id = post.id;
          this.current.name = post.name;
          this.current.price = post.price;
          this.current.postalCode = post.postalCode;
          this.current.bedrooms = post.bedrooms;
          this.current.bathrooms = post.bathrooms;
          this.current.size = post.size;
          this.current.city = post.city;
          this.current.bedrooms=post.bedrooms;
          this.current.bathrooms=post.bathrooms;
          this.current.size=post.size;
          this.current.garage=post.garage;
          this.current.constructionDate=post.constructionDate;
          this.current.Description=post.Description;
          return cac
       },
       getCur(){
         return cac
       },
       setCreate(){
         this.create = true;
         if(this.index === -1){
           console.log(this.houses)
           const NewInformation = {
                    id: Math.floor(Math.random() * 100000),
                    name : '',
                    price : 0,
                    postalCode : '',
                    bedrooms : 0,
                    bathrooms : 0,
                    size : 0,
                    city : '',
                    number : 0,
                    add : 0,
                    garage : false,
                    constructionDate : 0,
                    Description : ''
                }
           this.houses.push(NewInformation)
           this.index = this.houses.length -1
                       console.log(this.houses)
            console.log(this.index)
         }
         return this.create;
       },
       deleteHouse(house){
        this.toBeEdited = house;
        let i = this.houses.map(item => item.id).indexOf(this.dani.id) // find index of your object
        this.houses.splice(i, 1)
        this.showModal = false;
        this.create = false;
       },
       editHouse(){
         this.showModal=false;
         this.create=false;
         this.create = true;
       }
  }
}
</script>

<style>
body {
  background: rgb(232, 232, 232);
  padding: 20px;
  font-family: Helvetica;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
  margin-top: 10px;
  height: 20px;
  margin-bottom: 50px;
  right: 0px;
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
#house{
    background-color: rgb(242, 244, 245);
    flex: 1 0 auto;
    flex-direction: column;
    padding-left: 16px;
    padding-right: 16px;
    display: grid;
    margin: 0px auto;
    grid-template-rows: auto;
    grid-template-columns: [main-start] 800px [aside-start] 402px [aside-end];
    column-gap: 15px;
}
#info {
  display: flex;
  position: relative;
  font-family: Helvetica;

}
#button{
right: 10px;
position: absolute;
background-color: #d85555;
vertical-align: center;
border-radius: 10px;
text-align: center;
font-family: Helvetica;
margin-top: 25px;
}
#back{
  vertical-align: center;
  }
#no-result{
  margin-top: 70px;
  text-align: center;
}
</style>

