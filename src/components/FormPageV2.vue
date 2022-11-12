<template>
    <form @submit="onSubmit" class="formContainer">
        <div id="form">
            <p>Street name*</p>
            <input
                type="text"
                :value="name"
                @input="$emit('update:name', $event.target.value)"
            />
        </div>
        <div id="form2">
            <span>
                <p>House number*</p>
                <input
                        type="text"
                        :value="number"
                        @input="$emit('update:number', $event.target.value)"
                    />
            </span>
            <span>
                <p>Aditional</p>
                <input  input="text"                >
            </span>
        </div>
        <div id="form">
            <p>Postal code*</p>
            <input
                type="text"
                :value="postalCode"
                @input="$emit('update:postalCode', $event.target.value)"
            />
        </div>
        <div id="form">
            <p>City*</p>
            <input
                type="text"
                :value="city"
                @input="$emit('update:city', $event.target.value)"
            />
        </div>
        <div id="form">
            <p>Upload picture*</p>
            <img src="@/assets/img_placeholder_house.png" alt="" width="300" height="180">
        </div>
        <div id="form">
            <p>Price*</p>
            <input
                type="number"
                :value="price"
                @input="$emit('update:price', $event.target.value)"
            />        </div>
        <div id="form2">
            <span>
                <p>Size*</p>
            <input
                type="number"
                :value="size"
                @input="$emit('update:number', $event.target.value)"
            />
            </span>
            <input type="checkbox" id="checkbox"           >
            <label for="checkbox">Garage</label>
        </div>
        <div id="form2">
            <span>
                <p>Bedrooms*</p>
            <input
                type="number"
                :value="bedrooms"
                @input="$emit('update:bedrooms', $event.target.value)"
            />
            </span>
            <span>
                <p>Bathrooms*</p>
            <input
                type="number"  
                :value="bathrooms"
                @input="$emit('update:bathrooms', $event.target.value)"
            />
            </span>
        </div>
        <div id="form">
            <p>Constrution date*</p>
            <input
                type="number"
                :value="constructionDate"
                @input="$emit('update:constructionDate', $event.target.value)"
            />
        </div>
        <div id="form3">
            <p>Description*</p>
            <input
                type="text"
                :value="Description"
                @input="$emit('update:description', $event.target.value)"
            />        
        </div>
        <input type="submit" value="Save Information" class="btn btn-block" />
    </form>
</template>

<script>

    export default {
        data(){
            return{
            }
        },
      props: {
          name: String,
          price: Number,
          postalCode: String,
          bedrooms: Number,
          bathrooms:Number,
          size:Number,
          city:String,
          garage:Boolean,
          constructionDate:Number,
          Description:String,
          number:Number,
          add:String
        },
        methods : {
            onSubmit(e){
                e.preventDefault()
                const NewInformation = {
                    id: Math.floor(Math.random() * 100000),
                    name : this.name,
                    price : this.price,
                    postalCode : this.postalCode,
                    bedrooms : this.bedrooms,
                    bathrooms : this.bathrooms,
                    size : this.size,
                    city : this.city,
                    number : this.number,
                    add : this.add,
                    garage : this.garage,
                    constructionDate : this.constructionDate,
                    Description : this.Description
                }
                 this.$emit('add-information', NewInformation)
                return NewInformation
            }
        },
      emits: ['update:name', 'update:price', 'update:postalCode', 'update:bedrooms', 'update:bathrooms', 'update:size', 'update:city', 'update:garage', 'update:constructionDate', 'update:description', 'add-information', 'update:number'],
    }
    </script>