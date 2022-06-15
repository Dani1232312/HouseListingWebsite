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
    bathrooms:Number
  }
}
</script>

<template>
<div class="house-card">
  <div class="house-image">
    <img src="@/assets/img_placeholder_house.png" alt="" width="350" height="180">
  </div>
  <div class="house-content">
    <div class="house-header">
      <p class="name">
        {{name}}
      </p>
      <p class="price">
        {{price}} €
      </p>
    </div>
    <div class="house-info">
      <div>
        <img src="@/assets/ic_bed.png" alt="">
        <span>
          {{bedrooms}}
        </span>
      </div>
      <div>
        <img src="@/assets/ic_bath.png" alt="" >
        <span>
          {{bathrooms}}
        </span>
      </div>
      <div>
        <img src="@/assets/ic_size.png" alt="" >
        <span>
          {{size}} ㎡	
        </span>
      </div>
    </div>
  </div>
</div>
</template>

<style>
.listing {
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.3) 0 5px 10px;
  margin: 10px;
  padding: 1%;
  border: 10px;
  width: 40%;
}
.content {
  padding: 30px;
}
.name {
  font-size: 18px;
  font-weight: 600;
}
.house-card{
  width: 350px;
  background-color: white;
  box-shadow: 1px 2px 10px -3px rgba(0,0,0,0.5);
  border-radius: 10px;
  position: relative;
  margin: 20px; 
}
.house-info{
  display: flex;
  padding: 10px 15px 18px 15px;
  color: #959ba4;
}
.house-info div{
  margin-right: 35px;
  margin-left: auto;
}
.house-info img{
  margin-right:8px ;
}
.house-card{
  text-align: center;
}
</style>