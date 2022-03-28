<template>
 <div class="container-md"> <!-- switch to margin x over MD size(fluid and !fluid) -->
  <div class="row">

    <div :class="{active: isActive, 'text-color': isActive}">text</div>

    <button @click="showMeDaData()">show data</button>
    <div v-if="showData">
      loading data...
    </div>
    <div v-else class="col-12 col-sm-6 col-md-4 mb-4" v-for="projectItem in projects" :key="projectItem">
      <div class="card" style="">
        <img :src="projectItem.projectURL" class="card-img-top" alt="...">
        <div class="card-body justify-content-start">
          <h5 id="cardOne" class="card-title ">{{projectItem.projectTitle}}</h5>
          <p class="card-text">{{projectItem.projectDescription}}</p>
          <a href="#" class="btn btn-primary">Go somewhere {{projectItem.id}}</a>
        </div>
      </div>
    </div>

  

  </div>
  
</div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    let showData = ref(true)
    let isActive = ref(false)

    /* function showMeDaData() {
      showData.value = !showData.value
      isActive.value = !isActive.value
    } */

    let showMeDaData = () => {
      showData.value = !showData.value
      isActive.value = !isActive.value
    }

    let projects = ref([
      {
        id: 1,
        projectURL:"https://images.unsplash.com/photo-1572177812156-58036aae439c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8cHJvamVjdHN8ZW58MHx8MHx8&w=1000&q=80",
        projectTitle:"Card TitleOne",
        projectDescription:"Some quick example text to build up the bulk of the card's content."
      },
      {
        id:2,
        projectURL:"https://images.unsplash.com/photo-1572177812156-58036aae439c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8cHJvamVjdHN8ZW58MHx8MHx8&w=1000&q=80",
        projectTitle:"Card TitleTwo",
        projectDescription:"Lorem ipsum"
      }, 
      
    ])

    return {
      projects,
      showData,
      showMeDaData,
      isActive
      
    }
  }
}
</script>

<style scoped>
#cardOne{
  color:red
}
.active {
  background-color: khaki;
  
}
.text-color {
  color:darkviolet;
}
</style>
