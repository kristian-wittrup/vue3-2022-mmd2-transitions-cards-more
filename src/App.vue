<template>
  <div id="toplevel-wrapper" class="container-fluid d-flex min-vh-100 flex-column">
    <NavigationComponent />
    <router-view v-slot="{ Component }">
      <transition name="route" mode="out-in">
        <component :is="Component"></component>
      </transition>
    </router-view>
    <FooterComponent class="row mt-auto gx-0" /> <!-- fixed-bottom (class) -->
  </div>  
</template>

<script>
import gsap from 'gsap'

import NavigationComponent from '@/components/NavigationComponent.vue'
import FooterComponent from '@/components/FooterComponent.vue'

export default {
  setup() {

    const beforeEnter = (el, done) => {
      console.log("before enter")
      gsap.from(el, { // with GSAP .from()
        onComplete: done
      })
    }
    const enter = (el, done) => {  // add done, to have vue wait with firing afterEnter
      gsap.set(el, {
				x: window.innerWidth * 1.5,
				scale: 0.8,
        transformOrigin: '50% 50%',
      })
      gsap.to(el,  {
        delay: 0.3, // add delay to match leave animation
        x: 0,
        duration:.5,
        ease: 'Power4.easeOut',
    
      })
      gsap.to(el,  {
        duration: 0.4,
				scale: 1,
        ease: 'Power4.easeOut',
        onComplete: done
			});
    }
    
     const leave = (el, done) => {
			gsap.fromTo(el, {  
        autoAlpha: 1  // fade out object (same af opacity almost) 
                      //=> if an object already exists its better to use use AutoAlpha to improve browser rendering
			}, {
				autoAlpha: 0,
        duration: 0.1,
				ease: 'Power4.easeOut',
				onComplete: done
			});
		}	
 
  return { enter, beforeEnter, leave }
   
  },
  components: {
    FooterComponent,
    NavigationComponent
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
/*  text-align: center;  Remove, or all is centered  */ 
  color: #2c3e50;

}

#toplevel-wrapper { 
  padding:0; /* Added */
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

/* route transitions */
.route-enter-from {
  opacity: 0;
  transform: translateX(100px);
}
.route-enter-active {
  transition: all 0.3s ease-out; 
}
.route-leave-to {
  opacity: 0;
  transform: translateX(-100px);
}
.route-leave-active {
  transition: all 0.3s ease-in; 
}
</style>
