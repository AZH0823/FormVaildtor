<script>
export default {

}
</script>

<template>
  <div class="store fulid-container">
    <div class="block-container">
        <h4 class="block-store-title">Neque porro quisquam est qui dolorem!</h4>
        <div class="store-view bradius-20">
          <div class="roof">
            <img src="@/assets/images/stroe_roof.png" alt="">
          </div>
          <div class="store-title p-2">Argentina</div>
          <ul class="rate">
            <li>
              <img src="@/assets/images/stroe_start.png" alt=""> 
              adipisci velit.
            </li>
            <li>
                <img src="@/assets/images/stroe_start.png" alt=""> 
                adipisci velit.
            </li>
          </ul>
          <ul class="icon">
            <li class="icon-bg">
              <img src="@/assets/images/stroe_house.png" alt="">
            </li>
            <li class="icon-bg">
                <img src="@/assets/images/stroe_moto.png" alt="">
              </li>
              <li class="icon-bg">
                <img src="@/assets/images/stroe_gift.png" alt="">
              </li>
              <li class="icon-bg">
                <img src="@/assets/images/stroe_people.png" alt="">
              </li>
          </ul>
          <ul class="paginator">
            <li class="now"></li>
            <li></li>
            <li></li>
          </ul>
        </div>
      </div>
    </div>
</template>

<style lang="scss">
  @import "~@/assets/scss/base/color.scss";
  @import "~@/assets/scss/base/reset.scss";
  @import "~@/assets/scss/base/breakPoint.scss";
  @import "~@/assets/scss/base/color.scss";
  @import "~@/assets/scss/base/font.scss";
  @import "~@/assets/scss/mixin/mixin.scss";
  .store.fulid-container{
    border-radius: 50px 50px 0px 0px;
    background-color:  $primary-1;
    border: 1px solid transparent;
    .block-store-title{
      font-weight: 700;
      font-size: 20px;
      line-height: 200%;

      text-align: center;
      letter-spacing: 2.5px;
      color: white;
      max-width: 303px;
      
      margin: 0 auto;
      padding: 42px 0 42px;
        
    }
    .store-view{
      max-width: 340px;
      min-height: 492px;
      background: #D3D4DB;

      // outline: 2px solid red;
      position: relative;
      z-index: 1;
      margin: 0 auto;

      // fornt-bg
      &::before{
        content: '';
        display: block;
        box-sizing: border-box;
        position: absolute;
        z-index: -1;
        padding: 10px;
        left: 50%;
        top: 47.5%;
        transform: translate(-50%,-50%);
        background-color: #F7F7F8;
        border: 4.1239px solid #F7F7F8;
        opacity: 0.75;
        max-width: 320px;
        width: 90%;
        height: 432px;


        @media screen and (max-width:290px) { 
          &{
              grid-template-columns: 1fr;
              min-height: 501px;
          }
        }
      }

      // home-btn
      &::after{
        content: '';
        position: absolute;
        z-index: 2;
        bottom: 3%;
        left: 50%;
        transform: translateX(-50%);
        width: 15px;
        height: 15px;

        background: #C2C3C9;
        border: 0.877023px solid #EDEEF0;
        border-radius: 50%;
      } 
      .roof{
        // outline: 2px rgb(42, 165, 73) solid;
        position: relative;
        img{
          position: absolute;
          width: 120%;
          object-fit: cover;
          left: 50%;
          top: -30px;
          transform: translateX(-50%);
        }
      }
      .store-title{
        font-weight: 900;
        font-size: 32px;
        line-height: 200%;

        text-align: center;
        letter-spacing: 0.2em;
        z-index: 7;

        padding-top: 40px;  
        @include mobile() {
          font-size: 28px;
        }
        @media screen and (max-width:290px) { 
          &{
            font-size: 1em;
          }
        }
      }
      .rate{
        z-index: 3;
        color:#BED3E5;
        font-weight: 700;
        font-size: 12.4064px;
        line-height: 200%;
      
        text-align: center;
        letter-spacing: 0.2em;
        &>*{
          position: relative;
          z-index: 3;
        }
      }
      .icon{
        z-index: 3;
        margin: 17px 0;
        display: grid;
        // grid-template-columns:100px 100px;
        grid-template-columns: minmax(auto, 100px) minmax(auto, 100px);
        justify-items: center;
        justify-content: center;
        gap: clamp(8px,10px,20px) clamp(6px,10px,16px) ;
        cursor: pointer;
        transition: .65s all ease-in;
        
        .icon-bg{
          z-index: 3;
          position: relative;
          width: 200%;
          max-width: 80px;
          height: 80px;;  
          
          border-radius: 50%;
          background-color: #BED3E5;
          display: flex;
          align-items: center;
          justify-content: center;
          &:hover{
            filter: grayscale(80%);;
          }
          img{
            z-index: 3;

            max-height: 100%;  
            max-width: 100%; 
            width: auto;
            height: auto;
            position: absolute;  
            top: 0;  
            bottom: 0;  
            left: 0;  
            right: 0;  
            margin: auto;
            
          }
          
        }
        @media screen and (max-width:290px) { 
          &{
              grid-template-columns: 1fr;
          }
        }
      }

      .paginator{
        display: flex;
        justify-content: center;
        align-items: center;

        z-index: 6;
        width: 100%;
        min-height: 20px;
        margin-top: 20%;
        
        &>li{
          user-select: none;
          width: 4.65px;
          height: 4.65px;
          background: #9A999E;
          opacity: 0.35;
          border-radius: 50%;
          cursor: pointer;
          &+li{
            margin-left: 5px;
          }
          &.now{
              opacity: 1;
          }
        }
      }
    }
  }

</style>