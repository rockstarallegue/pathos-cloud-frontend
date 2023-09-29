<template>
    <div class="wrapper full container bg-cyan-11">
      <div class="full-width gradient gradient-1"></div>
      <div class="full-width gradient gradient-2"></div>
      <div class="full-width gradient gradient-3"></div>
    </div>
</template>
<style>
      bgg {
        color: #B9F6CA;
        background-color: #A7FFEB;
        padding: 0; 
      }

      .wrapper {
        width: 100%;
        height: 100%;
        filter: blur(241px);
      }

      .gradient {
        position: absolute;
        border-radius: 100%;
        opacity: 0.4;
        mix-blend-mode: screen;
        animation-iteration-count: infinite;
        animation-timing-function: cubic-bezier(0.1, 0, 0.9, 1);
      }

      
  .gradient-1 {
    background: rgb(104, 239, 174);
    height: 3000px;
    animation-duration: 20s;
    opacity: 0.81;
    z-index: -2;
    animation-name: animation-gradient-1;
  }
  .gradient-2 {
    background: #69F0AE;
    height: 3000px;
    animation-duration: 20s;
    opacity: 0.81;
    z-index: -4;
    animation-name: animation-gradient-2;
  }
  .gradient-3 {
    background: rgb(84, 254, 254);
    height: 3000px;
    animation-duration: 20s;
    opacity: 0.81;
    z-index: -3;
    animation-name: animation-gradient-3;
  }

      @keyframes animation-gradient-1 {
        0% {
          transform: translateY(-50%) translateX(-50%) rotate(-20deg) translateX(20%);
        }
        25% {
          transform: translateY(-50%) translateX(-50%) skew(-15deg, -15deg)
            rotate(80deg) translateX(30%);
        }
        50% {
          transform: translateY(-50%) translateX(-50%) rotate(180deg) translateX(25%);
        }
        75% {
          transform: translateY(-50%) translateX(-50%) skew(15deg, 15deg)
            rotate(240deg) translateX(15%);
        }
        100% {
          transform: translateY(-50%) translateX(-50%) rotate(340deg) translateX(20%);
        }
      }
      
      @keyframes animation-gradient-2 {
        0% {
          transform: translateY(-50%) translateX(-50%) rotate(40deg) translateX(-20%);
        }
        25% {
          transform: translateY(-50%) translateX(-50%) skew(15deg, 15deg)
            rotate(110deg) translateX(-5%);
        }
        50% {
          transform: translateY(-50%) translateX(-50%) rotate(210deg) translateX(-35%);
        }
        75% {
          transform: translateY(-50%) translateX(-50%) skew(-15deg, -15deg)
            rotate(300deg) translateX(-10%);
        }
        100% {
          transform: translateY(-50%) translateX(-50%) rotate(400deg) translateX(-20%);
        }
      }
      
      @keyframes animation-gradient-3 {
        0% {
          transform: translateY(-50%) translateX(-50%) translateX(-15%)
            translateY(10%);
        }
        20% {
          transform: translateY(-50%) translateX(-50%) translateX(20%)
            translateY(-30%);
        }
        40% {
          transform: translateY(-50%) translateX(-50%) translateX(-25%)
            translateY(-15%);
        }
        60% {
          transform: translateY(-50%) translateX(-50%) translateX(30%) translateY(20%);
        }
        80% {
          transform: translateY(-50%) translateX(-50%) translateX(5%) translateY(35%);
        }
        100% {
          transform: translateY(-50%) translateX(-50%) translateX(-15%)
            translateY(10%);
        }
      }

    </style>
  
  <script>
  import { defineComponent } from 'vue'  
  export default defineComponent({
    name: 'PlasmaWrapper'
  })
  </script>
  