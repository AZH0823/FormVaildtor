
<script>
export default {
  setup() {
    // scroll 動畫參數
    const easeInQuad = function (x) {
      return 1 - Math.pow(1 - x, 4);
    };

    // scrolling 動畫手刻
    const scrolltoVeiew = () => {

      const top = document.querySelector("#formInputer").getBoundingClientRect().top;
      const startPos = window.pageYOffset;
      const diff = top;
      const duration = 1200;
      const yOffset = -75;

      let startTime = null;
      let requestId;

      const loop = function (currentTime) {
        if (!startTime) {
          startTime = currentTime;
        }

        // Elapsed time in miliseconds
        const time = currentTime - startTime;

        const percent = Math.min(time / duration, 1);
        window.scrollTo(0, startPos + yOffset + diff * easeInQuad(percent));

        if (time < duration) {
          // Continue moving
          requestId = window.requestAnimationFrame(loop);
        } else {
          window.cancelAnimationFrame(requestId);
        }
      };
      requestId = window.requestAnimationFrame(loop);

    }
    return {
      scrolltoVeiew, easeInQuad
    }
  }
}
</script>

<template><!-- <h1 class="p-1">第一區塊</h1> -->
  <div class="intro fulid-container">
    <div class="block-container">
      <h2 class="white">There is no one</h2>
      <h2 class="white">who loves pain</h2>
      <button class="form-btn b-shadow" @click="scrolltoVeiew">Form</button>
      <div class="para-desc">
        <img src="@/assets/images/sup01.svg" class="sup sup01" alt="" />
        <img src="@/assets/images/sup02.svg" class="sup sup02" alt="" />
        <h5 class="para-icons p-1 bold">paragraph</h5>
        <ul>
          <li>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</li>
        </ul>
        <h5 class="para-icons p-1 bold">paragraph</h5>
        <ul>
          <li>Quisque sodales leo <span class="bold underline">vitae vulputate auctor.</span>
          </li>
          <li>Proin ac justo ut nisl tincidunt imperdiet.Maecenas viverra libero a pellentesque blandit.</li>
          <li>Cras tristique tellus id leo bibendum, eu dapibus nisl accumsan.</li>
          <li>Donec ultrices sapien <span class="bold">vitae leo venenatis ullamcorper.</span></li>
        </ul>
      </div>
    </div>
    <!-- <img src="@/assets/images/seaWave.png" alt=""> -->
  </div>
</template>

<style lang="scss" >
@import "~@/assets/scss/base/color.scss";
@import "~@/assets/scss/base/reset.scss";
@import "~@/assets/scss/base/breakPoint.scss";
@import "~@/assets/scss/base/color.scss";
@import "~@/assets/scss/base/font.scss";
@import "~@/assets/scss/mixin/mixin.scss";

.intro.fulid-container {

  background-color: $primary-1;
  color: $primary-1;
  // padding:70px 0;
  min-height: 687px;
  border: 1px solid transparent;

  background-image:
    url('~@/assets/images/Linear01.png'),
    url('~@/assets/images/Linear02.png'),
    url('~@/assets/images/Linear03.png'),
    url('~@/assets/images/seaWave.png');
  background-position: 20% 20%, 75% 30%, 45% 85%, 0% 101%;
  background-repeat: repeat no-repeat, repeat no-repeat, repeat no-repeat;
  background-size: 125%, 125%, 125%, auto;
  animation: moveBgPosition 60s infinite linear alternate;

  @keyframes moveBgPosition {
    from {
      background-position-x: 20%, 75%, 45%, 0%;
    }

    to {
      background-position-x: 195%, 210%, 135%, 220%;
    }
  }

  .para-desc {
    padding: 24px 16px;

    background: $primary-3;
    border: 2px solid $primary-2;
    border-radius: 20px;

    position: relative;

    // sup img
    .sup {
      position: absolute;

      &.sup01 {
        right: 0%;
        top: -10%;
      }

      &.sup02 {
        left: 5%;
        bottom: -15%;

      }
    }

    ul {
      // outline: 2px red solid;
      padding: 0 16px;
      margin: 0 auto;

      li {
        // @extend .title-16;
        list-style-type: decimal;
        list-style-position: outside;
        align-self: stretch;
        text-align: left;
        line-height: 180%;

        @include mobile() {
          text-align: inherit;
        }
      }

      li::marker {
        display: block;
        margin-left: 20px;
      }
    }

    h5.para-icons {
      padding: 20px;
      display: inline-block;
      position: relative;
      font-weight: 700;
      line-height: 22.5px;
    }

    .para-icons::before,
    .para-icons::after {
      content: '';
      position: absolute;
      background-size: 30px 30px;
      height: 30px;
      width: 30px;
      z-index: 999;
      background-image: url('~@/assets/images/cactus.png');
      background-repeat: no-repeat;

    }

    .para-icons::before {
      left: -7.5%;
    }

    .para-icons::after {
      right: -7.5%;
    }


  }


}</style>