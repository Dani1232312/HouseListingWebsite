<script>
export default {
    props: {
    id:Number,
    name: String,
    price:Number,
    postalCode:String,
    city:String,
    garage:Boolean,
    constructionDate:Number,
    Description:String,
    size:Number,
    bedrooms:Number,
    bathrooms:Number,
  },
  methods:{
      deleteHouse(){
        this.$emit('delete-House')
      },
      editHouse(){
        this.$emit('edit-House')
      }
  }
}
</script>

<template>
        <div class="house">
        <img src="@/assets/img_placeholder_house.png" alt="" id="imag">
            <div id="name">
                <h1 id="main">
                    {{name}}
                </h1>
                <span>
                    <img v-on:click="editHouse()" src="@/assets/ic_edit.png" alt="" id="image" height="21">
                    <img v-on:click="deleteHouse()" src="@/assets/ic_delete.png" alt="" id="image" height="21">
                </span>
            </div>
            <div class="information">
                <div>
                    <img src="@/assets/ic_location.png" alt="" id="image" height="21">
                    <p>
                        {{postalCode}} {{city}}
                    </p>
                </div>
            </div>
            <div class ="information" id="information">
                <div>
                    <img src="@/assets/ic_price.png" alt="" id="image">
                    <span id="info">
                        {{price}}
                    </span>
                </div>
                <div>
                    <img src="@/assets/ic_size.png" alt="" id="image">
                    <span id="info">
                        {{size}} m2
                    </span>
                </div>
                <div>
                    <img src="@/assets/ic_construction_date.png" alt="" id="image">
                    <span id="info">
                        Built in {{constructionDate}}
                    </span>
                </div>
            </div>
            <div class="information" id="information">
                <div>
                    <img src="@/assets/ic_bed.png" alt="" id="image">
                    <span id="info">
                        {{bedrooms}}
                    </span>
                </div>
                <div>
                    <img src="@/assets/ic_bath.png" alt="" id="image">
                    <span id="info">
                        {{bathrooms}}
                    </span>
                </div>
                <div>
                    <img src="@/assets/ic_garage.png" alt="" id="image">
                    <span id="info">
                        {{garage}}
                    </span>
                </div>
            </div>
            <p>
                {{Description}}
            </p>
        </div>
</template>

<style>
#information{
    display: flex;
    margin-bottom: 20px;
}
#image{
      margin-top: 10px;
}
#info{
}
.information div{
  margin-right: 40px;
  margin-left: 0px;
  display: flex;
  vertical-align: center;
}
.information img{
  margin-right:10px ;
  top: 50%;
  transform: translateY(-50%);
}
#imag{
    margin-top: 20px;
}
#house{
    border-radius: 10px;
}
.information span{
    vertical-align: center;
}
#name{
    display: flex;
}
#main{
    margin-right: 50%;
}
#name .img{
    float: right;
}
</style>