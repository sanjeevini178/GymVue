<script setup>
import { gymHealthFacts } from '../../utils'
import Grid from '../Grid.vue'
const randomNumber = Math.floor(Math.random() * gymHealthFacts.length)
const todaysFact = gymHealthFacts[randomNumber];

const props = defineProps({
    handleSelectWorkout: Function,
    firstIncompleteWorkoutIdx: Number
})
 </script>

<template>
    <section id="dashboard">
        <div class="card tip-container">
            <h2> Welcome Soldier!</h2>
        <div>
            <p class="tip"><strong>Daily Tip</strong> <br/>{{ todaysFact }}</p>
        </div>
        <button @click="() => handleSelectWorkout(firstIncompleteWorkoutIdx < 0 ? 0 : firstIncompleteWorkoutIdx)">Start Workout &rarr;</button>
    </div>
    <Grid v-bind="props"/>
    </section>
</template>

<style scoped>
    .tip-container,
    .tip-container div,
    #dashboard {
        display: flex;
    }

    .tip-container, #dashboard {
        flex-direction: column;
    }

    #dashboard {
        gap: 2rem;
    }
    .tip-container {
        gap: 0.5rem;
    }

    @media (min-width: 640px) {
        .tip-container {
            gap: 1rem;
        }
    }
</style>
