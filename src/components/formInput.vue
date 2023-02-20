<script>
import { ref, reactive,computed } from 'vue';
export default {
    setup() {
    // get dom with input(name_ref, phone_ref, amount_ref)
    const name_ref = ref(null);
    const phone_ref = ref(null);
    const amount_ref = ref(null);
    const payment_ref = ref(null);
    const form_btn = ref(null);
    const stroe_DatalistDOM = ref(null);
      
    // data and userInput
    const storeDataList = reactive(['stroe1', 'stroe2', 'stroe3']);
    let storeFilter = reactive(['stroe1', 'stroe2', 'stroe3'])
    const reslutF = ref(false);
    // let checklist = reactive([true, false, false, false, false])
    let checklist = reactive({store:false, name:false, phone:false, amount:false, payment:false})
    // const checklist = ref([true, true, true, true, true]);
    const userInput = reactive({
      store: '',
      name: '',
      phone: '',
      amount: '',
      payment: ''
    })

    const blurCheck = (str) => {
      // console.log(`blur`,str)
      if(str == 'name'){
        const check = vaildName()
        check ? name_ref._rawValue.classList.remove('vaildError'): name_ref._rawValue.classList.add('vaildError');
      }else if(str == 'phone'){
        const check = vaildPhone();
        check ? phone_ref._rawValue.classList.remove('vaildError') : phone_ref._rawValue.classList.add('vaildError');
      }else if(str == 'amount'){
        const check = vaildAmount();
        check ? amount_ref._rawValue.classList.remove('vaildError') : amount_ref._rawValue.classList.add('vaildError');
      }else if(str == 'payment'){
        const check = vaildPayment();
        check ? payment_ref._rawValue.classList.remove('vaildError') : payment_ref._rawValue.classList.add('vaildError');
      }
    }

    const stroeFoucs =()=>{
     document.querySelector('#input-store').focus()
      if(stroe_DatalistDOM._rawValue.className.includes('d-none')){
        stroe_DatalistDOM._rawValue.classList.remove('d-none');
      }
    }

    // const stroeBlur = () => { 
    //   if (!stroe_DatalistDOM._rawValue.className.includes('d-none')) {
    //     改用CSS 處理
    //     stroe_DatalistDOM._rawValue.classList.add('d-none');
    //   }
    // }

    const vaildStore = ()=>{
      let result = false
      let temp =  storeFilter.filter(el => el === userInput.store)
      console.log(temp)
      console.log(`length`, temp.length)
      if(temp.length !== 0 ){
        result = true
      } 
      console.log(`result`,result)
      return result
    }
    const vaildName = () => {
      let nameRule = new RegExp('^[\u4e00-\u9fa5]+$|^[a-zA-Z\s]+$');
      // console.log(`after`, nameRule.test(userInput.name.trim()))
      return nameRule.test(userInput.name.trim());
    }

    const vaildPhone = () => {
      let phoneRule = new RegExp("^09\\d{8}$");
      // console.log(`after`, phoneRule.test(userInput.phone))
      return phoneRule.test(userInput.phone);
    }

    const vaildAmount = () => {
      return parseInt(userInput.amount) > 0;
    }

    const vaildPayment =()=>{
      // console.log(userInput.payment.trim() !== '')
       return userInput.payment.trim() !==''
    }
    
    const clicklistItem = (item)=>{
      console.log(`cc`, item)
      userInput.store = item
    }
    const filterKW = computed(()=>{
      // console.log(userInput.store)
      // console.log(`2`, storeFilter.filter(el => el.includes(userInput.store)))
      return storeFilter.filter(el=>el.includes(userInput.store))
    })


    const submitCheck = () => {
      console.log(`check form is vaild`);
      reslutF.value = false
      checklist = reactive({ store: false, name: false, phone: false, amount: false, payment: false })
      // 驗證格式
      checklist.store = vaildStore()
      checklist.name = vaildName();
      checklist.phone = vaildPhone();
      checklist.amount = vaildAmount();
      checklist.payment = vaildPayment();
      // console.log(checklist)

      // 檢查最終結果
      let count = 0;
      for (const result in checklist) {
        // console.log(result,":",checklist[result])
        if (checklist[result] === true) {
          // console.log(`for in true add count`)
          count++
        }else{
          // console.log(`for in false~ do noting`)
        }
      }
      const vaildCheck_length = 5
      if( parseInt(count) === parseInt(vaildCheck_length) ){
        reslutF.value = true;
      }
      
      console.log('finsh resltf:~',reslutF.value)
      // 清空樣式
      form_btn._rawValue.classList.remove('btn-fail');
      form_btn._rawValue.classList.remove('btn-success');
       
      if(reslutF.value) {
        // console.log('active:~ success')
        form_btn._rawValue.classList.add('btn-success');
      } else {
        // console.log('active:~ fail')
        form_btn._rawValue.classList.add('btn-fail');
      }

    }
    return {
      // dom elemnt
      name_ref, phone_ref, amount_ref, payment_ref, form_btn,
      stroe_DatalistDOM,

      // stroe Datalist
      stroeFoucs, 
      // stroeBlur,
      //filter result
      storeFilter,
      // vaildtor 
      userInput, storeDataList, checklist, reslutF,
      submitCheck, clicklistItem, filterKW,
      
      vaildStore,vaildName, vaildPhone, vaildAmount, vaildPayment,
      blurCheck, 
    }
  }
}
</script>

