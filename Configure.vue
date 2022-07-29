<!-- Displays the configuration -->

<script setup>
 
  const props = defineProps({
    length: Number,
    numbers: Boolean,
    uppercase: Boolean,
    special: Boolean,
    extra: Boolean,
    refresh: Function,
  })

  // Emitted Events.
  const emit = defineEmits(['updateProp'])

  // Emits a checkbox event.
  function emitCheckbox( prop, target ) {
    emit( 'updateProp', prop, target.checked );
    props.refresh();
  }
  
   // Emits a value event.
  function emitNumber( prop, target ) {
    emit( 'updateProp', prop, parseFloat(target.value) );
    props.refresh();
  }
</script>

<template>
	<form @submit.prevent="refresh">
      <h3>Customize your password</h3>
 
      <div class="range-wrapper">
           <label class="range-label" for="password-length"> Password Length</label>
           <div class="range-inner">
               <input
                      :value="length"
                      class="range-number"
                      step="1"
                      id="password-length"
                      type="number"
                      min="0"
                      max="100"
                      @change="emitNumber('length', $event.target)"
                      >
              <input
                     type="range"
                     min="5"
                     max="100"
                     :value="length"
                     @change="emitNumber('length', $event.target)"
                     >
             </div>
       </div>
 
       <div class="checkboxes-wrapper">
           <p>
             <label class="checkbox">
                   <input
                       :checked="uppercase"
                       type="checkbox"
                       @change="emitCheckbox('uppercase', $event.target)"
                      >
                   Uppercase
                </label>
         </p>
               
         <p>
               <label class="checkbox">
                   <input
                       :checked="numbers"
                       type="checkbox"
                       @change="emitCheckbox('numbers', $event.target)"
                      >
                   Numbers
                </label>
         </p>

         <p>
           		<label class="checkbox">
                   <input
                       :checked="special"
                       type="checkbox"
                       @change="emitCheckbox('special', $event.target)"
                      >
                   Symbols
                </label>
         </p>
         
         <p>
               <label class="checkbox">
                   <input
                       :checked="extra"
                       type="checkbox"
                       @change="emitCheckbox('extraSpecial', $event.target)"
                      >
                   Special Chars
                </label>
          </p>
       </div>
    </form>
</template>

<style scoped>
  * {
    box-sizing: border-box;
  }
  form {
        background-color: #fff;
        border: 1px solid #eaeaea;
        border-radius: 5px;
        box-shadow: 0 2px 8px rgb(0 0 0 / 15%);
        margin: 0 auto 15px;
        max-width: 800px;
        display: flex;
        flex-wrap: wrap;
        padding: 30px 40px;
  }

  h3 {
    padding: 0;
    margin: 0;
    font-weight: 900;
    border-bottom: 2px solid #f0f2f5;
    line-height: 2.7rem;
    margin-bottom: 26px;
    flex-shrink: 0;
    font-size: 1.75rem;
    width: 100%;
  }
  
  .range-wrapper {
    display: block;
    padding-right: 40px;
    width: 50%;
    margin-bottom: 40px;
  }
  
  .checkboxes-wrapper {
			width: 50%;
  }
</style>
