<!-- cmd Vue -->
<script>
// import my 4block Component
// 表單簡介 
import formIntro from '@/components/formIntro.vue';
// 使用者驗證格式
import formInput from '@/components/formInput.vue';
// 資料渲染
import formDataList from '@/components/formDataList.vue';
// Store 畫面渲染
import formStore from '@/components/formStore.vue';

export default {
  components:{
    formIntro, formInput, formDataList, formStore
  },
}

</script>


<template>
  <formIntro></formIntro>
  <formInput></formInput>
  <formDataList></formDataList>
  <formStore></formStore>
</template>

<style lang="scss">
@import "~@/assets/scss/base/reset.scss";
@import "~@/assets/scss/base/breakPoint.scss";
@import "~@/assets/scss/base/color.scss";
@import "~@/assets/scss/base/font.scss";
@import "~@/assets/scss/mixin/mixin.scss";
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&display=swap');

body{
    background-color:$primary-4;
    font-family: 'Noto Sans TC';     
}
.fulid-container{
  width: 100%;
  // margin: 70px 0;
}
.block-container {
  max-width: 808px;
  margin: 60px auto;
  text-align: center;
  // outline: 2px solid red;
  @include pad() {
    padding: 24px;
  }
}
// class style 公用項目
  .underline {
    text-decoration: underline;
  }

  .bold {
    font-weight: bold;
  }

  .form-btn {
    max-width: 200px;
    width: 135%;
    height: 57px;
    margin: 32px auto;
    padding: 16px 20px;

    display: flex;
    align-items: center;
    justify-items: center;
    justify-content: center;

    font-weight: 700;
    font-size: 18px;
    line-height: 125%;
    letter-spacing: 0.2em;
    
    border: transparent;
    color:white;
    border-radius: 50px;
    background-color:$primary-2;
    box-shadow: 0px 0px 20px rgba(250, 163, 163, 0.91);

    cursor: pointer;
    &:hover{
      transition: .25s all;
      box-shadow: 0px 0px 25px rgba(250, 163, 163, 0.91);
    }
    &:active{
      transition: .25s all;
      background-color:lighten($primary-2,30%);
      box-shadow: 0px 4px 10px rgba(40, 35, 35, 0.35), 0px -4px 10px rgba(255, 255, 255, 0.9);
      // filter: lig(75%);
    }
    &.btn-success{
      color:$primary-6;
      position: relative;
     
      &::before{
        content: "";
        display: block;
        margin-right: 15px;

        background-image: url('~@/assets/images/Vector_sucessful.svg');
        background-repeat: no-repeat;
        background-size: contain;
        
        width: 32px;
        height: 32px;
      }
    }
    &.btn-fail{
      color:#FFE3E3;
      position: relative;
     
      &::before{
        content: "";
        display: block;
        margin-right: 15px;

        background-image: url('~@/assets/images/Vector_fail.svg');
        background-repeat: no-repeat;
        background-size: contain;
        
        width: 32px;
        height: 32px;
      }
    }     
  }
  
  .br-2{
    border: 2px solid #B57556;
  }
  .bradius-20{
    border-radius: 20px;
  }
  .b-shadow {
    box-shadow: 0px 1px 20px rgba(73, 72, 72, 0.25);
  }

h1{
  color:red;
  text-align: center;
  height: 100vh;
  
    @include pc() {   
        color: green;
    }
    @include pad() {
      color: pink;
    }
    @include mobile() {
      color: purple;
    }
}
.sub-title.error{
  color: red;
  margin: -20px;
}
</style>