<template>
  <div class="formInput fulid-container">
     <div class="block-container">
        <div class="formInputer br-2 b-shadow bradius-20" id="formInputer">
          <h5 class="formTitle p-2 bradius-20">Form</h5>
          <div class="multi-select input">
            <label for="input-store" class="p-1">store<span class="p-2">*</span></label>
            <div class="arrow" @click="stroeFoucs()"></div> 
            <!-- <select placeholder="placeholder text" id="input-store" class="bradius-20">
              <option :value="store" v-for="store in storeDataList">{{ store }}</option>
            </select> -->
            <input type="text" class="bradius-20" placeholder="placeholder text" id="input-store" @focus="stroeFoucs()" @input="seachKW"
           v-model="userInput.store"/>
            <!-- @blur="stroeBlur()" -->
            <ul ref="stroe_DatalistDOM" class="d-none" >
              <li v-for="store in filterKW" :value="store" @click="clicklistItem(store)">{{ store }}</li>    
            </ul>
            <!-- <span class="error" v-if="filterKW.length == 0 || userInput.store== ''">store format error</span> -->
            <span class="error" v-if="!vaildStore()">required</span>
          </div>
           <div class="input">
              <label for="input-name" class="p-1">name<span class="p-2">*</span></label>
              <input type="text" placeholder="placeholder text" id="input-name" class="bradius-20" v-model="userInput.name" @blur="blurCheck('name')" ref="name_ref">

              <span v-if="!vaildName()" class="error">required</span>
            </div>
             <div class="input">
              <label for="input-phone" class="p-1">phone<span class="p-2">*</span></label>
              <input type="text" placeholder="placeholder text" id="input-phone" class="bradius-20" v-model="userInput.phone" maxlength="10" @blur="blurCheck('phone')" ref="phone_ref">
              <span v-if="!vaildPhone()" class="error">required</span>
            </div>
             <div class="input">
              <label for="input-amount" class="p-1">Amount of consumption<span class="p-2">*</span></label>
              <input type="number" placeholder="placeholder text" id="input-amount" class="bradius-20" v-model.amount="userInput.amount" @blur="blurCheck('amount')" ref="amount_ref">
               <span v-if="!vaildAmount()" class="error">required</span>
            </div>
             <div class="input">
              <label for="input-pay" class="p-1">payment<span class="p-2">*</span></label>
              <select placeholder="placeholder text" id="input-pay" class="bradius-20" v-model="userInput.payment" @blur="blurCheck('payment')" ref="payment_ref">
                <option value="digtal payment" selected>required</option>
                <option value="ATM">ATM</option>
              </select>
              <span v-if="!vaildPayment()" class="error">required</span>
            </div>
        </div>
        <button class="form-btn b-shadow" ref="form_btn" @click="submitCheck">submit</button>
        <p class="sub-title error" v-if="!reslutF">
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

          transform: translate(18px, -11px) rotate(8deg);
          animation: movePosition 6s infinite ease-in-out alternate;

          @keyframes movePosition {
            0% {
              transform : translate(18px, -11px) rotate(8deg);
            }
            27% {
              transform : translate(12px, 7px) rotate(-10deg);
            }
            77%{
               transform : translate(5px, 10px) rotate(-7deg);
            }
            100% {
               transform: translate(18px, -11px) rotate(8deg);
            }
          }
        }
        &::before{
          
        } 
      }
      .multi-select.input {
        position: relative;
        width: 100%;
        height: 57px;
        margin-bottom: 48px;
        .arrow{
          position: absolute;
          bottom: -50%;
          height: 60px;
          width: 100%;
          
          &::after{
            content: '';
            display: block;
            position: absolute;
            right: 1%;
            top: 5%;
            cursor: pointer;
            background-image: url('~@/assets/images/arrow.png');
            background-repeat: no-repeat;
            background-position: center center;
            width: 30px;
            height: 50px;
            z-index: 10;
          }
        }
        
        input {
          position: relative;
          width: 100%;
          height: 57px;
          background: #FFFFFF;
          border: 1px solid #204379;
          padding: 8px 16px; 
          z-index: 9;
         
          &:not(:focus) + ul{
            opacity: 0;
            user-select: none;
           
          }
        }
        ul {
          position: absolute;
         
          border: 1px solid #ccc;
          border-top: none;
          list-style: none;
          background-color: #fff;
          // overflow-y: scroll;
          // max-height: 150px;
          width: 98%;
          left: 1.5%;
          // display: none;

          li {
            padding: 5px;
            cursor: pointer;
          }
          li:hover {
            background-color: #eee;
          }
          li.selected {
            background-color: #337ab7;
            color: #fff;
          }
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
        &>select:focus,
        &>input:focus{
          outline: 3px solid #93BBF9;
          border: transparent;
        }
        &>select.vaildError,
        &>input.vaildError{
          outline: 3px solid #E06D6D;
          border: transparent;
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
        color: #E06D6D;
        display: block;
        line-height: 1.25;
        text-align: left;
      }
    }
  }
</style>