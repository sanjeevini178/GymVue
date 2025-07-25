<script setup>
import Layout from './components/layouts/Layout.vue';
import Dashboard from './components/pages/Dashboard.vue';
import Welcome from './components/pages/Welcome.vue';
import Workout from './components/pages/Workout.vue';
import { computed, onMounted, ref } from 'vue';
import { workoutProgram } from './utils';

const defaultData = {}

for (let workoutIdx in workoutProgram) {
  //iterating over every workout

  const workoutData = workoutProgram[workoutIdx]
  defaultData[workoutIdx] = {} // initialise workout obj

  for (let e of workoutData.workout)  {
    defaultData[workoutIdx][e.name] = ''
  }
}
const selectedDisplay = ref(1)
const data = ref(defaultData) // creating a stateful variable
// {1-30: {exercise: '', ...}}
const selectedWorkout = ref(-1)

const isWorkoutComplete = computed(() => {
  const currWorkout = data.value?.[selectedWorkout.value]
  if (!currWorkout) { return false } //guard clause to exit function

  const isCompleteCheck = Object.values(currWorkout).every(ex => !!ex)
  console.log('ISCOMPLETE: ', isCompleteCheck)
  return isCompleteCheck

})

const firstIncompleteWorkoutIdx = computed(() => {
  const allWorkouts = data.value
  if (!allWorkouts) { return -1 }

  for (const [index, workout] of Object.entries(allWorkouts)) {
    const isComplete = Object.values(workout).every(ex => !!ex)
    if (!isComplete) {
      return parseInt(index)
    }
    
  }
  return -1 // all are complete
})
function handleChangeDisplay(idx) {
  selectedDisplay.value = idx
}

function handleSelectWorkout(idx) {
  selectedDisplay.value = 3
  selectedWorkout.value = idx
}

function handleSaveWorkout() {
  // save the current data snapshot to local storage in order to retrieve it next time
  localStorage.setItem('workouts', JSON.stringify(data.value))
  // show the dashboard
  selectedDisplay.value = 2
  console.log(selectedDisplay)
  //deselect a workout
  selectedWorkout.value = -1
}

function handleResetPlan() {
  selectedDisplay.value = 2
  selectedWorkout.value = -1
  data.value = defaultData
  localStorage.removeItem('workouts')
}

onMounted(() => {
  if (!localStorage) {return}
  if (localStorage.getItem('workouts')) {
    const savedData = JSON.parse(localStorage.getItem('workouts'))
    data.value = savedData
    selectedDisplay.value = 2
  }
}) 

 </script>

<template>
  <Layout>
    <!-- Page 1 -->
     <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay == 1"/>
     <!-- Page 2 -->
     <Dashboard :handleResetPlan="handleResetPlan" :firstIncompleteWorkoutIdx="firstIncompleteWorkoutIdx" :handleSelectWorkout="handleSelectWorkout" v-if="selectedDisplay == 2"/>
    <!-- PAGE 3 -->
    <Workout :handleSaveWorkout="handleSaveWorkout" :isWorkoutComplete="isWorkoutComplete" :data="data" :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]"/>
  </Layout>
  
</template>

<style scoped>

</style>
