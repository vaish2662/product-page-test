<template>

    <div class="productImg">
        <div class="row">
            <div class="col img-card">
                <!-- <img class="showImg featured-Img" src="../../../public/images/image-product-1.jpg" alt="im1"> -->
                
                <img :src="featuredImage" id="featured-image" class="showImg" alt="Featured Image" />
                <div class="row">
            <div class="col small-Card">

<div v-for="(image, index) in productData?.images" :key="index">
  <img :src="image" :class="{ 'sm-card': currentIndex === index }" @click="setFeaturedImage(index)" class="small-Img" />
</div>
                    <!-- <img class="small-Img" @click="setFeaturedImage(index)"  src="../../../public/images/image-product-2.jpg" alt="im1">  -->
                    <!-- <img class="small-Img" @click="setFeaturedImage(index)" src="../../../public/images/image-product-3.jpg" alt="im1">                       -->
                    <!-- <img class="small-Img" src="../../../public/images/image-product-4.jpg" alt="im1">  -->
            </div>
        </div>
                
            </div>
            <div class="col mobileContainer">
                <h3 class="sneakerHeader">SNEAKER COMPANY</h3>
                <h1 class="heading">{{ productData?.name }}</h1>
                <p class="description">{{ productData?.description }}</p><br>
                <div class="row">
                <p class="discountedPrice">${{ productData?.price?.discounted.toFixed(2) }}</p>
                <p class="percent"><b>{{ productData?.discount.amount }}%</b></p> 
                </div>
                <p class="priceFull">${{ productData?.price?.full }}</p>
                <div class="container">
            <div class="quantity">
            <button class="quantity-button minus"><p style="margin-left: 20px;">-</p></button>
            <input type="text" value="0" class="quantity-input" >
            <button class="quantity-button plus"> <p style="margin-left: 20px;">+</p></button>
             </div>
             
        <button class="add-to-cart">
           <span class="cart-icon">🛒</span> Add to cart
        </button>
    </div>
            </div>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios';
