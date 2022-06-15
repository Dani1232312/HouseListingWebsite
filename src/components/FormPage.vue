<template>
    <form @submit="onSubmit" class="formContainer">
        <div id="form">
            <p>Street name*</p>
            <input v-model="name" input="text"
                @input="$emit('update:name', $event.target.value)"
            >
        </div>
        <div id="form2">
            <span>
                <p>House number*</p>
                <input v-model="number" input="text"
                                @input="$emit('update:firstName', $event.target.value)"
            >
            </span>
            <span>
                <p>Aditional</p>
                <input v-model="add" input="text"
                                @input="$emit('update:firstName', $event.target.value)"
                >
            </span>
        </div>
        <div id="form">
            <p>Postal code*</p>
            <input v-model="postalCode" input="text"
                            @input="$emit('update:postalCode', $event.target.value)"
                >
        </div>
        <div id="form">
            <p>City*</p>
            <input v-model="city" input="text"
                            @input="$emit('update:city', $event.target.value)"
            >
        </div>
        <div id="form">
            <p>Upload picture*</p>
            <img src="@/assets/img_placeholder_house.png" alt="" width="300" height="180">
        </div>
        <div id="form">
            <p>Price*</p>
            <input v-model="price" input="number"
                            @input="$emit('update:price', $event.target.value)"
            >
        </div>
        <div id="form2">
            <span>
                <p>Size*</p>
                <input v-model="size" input="text">
            </span>
            <input type="checkbox" id="checkbox" v-model="garage"
                            @input="$emit('update:garage', $event.target.value)"
            >
            <label for="checkbox">Garage</label>
        </div>
        <div id="form2">
            <span>
                <p>Bedrooms*</p>
                <input v-model="bedrooms" input="text"
                                @input="$emit('update:bedrooms', $event.target.value)"
                >
            </span>
            <span>
                <p>Bathrooms*</p>
                <input v-model="bathrooms" input="text"
                                @input="$emit('update:bathrooms', $event.target.value)"
                >
            </span>
        </div>
        <div id="form">
            <p>Constrution date*</p>
            <input v-model="constructionDate" type="date"
                            @input="$emit('update:condstructionDate', $event.target.value)"
            >
        </div>
        <div id="form3">
            <p>Description*</p>
            <input v-model="description" input="text"
                            @input="$emit('update:description', $event.target.value)"
            >
        </div>
        <input type="submit" value="Save Information" class="btn btn-block" />
    </form>
</template>



<script>
    export default {
        props: {


        },
        name : 'AddInformation',
        data (){
            return {
                name : 'z',
                age : '',
                number:-1,
                add:-1,
                postalCode:-1,
                city:'',
                price:-1,
                size:-1,
                garage:false,
                bedrooms:-1,
                bathrooms:-1,
                constructionDate:-1,
                check:false
            }
        },
        methods : {
            onSubmit(e){
                e.preventDefault()
                if(!this.name){
                    alert('Please Add a Street Name')
                    return
                }
                if(!this.city){
                    alert('Please Add a City')
                    return
                }
                if(this.postalCode === -1){
                    alert('Please Add a postal code')
                    return
                }
                if(this.price === -1 || this.price < 100000){
                    alert('Please Add a price')
                    return
                }
                if(this.size === -1){
                    alert('Please Add a Size')
                    return
                }
                const NewInformation = {
                    id: Math.floor(Math.random() * 100000),
                    title : this.name,
                    price : this.price,
                    postalCode : this.postalCode,
                    bedrooms : this.bedrooms,
                    bathrooms : this.bathrooms,
                    size : this.size,
                    city : this.city,
                    // number : this.number,
                    // add : this.add,
                    garage : this.garage,
                    constructionDate : this.constructionDate,
                    Description : this.Description
                }
                this.$emit('add-information', NewInformation)
                this.name = ' ',
                this.age = ' '
            },
            requestHouse(){
                
            }
        },
        emits: ['update:name', 'update:price', 'update:postalCode', 'update:bedrooms', 'update:bathrooms', 'update:size', 'update:city', 'update:garage', 'update:constructionDate', 'update:description', 'update:lastName']
    }
</script>

<style>
#formContainer{
    position:absolute;
    left:0;
}
#form2{
    display: flex;
    margin-bottom: 0px;
}
#form{
    margin-bottom: 0px;
}

</style>