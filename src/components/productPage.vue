<template>
   <div class="content-container">
      <div class="modal-overlay" ref="modalOverlay"></div>
      <div class="product">
         <img src="../assets/images/logo-mastercraft.svg" alt="logo-img" class="logo-img">
         <h1>Mastercraft Bamboo Monitor Riser</h1>
         <p>A beautiful & handcrafted monitor stand to reduce neck and eye strain.</p>
         <div class="flex-cont">
            <button @click="toggleModal" class="cta-btn">Back this project</button>
            <div @click="bookmarkToggle()" class="bookm">
               <!-- <img :src="bookmark1" v-if="!bookmarkSelected" alt="bookmark" class="bookmark" /> -->
               <svg v-if="bookmarkSelected" class="bookmark" width="56" height="56" xmlns="http://www.w3.org/2000/svg"><g fill="none" fill-rule="evenodd"><circle fill="hsl(176, 72%, 28%)" cx="28" cy="28" r="28"/><path fill="white" d="M23 19v18l5-5.058L33 37V19z"/></g></svg>
               <svg v-if="!bookmarkSelected" width="56" height="56" xmlns="http://www.w3.org/2000/svg"><g fill="none" fill-rule="evenodd"><circle fill="#2F2F2F" cx="28" cy="28" r="28"/><path fill="#B1B1B1" d="M23 19v18l5-5.058L33 37V19z"/></g></svg>
               <span ref="bookmark" class="bookmark-btn">Bookmark</span>
            </div>
         </div>
         <div v-if="showModal">
            <Modal @close="toggleModal">
               <template v-slot:modalCont>
                  <div v-for="product in product" v-bind:key="product.title" class="stand modal-stand" :class="{hide: product.remaining==0}">
                     <div class="grid-container">
                        <button @click="chooseReward" class="choose-btn item-button choose-reward-btn"></button>
                        <h3 class="product-title product-title-modal item-title">{{ product.title }}</h3>
                        <p id="product-pledge" class="product-pledge product-pledge-modal item-pledge">{{ product.pledge }}</p>
                        <p class="product-remaining item-left"><span>{{ product.remaing + ' '}}</span> left</p>
                        <p class="product-text item-text">{{ product.text }}</p>
                     </div>
                     <div class="continue-container">
                        <p>Enter your pledge</p>
                        <div class="continue-bottom">
                           <div class="currency"><input id="yourInput" class="inputValue" type="text" :placeholder="product.pledgeValue" value=""></div>
                           <button @click="toggleSuccessModal" class="continue">Continue</button>
                        </div>
                     </div>
                  </div>
               </template>
            </Modal>
         </div>
      </div>
      <div class="progress-bar-section">
         <div class="amount"><span>{{ amountValue }}</span> of $100,000 backed</div><hr>
         <div class="backers-num"><span>{{ backers }}</span>total backers</div><hr>
         <div class="remaining-days"><span>{{ days }}</span> days left</div>
         <div class="range-slider">
            <progress min="1" max="100000" :value="amount" id="rangeSlider">
               <div class="progress-bar"><span :style="{ width: amount/1000 + '%'}"></span></div>
            </progress>
         </div>
      </div>
      <div class="main-product">
         <h2>About this product</h2>
         <p>The Mastercraft Bamboo Monitor Riser is a sturdy and stylish platform that elevates your screen 
            to a more comfortable viewing height. Placing your monitor at eye level has the potential to improve 
            your posture and make you more comfortable while at work, helping you stay focused on the task at hand.
         </p>
         <p> Featuring artisan craftsmanship, the simplicity of design creates extra desk space below your computer 
            to allow notepads, pens, and USB sticks to be stored under the stand.</p>
         <div v-for="product in products" v-bind:key="product.title" class="stand" :class="{hide: product.remaining==0}">
            <div class="product-flex-container">
               <h3 class="product-title">{{ product.title }}</h3>
               <p id="product-pledge" class="product-pledge">{{ product.pledge }}</p>
            </div>
            <p class="product-text">{{ product.text }}</p>
            <div class="product-flex-container">
               <p class="product-remaining"><span>{{ product.remaining }}</span> left</p>
               <button @click="bookmarkToggle()" v-bind:key="product.title" ref="selectBtn" class="select-btn" :class="{hideBtn: product.remaining==0}">{{ product.select }}</button>
            </div>
         </div>
      </div>
   </div>
