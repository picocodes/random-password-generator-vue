<!-- Displays the password -->

<script setup>

  import { computed } from 'vue'
 
  // Define product_id prop.
  const props = defineProps({
    password: String,
    refresh: Function,
  })

  // Calculates a password's strength.
  function calculatePasswordStrength( password ) {
    let strength = 0;
    if ( password.length > 6 ) {
      strength++;
    }
    if ( password.length > 10 ) {
      strength++;
    }
    if ( password.match(/[a-z]/) ) {
      strength++;
    }
    if ( password.match(/[A-Z]/) ) {
      strength++;
    }
    if ( password.match(/\d/) ) {
      strength++;
    }
    if ( password.match(/\W|_/) ) {
      strength++;
 
      if ( password.length > 5 ) {
      strength++;
    } 
    }
  	return strength;
}

// Returns the color to use for the strength meter.
function passwordStrengthMeterColor( strength ) {
	const colors = [ 'red', 'orange', 'yellow', '#9e9d24', 'lime', 'green' ];
	return colors[ Math.min( strength, colors.length - 1 ) ];
}

// Returns the width to use for the strength meter.
function passwordStrengthMeterWidth( strength ) {
	const colors = [ '10%', '25%', '40%', '70%', '90%', '105%' ];
	return colors[ Math.min( strength, colors.length - 1 ) ];
}

 // Computed styles.
const strengthStyles = computed(() => {
  const strength = calculatePasswordStrength(props.password);
  return {
    width: passwordStrengthMeterWidth(strength),
    backgroundColor: passwordStrengthMeterColor(strength),
  }
})
</script>

<template>
   <div class="generated-password">
       <form>
           <input v-model="password" spellcheck="false" class="the-password" type="text" />
        </form>
        <div class="icon-wrapper">
            <button class="copy-icon">
               <i class="fas fa-copy"></i>
            </button>
            <button class="refresh-icon" @click.prevent="refresh">
               <i class="fas fa-refresh"></i>
            </button>
         </div>
         <div class="strength-wrapper">
             <div class="password-strength" :style="strengthStyles"></div>
         </div>
    </div>
</template>

<style scoped>

  .generated-password {
        background-color: #fff;
        border-radius: 5px;
        box-shadow: 0 2px 8px rgb(0 0 0 / 15%);
        border: 1px;
        border-bottom: 0;
        display: flex;
        max-width: 800px;
        position: relative;
        height: 115px;
        margin: 0 auto 20px;
        padding: 34px;
   }

  form {
			flex-grow: 1;
  }
  
  input {
        background-color: #fff;
        border-radius: 8px;
        font-family: monospace;
        box-shadow: none;
        border: 0;
        color: #000;
        display: block;
        font-size: 2.25rem;
        height: 50px;
        left: 0;
        max-width: 100%;
        padding-left: 44px;
        padding-right: 108px;
        position: absolute;
        text-align: left;
        top: 50%;
        transform: translateY(-50%);
        width: 100%;
  }
  
  .icon-wrapper {
        height: 32px;
        padding: 0;
        position: absolute;
        right: 30px;
        top: 50%;
        transform: translateY(-50%);
        width: 76px;
        display: flex;
        flex-shrink: 0;
  }
  
  button {
        background-color: #fff;
        background-position: 50%;
        background-repeat: no-repeat;
        border: 0;
        display: inline-block;
        height: 31px;
        position: relative;
        -webkit-tap-highlight-color: rgba(0,0,0,0);
        width: 32px;
        margin-right: 8px;
  }
  
  i {
    font-size: 24px;
    color: #454545;
  }
  
  .strength-wrapper {
        background-color: #f5f5f5;
        border-bottom-left-radius: 5px;
        border-bottom-right-radius: 5px;
        bottom: -1px;
        height: 11px;
        left: 0;
        overflow: hidden;
        position: absolute;
        transition: background-color .63s;
        width: 100%;
   }
  
  .password-strength {
        background-color: #368149;
        border-bottom-right-radius: 5px;
        border-top-right-radius: 5px;
        bottom: 1px;
        height: 10px;
        left: 0;
        position: absolute;
        transition: width .63s,background-color .2s;
        width: 0;
    }
</style>
