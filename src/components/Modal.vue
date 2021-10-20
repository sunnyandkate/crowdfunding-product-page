<template>
   <div class="success-message" ref="success-message">
      <img src="../assets/images/icon-check.svg" alt="check" class="check-img"/>
      <h3>Thanks for your support</h3>
      <p>Your pledge brings us one step closer to sharing Mastercraft Bamboo Monitor Riser worldwide. You will get an email once our campaign is completed.</p>
      <button @click="closeConfirm" class="confirm">Got it!</button>
   </div>
   <div :class="{hideModal: successMessage}" class="modal-container">
      <h2>Back this project</h2>
      <div class="close-btn" @click.self="closeModal">X</div>
      <p>Want to support us in bringing Mastercraft Bamboo Monitor Riser out in the world?</p>
      <div class="no-reward" ref="noRewardField">
         <button @click="chooseNoReward" class="choose-btn"></button>
         <h3>Pledge with no reward</h3>
         <p>Choose to support us without a reward if you simply believe in our project. As a backer, you will be signed up to receive product updates via email.</p>
      </div>
      <slot name="modalCont"></slot>
   </div>
   
</template>
<script>
export default({
   name: 'Modal',
   data(){
      return{
         successMessage:false
      }
   },
   methods:{
      closeModal(){
         this.$emit('close')
      }
   }
})
</script>
<style>
   .modal-container{
      background-color:white;
      position:relative;
      top:0;
      left:45%;
      padding:1rem;
      margin-top:-20rem;
      margin-left:-45%;
      width:90%;
      height:100%;
      border-radius:.8rem;
      text-align:center;
      line-height:1.5;
   }
   .modal-container h2{
      display:inline-block;
      text-align:left;
      margin:0;
   }
   .modal-container p{
      text-align:left;
   }
   .no-reward{
      padding:1rem;
      margin-bottom:1rem;
      border:1px solid hsl(0, 0%, 48%);
      border-radius:5px;
   }
   .no-reward h3{
      display:inline-block;
      vertical-align: top;
   }
   .choose-btn{
      background-color:white;
      border:1px solid hsl(0, 0%, 48%);
      height:1rem;
      width:1rem;
      margin-top:1.5rem;
      margin-right:1rem;
      border-radius:50%;
      display:inline-block;
      text-align:left;
      vertical-align: middle;
      outline:none;
   }
   .close-btn{
      color:hsl(0, 0%, 48%);
      position:absolute;
      right:1rem;
      top:1rem;
      cursor: pointer;
   }
   .choosenReward{
      border:2px solid hsl(176, 50%, 47%) !important;
   }
   .choosenReward>.choose-btn, .choosenRewardBtn{
      position:relative;
   }
   .choosenReward>.choose-btn:after, .choosenRewardBtn:after{
      content:'';
      position:absolute;
      top:0;
      left:0;
      right:0;
      bottom:0;
      width:.7rem;
      height:.7rem;
      margin:auto;
      border-radius:50%;
      background-color:hsl(176, 50%, 47%);
   }
   .continue-container{
      display:none;
      padding-top:1rem;
      border-top:1px solid hsl(0, 0%, 48%);
      text-align:center;
   }
   .continue-container p{
      text-align:center;
   }
   .showContinue{
      display:block;
   }
   .continue-bottom{
      display:flex;
      justify-content:space-between;
   }
   .currency{
      position:relative;
   }
   .currency:after{
      color:hsl(0, 0%, 48%);
      position:absolute;
      content:'$';
      left:20%;
      top:20%;
   }
   .inputValue{
      border-radius:1.5rem;
      height:3rem;
      width:6rem;
      border:1px solid lightgrey;
      outline:none;
      cursor:pointer;
      text-align:center;
   }
   .inputValue:hover{
      border-color:hsl(176, 50%, 47%);
   }
   .continue{
      color:white;
      background-color:hsl(176, 50%, 47%);
      font-weight:700;
      padding:1rem 2rem;
      border:none;
      outline:none;
      border-radius:1.5rem;
   }
   .continue:hover{
      background-color:hsl(176, 72%, 28%);
   }
   .success-message{
      background-color:white;
      position:relative;
      margin:-70% auto 0 auto;
      padding:2rem;
      width:60%;
      line-height:1.5;
      text-align:center;
      border-radius:1rem;
      display:none;
   }
   .confirm{
      background-color:hsl(176, 50%, 47%);
      color:white;
      padding:1rem 2rem;
      border:none;
      border-radius:2rem;
   }
   .confirm:hover{
      background-color:hsl(176, 72%, 28%);
   }
   @media(min-width:770px){
      .modal-container{
         width:100%;
         left:50%;
         margin-left:-50%;
      }
      .showContinue{
         display:flex;
         justify-content: space-between;
         align-items:center;
      }
      .continue{
         margin-left:1rem;
      }
   }
   
</style>