</template>
<script>
// import bookmark1 from "../assets/images/icon-bookmark.svg"
import Modal from "./Modal.vue"

export default{
   name: 'productPage',
   components:{ Modal },
   data(){
      return{
         // bookmark1 : bookmark1,
         amount: 89914,
         amountValue: new Intl.NumberFormat().format(89914),
         backers: 5007,
         days: 56,
         products:[
            {
               title: 'Bamboo Stand',
               pledge: 'Pledge $25 or more',
               text: "You get an ergonomic stand made of natural bamboo. You've helped us launch our promotional campaign, and you’ll be added to a special Backer member list.",
               remaining: 101,
               select: 'Select Reward',
               pledgeValue: 25,
            },
            {
               title: 'Black Edition Stand',
               pledge: 'Pledge $75 or more',
               text: "You get a Black Special Edition computer stand and a personal thank you. You’ll be added to our Backer member list. Shipping is included.",
               remaining: 64,
               select: 'Select Reward',
               pledgeValue: 75,
            },
            {
               title: 'Mahagoni Special Edition',
               pledge: 'Pledge $200 or more',
               text: "You get two Special Edition Mahogany stands, a Backer T-Shirt, and a personal thank you. You’ll be added to our Backer member list. Shipping is included.",
               remaining: 0,
               select: 'Out of Stock',
               pledgeValue: 200,
            }
         ],
         bookmarkSelected: false,
         showModal:false
      }
   },
   methods:{
      bookmarkToggle(){
         this.bookmarkSelected = !this.bookmarkSelected

         if(this.bookmarkSelected){
            this.$refs.bookmark.style.color="hsl(176, 72%, 28%)";
            this.$refs.bookmark.innerText='Bookmarked';
         }else{
            this.$refs.bookmark.style.color="grey";
            this.$refs.bookmark.innerText='Bookmark';
         }
      },
      toggleModal(){
         this.showModal = !this.showModal
         if(this.showModal){
            this.$refs.modalOverlay.classList.add('showOverlay');
         }else{
            this.$refs.modalOverlay.classList.remove('showOverlay');
         }
      }
   },
   mounted(){
      let selectBtn = document.querySelectorAll('.select-btn');
      for(let i=0; i<selectBtn.length;i++){
         selectBtn[i].addEventListener('click', function(){
            this.classList.toggle('selected');
         });
      }
      
   }
}
</script>
<style>
   .content-container{
      width:90%;
      margin: -2.5rem auto 0 auto;
   }
   .product, .progress-bar-section, .main-product{
      background-color:white;
      border-radius: 10px;
      text-align:center;
      margin-bottom: 1.5rem;
   }
   .product h1{
      color:hsl(0, 0%, 0%);
      font-size:1.5rem;
   }
   .product p, .main-product p{
      color:hsl(0, 0%, 48%);
      font-size:.8rem;
      margin-bottom: 2rem;
   }
   .logo-img{
      margin-top:-1.5rem;
   }
   .flex-cont{
      padding-bottom:2rem;
   }
   .cta-btn{
      color:white;
      background-color:hsl(176, 50%, 47%);
      font-weight: 700;
      padding:1rem 2rem;
      margin-right: 1rem;
      outline:none;
      border:none;
      border-radius:1.5rem;
      cursor:pointer;
   }
   .cta-btn:hover{
      background-color:hsl(176, 72%, 28%);
   }
   .bookm, svg{
      display:inline-block;
      vertical-align:middle;
      cursor:pointer;
   }
   .bookm>span{
      display:none;
   }
   .progress-bar-section{
      padding-top:1rem;
      padding-bottom:1.5rem;
   }
   .amount, .backers-num, .remaining-days{
      color:hsl(0, 0%, 48%);
      padding-top:1.5rem;
      padding-bottom:1.5rem;
   }
   .amount>span, .backers-num>span, .remaining-days>span{
      color:black;
      font-size:2rem;
      font-weight:700;
      padding-bottom:1rem;
      display:block;
   }
   hr{
      width:20%;
      color:hsl(0, 0%, 83%);
   }
   .range-slider{
      margin-bottom:2rem;
   }
   progress[value]{
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
      border:none;
      background-color:lightgrey;
      border-radius:1.5rem;
      height:1.5rem;
   }
   progress[value]::-moz-progress-bar{
      background-color:hsl(176, 50%, 47%);
      width:100%;
      height:1.5rem;
      border-radius:1.5rem;
   }
   progress[value]::-webkit-progress-bar{
      background-color:lightgrey;
      width:100%;
      height:1.5rem;
      border-radius:1.5rem;
   }
   progress[value]::-webkit-progress-value{
      background-color:hsl(176, 50%, 47%);
      border-radius:1.5rem;
   }
   .progress-bar{
      background-color:lightgrey;
      border-radius:1.5rem;
      height:1.5rem;
      width:80%;
      margin:auto;
      position:relative;
   }
   .progress-bar>span{
      content:'';
      position:absolute;
      top:0;
      left:0;
      height:1.5rem;
      border-radius:1.5rem;
      background-color:hsl(176, 50%, 47%);
   }
   .main-product{
      padding:1.5rem;
      line-height:1.5;
      text-align:left;
   }
   .main-product h2, .main-product p{
      text-align:left;
   }
   .stand{
      padding:1rem;
      margin-bottom:1rem;
      border:1px solid hsl(0, 0%, 48%);
      border-radius:5px;
   }
   .hide{
      opacity:.5;
   }
   
   .product-title{
      margin-bottom:0;
   }
   .product-title-modal{
      display:inline-block;
   }
   #product-pledge{
      color:hsl(176, 50%, 47%);
   }
   .product-pledge{
      margin-top:0;
   }
   .product-remaining>span{
      color:black;
      font-size:2rem;
      font-weight:700;
   }
   .select-btn{
      color:white;
      background-color:hsl(176, 50%, 47%);
      font-weight:700;
      padding:.8rem 1.5rem;
      border:none;
      border-radius:1.5rem;
      cursor:pointer;
   }
   .selected{
      background-color:hsl(176, 72%, 28%);
   }
   .hideBtn{
      background-color:hsl(0, 0%, 48%);
   }
   .grid-container{
      display:grid;
      grid-template-columns:1fr 5fr;
      grid-template-rows:auto;
      grid-template-areas:
         "button title"
         " . pledge"
         "text text"
         "left left";
   }
   .item-button{
      grid-area:button;
   }
   .item-pledge{
      grid-area:pledge;
   }
   .item-pledge{
      grid-area:title;
   }
   .item-title{
      grid-area:title;
   }
   .item-left{
      grid-area:left;
   }
   .item-text{
      grid-area:text;
   }
