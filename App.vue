<!-- Vue random password generator -->

<script>
  import ViewPassword from './ViewPassword.vue';
  import Configure from './Configure.vue';

export default {
  components: {
    ViewPassword,
    Configure
  },
  data() {
    return {
      length: 12,
      numbers: true,
      uppercase: true,
      special: false,
      extraSpecial: false,
      password: '',
    }
  },
  computed: {
    chars() {
      let chars = 'abcdefghijklmnopqrstuvwxyz';
 
      if ( this.uppercase ) {
        chars += 'ABCDEFGHIJKLMNPQRSTUVWXYZ';
      }
      
      if ( this.numbers ) {
        chars += '123456789';
      }
      
      if ( this.special ) {
        chars += '!@#$%^&*()';
      }
      
      if ( this.extraSpecial ) {
        chars += '-_[]{}<>~`+=,.;:/?|';
      }
      
      return chars;
    }
  },
  methods: {
    generatePassword() {
      this.password = '';

      for (var i = 1; i <= this.length; i++) {
        this.password += this.chars.charAt( Math.floor( Math.random() * this.chars.length ) );
      }
    },
    updateProp( prop, val ) {
      this[prop] = val;

  },
  created() {
    this.generatePassword();
  }
}
</script>

<template>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.2/css/all.min.css" integrity="sha512-1sCRPdkRXhBV2PBLUdRb4tMg1w2YPf37qatUFeS7zlBy7jJI8Lf4VHwWfZZfpXtYSLy85pkm9GaYVYMfw5BC1A==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  <h1 class="title">Generate a random password</h1>
  <ViewPassword :password="password" :refresh="generatePassword"/>
  <Configure
             :length="length"
             :numbers="numbers"
             :uppercase="uppercase"
             :extra="extraSpecial"
             :special="special"
             :refresh="generatePassword"
             @update-prop="updateProp"/>
</template>

<style>
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  }
  
  .title {
    text-align: center;
    color: #454545;
  }
</style>
