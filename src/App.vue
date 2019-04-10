<template>
  <div id="app">
  
    <img alt="Vue logo" src="./assets/logo.png">
    <RoutineList msg="Welcome to Your Vue.js App"/>
  
  </div>
</template>

<script>
import RoutineList from './components/RoutineList.vue'
import UserSelect from './components/UserSelect.vue'
import CustomizeRoutine from './components/CustomizeRoutine.vue'
import CustomizeExercise from './components/CustomizeExercise.vue'
import ExerciseLibrary from './components/ExerciseLibrary.vue'

export default {
  name: 'app',
  components: {
    RoutineList,
	UserSelect,
	CustomizeRoutine, 
    CustomizeExercise,
	ExerciseLibrary
   }   
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
