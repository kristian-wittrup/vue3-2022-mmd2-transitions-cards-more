<template>
  <div class="about">
    <h1>This is an about pagesss</h1>
    <button v-on:click="isHidden = !isHidden">Toggle hide and show</button>
  <!--   <Transition>
      <h1 v-if="!isHidden">Hide me on click event!</h1>
    </Transition>  --> 
    <Transition name="fade">
      <h1 v-if="!isHidden">Hide me on click event!</h1>
    </Transition>  
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {
    let isHidden = ref(false)

    return {
      isHidden
    }
  }
}
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
 
}

/*
.fade-enter-active,
 {
  transition: all 0.3s ease-out;
  transition: opacity 0.5s ease;
}
.fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateX(20px);
}
*/
</style>
