<template>
    <div id="login" class="intro">
      <h1 class="intro__title">Welcome</h1>
      <form
        action="https://localhost:9000"
        method="POST"
        id="introForm"
        class="form intro__form"
        v-on:submit.prevent="sub"
      >
        <input
          type="text"
          placeholder="First name"
          id="firstName"
          v-model="firstName"
          class="intro__input"
        />
        <input
          type="text"
          placeholder="Last name"
          id="lastName"
          v-model="lastName"
          class="intro__input"
        />
        <button type="submit" id="login-button" class="intro__button">Enter to conference</button>
      </form>
    </div>
</template>

<script>

  import axios from "axios";

  const SERVER_URL = 'https://192.168.178.39:9000/';

  export default {
    data() {
      return {
        firstName: "",
        lastName: "",
      };
    },
    methods: {
      sub: function () {
        if (this.firstName !== "" && this.lastName !== "") {
          axios
            .post(SERVER_URL, {
              "firstName": this.firstName,
              "lastName": this.lastName
            })
            .catch(err => console.log('error', err))
            .finally(() => {
              this.fadeOut();
              this.goToConf();
            });
        }
      },
      fadeOut() {
        document.getElementById("introForm").classList.add('fadeOut');
        document.getElementById("login").classList.add('form-success');
      },
      goToConf() {
        setTimeout(() => this.$router.push({ name: 'conference'}), 1000);
      }
    }
  };
</script>

<style scoped lang="less">
@prim: #53e3a6;
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-weight: 300;
}
  &.form-success {
      .intro__title {
        transform: translateY(85px);
        -webkit-transition-delay: 0.5s;
        -o-transition-delay: 0.5s;
        -moz-transition-delay: 0.5s;
        transition-delay: 1s;
      }
  }
  ::-webkit-input-placeholder {
    /* WebKit browsers */
    font-family: "Source Sans Pro", sans-serif;
    color: white;
    font-weight: 300;
  }
  :-moz-placeholder {
    /* Mozilla Firefox 4 to 18 */
    font-family: "Source Sans Pro", sans-serif;
    color: white;
    opacity: 1;
    font-weight: 300;
  }
  ::-moz-placeholder {
    /* Mozilla Firefox 19+ */
    font-family: "Source Sans Pro", sans-serif;
    color: white;
    opacity: 1;
    font-weight: 300;
  }
  :-ms-input-placeholder {
    /* Internet Explorer 10+ */
    font-family: "Source Sans Pro", sans-serif;
    color: white;
    font-weight: 300;
  }

.intro {
  max-width: 600px;
  text-align: center;
  margin: auto;
  
  &__title {
    font-size: 40px;
    transition-duration: 1s;
    transition-timing-function: ease-in-put;
    font-weight: 200;
    color:#fff;
    position: relative;
  }

  &__form {
    padding: 20px 0;
    position: relative;
    z-index: 2;
  }

  &__input {
    display: block;
    appearance: none;
    outline: 0;
    border: 1px solid fade(white, 40%);
    background-color: fade(white, 20%);
    width: 250px;
    border-radius: 3px;
    padding: 10px 15px;
    margin: 0 auto 10px auto;
    display: block;
    text-align: center;
    font-size: 18px;
    color: white;
    transition-duration: 0.25s;
    font-weight: 300;
    &:hover {
      background-color: fade(white, 40%);
    }
    &:focus {
      background-color: white;
      width: 300px;
      color: @prim;
    }
  }

  &__button {
    appearance: none;
    outline: 0;
    background-color: white;
    border: 0;
    padding: 10px 15px;
    color: @prim;
    border-radius: 3px;
    width: 250px;
    cursor: pointer;
    font-size: 18px;
    transition-duration: 0.25s;
    &:hover {
      background-color: rgb(245, 247, 249);
    }
  }
}

input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus {
  -webkit-text-fill-color: @prim;
  -webkit-box-shadow: 0 0 0px 1000px #ffffff20 inset;
  transition: background-color 5000s ease-in-out 0s;
}
</style>