@media(min-width:770px){
   .content-container{
      width:60%;
   }
   .flex-cont{
      display:flex;
      justify-content: space-around;
   }
   .cta-btn{
      font-size:1rem;
      padding:1.2rem 2rem;
      border-radius:2rem;
   }
   .bookm{
      background-color:hsla(0, 0%, 47.8%, 0.25);
      padding-right:1.5rem;
      border:none;
      border-radius:2rem;
      display:inline-block;
   }
   .bookm>img{
      vertical-align: middle;
   }
   .bookm>span{
      color:grey;
      font-size:1rem;
      font-weight:700;
      padding-left:1.5rem;
      display:inline-block;
   }
   .bookm:hover{
      opacity: .8;
   }
   .progress-bar-section{
      padding-left:3.5rem;
      padding-top:2.5rem;
      text-align:left;
   }
   .amount, .backers-num, .remaining-days{
      display:inline-block;
      padding-top:0;
      padding-bottom:0;
      width:30%;
   }
   .amount, .backers-num{
      border-right:1px solid hsl(0, 0%, 83%);
   }
   .backers-num, .remaining-days{
      padding-left:1rem;
   }
   hr{
      display: none;
   }
   progress[value]{
      margin-top:2rem;
      margin-left:0;
      width:90%;
   }
   .product-title{
      margin-bottom:1rem;
   }
   #product-pledge{
      margin-bottom:0;
   }
   .product-flex-container{
      display:flex;
      justify-content: space-between;
      align-items: center;
   }
   .grid-container{
      grid-template-columns: auto 2fr 1fr 1fr;
      grid-template-rows: 1fr 1fr;
      grid-template-areas: 
         "button title pledge left"
         "text text text text";
   }
   .item-left{
      justify-self:end;
   }
   .item-pledge{
      margin-top:1.5rem;
   }
}

</style>