export default {
    components:{
    },
    data(){
        return{
            productData:null,
            featuredImage: '',
            currentIndex: 0,
            images:null,
        }
    },
    async mounted(){
            const res= await axios.get('/client/products/fall-limited-edition-sneakers');
            // console.log(res);
            this.productData=res.data.data;
            // console.log(this.productData);
            this.images=this.productData.images;
            // console.log(this.images);
            this.featuredImage=this.images[0];
        
    },
    methods:{
        setFeaturedImage(index) {
      this.featuredImage = this.images[index];
      this.currentIndex = index;
    }
    },
    created() {
    // this.featuredImage = this.images[0]; // Set the initial featured image
  }

}
</script>
<style scoped>
@media only screen and (min-width: 1440px) {
.productImg{
    padding: 160px;
}
.showImg{
    height: 80%;
    border-radius: 20px;
}
.sneakerHeader{
    /* visibility: hidden; */
    display: none;
}
.img-card img {
  width: 100%;
  flex-shrink: 0;
  border-radius: 4px;
  height: 520px;
  object-fit: cover;
}

.small-Card {
  display: flex;
  justify-content: start;
  align-items: center;
  margin-top: 15px;
  gap: 12px;
}

.small-Card img {
  width: 100%;
  height: 100%;
  border-radius: 4px;
  cursor: pointer;
}

.small-Card img:active {
  border: 1px solid #17696a;
}

.heading{
    padding-top: 20px;
    font-size: 50px;
    text-align: left;
    color: hsl(220, 13%, 13%);
}
.description{
    font-size: 16px;
    text-align: left;
    padding-top: 20px;
    color: hsl(220, 14%, 75%);
}
.discountedPrice{
    font-size: 30px;
    text-align: left;
    color: hsl(220, 13%, 13%);  
    font-weight: bold;
}
.percent{
    color:hsl(26, 100%, 55%);
    background-color: hsl(25, 100%, 94%);
    font-size: 16px;
    margin-top: 8px;
    padding: 4px;
    margin-left: 10px;
}
.priceFull{
    text-decoration: line-through;
    text-align: left;
    color: hsl(220, 14%, 75%);
    margin-top: 4px;
}
.container {
    display: flex;
    align-items: center;
}

.quantity {
    display: flex;
    align-items: center;
    border: 1px solid #ddd;
    border-radius: 5px;
    overflow: hidden;
    margin-right: 10px;
    background-color: hsl(223, 64%, 98%);
}

.quantity-button {
    background-color: hsl(223, 64%, 98%);
    border: none;    
    padding: 15px 25px;
    align-items: center;
    display: flex;
    cursor: pointer;
    font-size: 16px;
    color: hsl(26, 100%, 55%);
    font-weight: bold;
}

.quantity-button:hover {
    background-color: #e0e0e0;
}

.quantity-input {
    width: 40px;
    text-align: center;
    border: none;
    outline: none;
    font-weight: bold;
    background-color: hsl(223, 64%, 98%)   ;
}
.add-to-cart {
    background-color: #ff6600;
    color: white;
    border: none;
    display: flex;
    align-items: center;
    justify-content: center; /* This centers the content inside the button */
    font-size: 16px;
    font-weight: bold;
    border: 1px solid #ddd;
    border-radius: 5px;
    /* cursor: pointer; */
    margin-bottom: 10px;
}

.add-to-cart:hover {
    background-color: #e65c00;
}

.cart-icon {
    /* margin-left: 40px; */
    color: white;
}
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

.row {
    display: flex; 
    flex-wrap: wrap; 
}

.col {
    flex: 1; 
    max-width: 50%;
    padding: 10px; 
}

.col {
    text-align: center;
    padding: 20px;
    margin: 5px;
}
}
@media only screen and (min-width: 375px) {
.mobileContainer{
    padding:20px;
}

.sneakerHeader{
    color: hsl(26, 100%, 55%);
}
.small-Card {
  display: flex;
  justify-content: start;
  align-items: center;
  margin-top: 15px;
  gap: 12px;
}

.small-Card img {
  width: 100%;
  height: 100%;
  border-radius: 4px;
  cursor: pointer;
}

.small-Card img:active {
  border: 1px solid #17696a;
}
.heading{
    padding-top: 20px;
    /* font-size: 30px; */
    text-align: left;
    color: hsl(220, 13%, 13%);
}
.description{
    font-size: 16px;
    text-align: left;
    padding-top: 20px;
    color: hsl(220, 14%, 75%);
}
.discountedPrice{
    font-size: 30px;
    text-align: left;
    color: hsl(220, 13%, 13%);  
    font-weight: bold;
}
.percent{
    color:hsl(26, 100%, 55%);
    background-color: hsl(25, 100%, 94%);
    font-size: 16px;
    margin-top: 8px;
    padding: 4px;
    margin-left: 10px;
}
.priceFull{
    text-decoration: line-through;
    text-align: left;
    color: hsl(220, 14%, 75%);
    margin-top: 4px;
}
/* .container {
    display: flex;
    align-items: center;
    margin-top: 20px;
} */

.quantity {
    display: flex;
    width: 100%;
    align-items: center;
    border: 1px solid #ddd;
    border-radius: 10px;    
    margin-top: 10px;
    overflow: hidden;
    background-color: hsl(223, 64%, 98%);
}

.quantity-button {
    background-color: hsl(223, 64%, 98%);
    border: none;
    width: 100%;
    padding: 15px 25px;
    align-items: center;
    cursor: pointer;
    font-size: 25px;
    color: hsl(26, 100%, 55%);
    font-weight: bold;
}

.quantity-button:hover {
    background-color: #e0e0e0;
}

.quantity-input {
    width: 40px;
    text-align: center;
    font-size: 16px;
    border: none;
    outline: none;
    font-weight: bold;
    background-color: hsl(223, 64%, 98%);
}

.add-to-cart {
    background-color: #ff6600;
    color: white;
    border: none;
    width: 100%;
    border-radius: 5px;
    margin-top: 20px;
    padding: 20px;
    cursor: pointer;
    display: inline;
    align-items: center;
    font-size: 16px;
    font-weight: bold;
    transition: background-color 0.3s ease;
}


.add-to-cart:hover {
    background-color: #e65c00;
}

.cart-icon {
    /* margin-left: 20px; */
    align-items: center;
    color: hsl(0, 0%, 100%);
}
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
.row {
    display: flex; 
    flex-wrap: wrap; 
}

}
</style>