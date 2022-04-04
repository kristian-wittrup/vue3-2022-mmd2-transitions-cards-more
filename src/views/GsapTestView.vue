<template>
  <div class="container-md"> 

    <h1>Contact</h1>
    <div class="row">
      <transition-group 
        appear
        @before-enter="beforeEnter"
        @enter="enter"
       
      >
        <div v-for="(project, index) in projects" :key="project.projectTitle" :data-index="index" class="col-12 col-sm-6 col-md-4 mb-4"  >
          <div class="card" style="">
            <img :src="project.projectURL" class="card-img-top" alt="...">
            <div class="card-body justify-content-start">
              <h5 id="cardOne" class="card-title ">{{project.projectTitle}}</h5>
              <p class="card-text">{{project.projectDescription}}</p>
              <p>Category: {{project.projectCategory}}</p>
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
import getProjects from '../modules/getProjects'
import gsap from 'gsap'

export default {
  setup() {
    const { projects } = getProjects();

    const beforeEnter = (el) => {
      
      el.style.opacity = 0
      el.style.transform = 'translateY(100px)'
    }
    const enter = (el) => {
      gsap.to(el, {
        opacity: 1,
        y: 0,
        duration: 0.8,
       // onComplete: done,
       
        delay: 1 + el.dataset.index * 0.1 // add one for 1 sec delay before running through 
      }) 
    }

    return { projects, beforeEnter, enter }
  }
}
</script>

<style>
  .contact ul {
    padding: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    max-width: 400px;
    margin: 60px auto;
  }
  .contact li {
    list-style-type: none;
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    cursor: pointer;
    line-height: 1.5em;
  }
</style>