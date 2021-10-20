<template>
    <header>
        <div class="overlay" ref="overlay"></div>
        <div class="top-header">
            <img src="../assets/images/logo.svg" alt="logo" class="logo" />
            <div class="desktop-menu">
                <a href="#">About</a>
                <a href="#">Discover</a>
                <a href="#">Get Started</a>
            </div>
            <div @click="toggleMenu" class="toggle-menu">

                <img :src='image1' v-if="!showMenu" alt="menu" class="menu-icon" />
                <img :src="image2" v-if="showMenu" alt="menu" class="menu-icon" />
            </div>
        </div>
        <div v-if="mobileMenu" class="menu-items" ref="mobileMenu">
            <a href="#">About</a>
            <a href="#">Discover</a>
            <a href="#">Get Started</a>
        </div>
    </header>
</template>
<script>
import image1 from "../assets/images/icon-hamburger.svg"
import image2 from "../assets/images/icon-close-menu.svg"

export default {
    name:'Header',
    data(){
        return{
            image1 : image1,
            image2 : image2,
            showMenu: false,
            mobileMenu: false,
        }
    },
    methods:{
        toggleMenu(){
            this.showMenu = !this.showMenu
            if(this.showMenu){
                this.$refs.overlay.classList.add('showOverlay'),
                this.mobileMenu = true
            }else{
                this.$refs.overlay.classList.remove('showOverlay'),
                this.mobileMenu = false
            }
        }
    },
    mounted(){
        let toggleMenu = document.querySelector('.toggle-menu');
        if(toggleMenu.style.display == 'none'){
            this.mobileMenu = true
        }
       
    }
}
</script>
<style>
    header{
        background-image:url('../assets/images/image-hero-mobile.jpg');
        background-size:cover;
        background-repeat:no-repeat;
        height:14rem;
        padding:1.5rem;
    }
    .top-header{
        display:flex;
        justify-content: space-between;
        align-items:flex-start;
        position:relative;
        z-index:33;
    }
    .toggle-menu{
        display:inline-block;
    }
    .menu-items{
        background-color:white;
        margin-top:1.8rem;
        border-radius:5px;
        position:relative;
        z-index:33;
    }
    .menu-items a{
        color:hsl(0, 0%, 0%);
        font-weight:500;
        padding:1.5rem;
        text-decoration:none;
        display:block;
        cursor:pointer;
    }
    .menu-items a:hover{
        opacity:.8;
    }
    .menu-items a:not(:last-child){
        border-bottom: 1px solid hsl(0, 0%, 68%);
    }
    .overlay{
        display:none;
    }
    .showOverlay{
        background-color:grey;
        height:100vh;
        position:fixed;
        top:0;
        right:0px;
        bottom:0px;
        left:0px;
        display:block;
        opacity:.3;
    }
    .desktop-menu{
        display:none;
    }
    @media(min-width:700px){
        header{
            background-image:url("../assets/images/image-hero-desktop.jpg");
            padding:2.5rem 3.2rem;
        }
        .toggle-menu{
            display:none;
        }
        .desktop-menu{
            display:inline-block;
        }
        .desktop-menu a{
            color:white;
            padding:2rem;
            text-decoration:none;
        }
        .desktop-menu a:hover{
            opacity:.7;
        }
    }

</style>
