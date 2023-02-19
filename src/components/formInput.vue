<script>
import { ref, reactive } from 'vue';
export default {
    setup() {
    const storeDataList = ref(['stroe1', 'stroe2', 'stroe3'])
    // const checklist = ref([false, false, false, false, false])
    const reslutF = ref(false)
    const checklist = ref([true, true, true, true, true])
    const userInput = reactive({
      store: '',
      name: '',
      phone: '',
      amount: '',
      payment: 'digtal payment'
    })

    const vaildName = () => {
      let nameRule = new RegExp('^[\u4e00-\u9fa5]+$|^[a-zA-Z\s]+$');
      // console.log(`after`, nameRule.test(userInput.name.trim()))
      return nameRule.test(userInput.name.trim())
    }

    const vaildPhone = () => {
      let phoneRule = new RegExp("^09\\d{8}$");
      // console.log(`after`, phoneRule.test(userInput.phone))
      return phoneRule.test(userInput.phone);
    }

    const vaildAmount = () => {
      return parseInt(userInput.amount) > 0;
      // return false
    }
    console.log(vaildName());
    console.log(vaildPhone());
    console.log(vaildAmount());
    const submitCheck = () => {
      console.log(`check form is vaild`)

      for (const result in checklist.value) {
        // console.log(result)
        console.log(checklist.value[result])
        if (checklist.value[result]) {
          reslutF.value = true
        } else {
          reslutF.value = false
          // console.log(result)
          break;
        }

      }

      if (reslutF) {
        // console.log(reslutF)
        // console.log(`sucessful`)
        form_btn.classList.remove('btn-fail')
        form_btn.classList.add('btn-success')
      } else {
        // console.log(`fail`)
        form_btn.classList.remove('btn-success')
        form_btn.classList.add('btn-fail')
      }




    }
    return {
      userInput, storeDataList, checklist, reslutF,
      submitCheck,
      // 驗證
      vaildName, vaildPhone, vaildAmount
    }
  }
}
</script>

<template>
  <div class="formInput fulid-container">
     <div class="block-container">
        <div class="formInputer br-2 b-shadow bradius-20" id="formInputer">
          <h5 class="formTitle p-2 bradius-20">Form</h5>
          <div class="input">
            <label for="input-store" class="p-1">store<span style="color:red">*</span></label>
            <select placeholder="placeholder text" id="input-store" class="bradius-20">
              <option :value="store" v-for="store in storeDataList">{{ store }}</option>
            
            </select>
          </div>
           <div class="input">
              <label for="input-name" class="p-1">name<span style="color:red">*</span></label>
              <input type="text" placeholder="placeholder text" id="input-name" class="bradius-20" v-model="userInput.name">

              <span v-if="!vaildName()" class="error">required</span>
            </div>
             <div class="input">
              <label for="input-phone" class="p-1">phone<span style="color:red">*</span></label>
              <input type="text" placeholder="placeholder text" id="input-phone" class="bradius-20" v-model="userInput.phone" maxlength="10">
              <span v-if="!vaildPhone()" class="error">required</span>
            </div>
             <div class="input">
              <label for="input-amount" class="p-1">Amount of consumption<span style="color:red">*</span></label>
              <input type="number" placeholder="placeholder text" id="input-amount" class="bradius-20" v-model.amount="userInput.amount">
               <span v-if="!vaildAmount()" class="error">required</span>
            </div>
             <div class="input">
              <label for="input-pay" class="p-1">payment<span style="color:red">*</span></label>
              <select placeholder="placeholder text" id="input-pay" class="bradius-20" v-model="userInput.payment">
                <option value="digtal payment" selected>digtal payment</option>
                <option value="ATM">ATM</option>
              </select>
            </div>
        </div>
        <button class="form-btn b-shadow">submit</button>
        <p class="sub-title error">
          This person does not exist
        </p>
        <!-- <button class="form-btn btn-success b-shadow">submit</button> -->
        <!-- <button class="form-btn btn-fail b-shadow">submit</button> -->
     </div>
  </div>
</template>

<style lang="scss">
  @import "~@/assets/scss/base/reset.scss";
  @import "~@/assets/scss/base/breakPoint.scss";
  @import "~@/assets/scss/base/color.scss";
  @import "~@/assets/scss/base/font.scss";
  @import "~@/assets/scss/mixin/mixin.scss";
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700&display=swap');
  
  .formInput.fulid-container{
    // outline: 2px red solid;
    .block-container{
      // outline: 2px solid orange;
    }
    .formInputer{
      padding: 40px 20px;
      position: relative;
      max-width: 808px;
      border: 2px solid  $primary-2;
      background-color: #fff;

      @include pad() {
        max-width: 720px;
      }
      @include mobile() {
        max-width: 366px;
      }

      .formTitle{
        position: absolute;
        left: 50%;
        top: -5%;
        transform: translateX(-50%);
        font-weight: 700;
        line-height: 125%;
        padding: 10px 20px;
        user-select: none;
        background-color: white;
        border:2px solid $primary-2;
        &::before{
          content: '';
          display: block;
          position: absolute;
          left: -15px;
          top:-10px;

          background-image: url('~@/assets/images/turtle.png');
          background-position: 90px 10px;
          background-repeat:no-repeat;
          height: 70px;
          width: 165%;
        }
      }
      .input{
        &+.input{
          margin: 16px 0;
        }
        
        label{
          display: block;
          font-weight: 400;
          font-size: 16px;
          line-height: 140%;
          text-align: left;
          margin-bottom: 4px;

          span{
            margin-left: 3px;
          }
        }

        &>select,
        &>input{
          width: 100%;
          height: 57px;
          background: #FFFFFF;
          border: 1px solid #204379;
          padding: 8px 16px; 
        }
        &>#input-amount::-webkit-outer-spin-button,
        &>#input-amount::-webkit-inner-spin-button{
          -webkit-appearance: none;
          margin: 0;
        }
        &>#input-amount{
            -moz-appearance: textfield;
        }
        input#input-amount:hover,
        input#input-amount:focus {
            -moz-appearance: number-input;
        }
        &>select{
          -webkit-appearance: none;
          -moz-appearance: none;
          appearance: none;
          cursor: pointer;
          background-image: url('~@/assets/images/arrow.png');
          background-repeat: no-repeat;
          background-position: 97% center;

          &>option{
            padding: 10px;
            display: block;
            font-weight: 400;
            font-size: 16px;
            line-height: 140%;

            max-width: 50px;
            margin: -10px;
          }
        }
      }

      .error{
        color: red;
        display: block;
        line-height: 1.25;
        text-align: left;
      }
    }
  }
</style>