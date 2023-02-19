<script>
  import { ref,reactive } from "vue";
  export default {
    setup(){
      const datalist = reactive([
        { AorD: true, level: "A", title: "dehumidifier", tag: 'ONE' },
        { AorD: true, level: "B", title: "range hood", tag: 'ONE' },
        { AorD: true, level: "C", title: "vacuum cleaner", tag: 'ONE' },
        { AorD: false, level: "D", title: "toaster", tag: 'ONE' },
        { AorD: false, level: "E", title: "scale", tag: 'ONE' },
        { AorD: false, level: "F", title: "straightening iron", tag: 'ONE' },
        { AorD: false, level: "G", title: "vacuum cleaner", tag: 'ONE' }, 
        { AorD: false, level: "H", title: "rice cooker", tag: 'ONE' }
      ])

      return {
        datalist
      }
    }
  }

  
</script>

<template>
  <div class="dataList fulid-container sands-bg">
    
    <div class="block-container">
      <ul class="data-container">
        <li class="dataBox b-shadow bradius-20 " :class="[data.AorD ? 'levelA':'levelD']" v-for="data in datalist">
            <div class="certContainer">
              <p class="level-title">{{ data.level }}</p>
            </div>
            <div class="amount-tag bradius-20">{{ data.tag }}</div>
            <h5 class="cert-title">{{ data.title }}</h5>
          </li>
        
          <!-- html template -->
          <!-- <li class="dataBox b-shadow bradius-20 levelA">
            <div class="certContainer">
              <p class="level-title">A</p>
            </div>
            <div class="amount-tag bradius-20">ONE</div>
            <h5 class="cert-title">dehumidifier</h5>
          </li> -->
       
      </ul>
    </div>
   
  </div>

   <div class="dataList fulid-container">
     <div class="block-container">
         <div class="builds-container">
              <div class="builds-title">
                <div class="timespan p-2">13.32</div>
                <div class="builds-descri p-1">who seeks after it and wants to have it</div>
              </div>
              <div class="build-img">
                <img src="@/assets/images/builds.png" alt="">
              </div>
            </div>
      </div>
   </div>

</template>

<style lang="scss">
  @import "~@/assets/scss/base/reset.scss";
  @import "~@/assets/scss/base/breakPoint.scss";
  @import "~@/assets/scss/base/color.scss";
  @import "~@/assets/scss/base/font.scss";
  @import "~@/assets/scss/mixin/mixin.scss";
  // @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700&display=swap');
  .dataList.fulid-container.sands-bg{
    background-image: url('~@/assets/images/sandBG.svg');
    background-repeat: repeat-x repeat-y;
  }
  .dataList.fulid-container {

    .block-container{
      // outline: 2px solid green;
    }
    .data-container {
      // outline: 2px pink solid;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      justify-content: center;
      justify-items: center;
      gap: 45px 25px;
      padding :72px 0;
      @include pad() {
        grid-template-columns: repeat(2, 1fr);
      }

      .dataBox {
        max-width: 178px;
        width: 100%;
        height: 112px;
        background-color: white;
        box-shadow: 0px 8px 0px #EDEEF0;

        display: flex;
        justify-items: center;
        justify-content: center;
        align-items: center;
        position: relative;

        cursor: pointer;
        .certContainer{
          position: absolute;
          top: -35%;
          left: 50%;
          transform: translateX(-50%);

          width: 65px;
          height: 100px;
          .level-title{
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%,-50%);
            text-align: center;
            color: white;
          }

        }
        .amount-tag{
          padding: 2px 6px;
          position: absolute;
          right: 5%;
          top: 15%;

          background: #FAFAFA;
        }
          

       
        &>h5{
          margin-top: 45px;
         
          font-weight: 700;
          font-size: 18px;
          line-height: 125%;
          letter-spacing: -1px;
        }
      }


       .dataBox.levelA{

          .certContainer{
            background-image: 
              url('~@/assets/images/certificateA.svg'),
              url('~@/assets/images/certificateA_L.svg'),
              url('~@/assets/images/certificateA_R.svg');
            background-size: contain,auto,auto;
            background-position:center, 2px 52px,33px 52px;
            background-repeat:no-repeat,no-repeat,no-repeat ;
          }

          .cert-title,
          .amount-tag{
            @extend .p-6;
          }
          .amount-tag{
            border: 1px solid $primary-6;
          }
        }
        .dataBox.levelD{
          .certContainer{
            background-image: 
              url('~@/assets/images/certificateD.svg');
            background-size: contain;
            background-position:center;
            background-repeat:no-repeat; 
          }
          .cert-title,
          .amount-tag{
            @extend .p-7;
          }
          .amount-tag{
            border: 1px solid $primary-7;
          }
        }
    }

    .builds-container{
      // outline: 2px solid orange;
      margin: 20px 0;
      .builds-title{
        max-width: 275px;
        min-height: 85px;
        margin: 15px auto;
        font-weight: 700;
        font-size: 20px;
        line-height: 28px;
        text-align: center;

        position: relative;

        &::before{
          content: '';
          display: block;
          position: absolute;
          top: 0%;
          left: -15%;
          width: 120px;
          height: 100px;
          background: linear-gradient(72deg, transparent 49.5%, #204379 49.5%, #204379 50.3%, transparent 50.3%);
        }
        &::after{
          content: '';
          display: block;
          position: absolute;
          top: 0%;
          right: -15%;
          width: 120px;
          height: 100px;
          background: linear-gradient(-72deg, transparent 49.5%, #204379 49.5%, #204379 50.3%, transparent 50.3%);
        }
      }
    }
  }
</style>