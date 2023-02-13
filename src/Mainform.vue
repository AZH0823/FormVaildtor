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
  <formIntro>123</formIntro>
  <formInput>456</formInput>
  <formDataList>789</formDataList>
  <formStore>333</formStore>
</template>

<style lang="scss">
@import "@/assets/scss/reset.scss";
body{
    background-color:#E5E5E5;
}
  h1{
    color:red;
    text-align: center;
    height: 100vh;
  }
</style>