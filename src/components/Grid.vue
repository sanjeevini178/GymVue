<script setup>
    import { workoutProgram } from '../utils';
    console.log(workoutProgram);
    const workoutTypes = ['Push', 'Pull', 'Legs']
</script>

<template>
    <section id="grid">
        <button :key="workoutIdx" v-for="(workout, workoutIdx) in Object.keys(workoutProgram)" class="card-button plan-card">
            <div>
                <p>Day {{ workoutIdx < 9 ? '0' + (workoutIdx + 1 ): workoutIdx + 1}}</p>
                <i v-if="workoutIdx % 3 == 0" class="fa-solid fa-dumbbell"></i>
                <i v-if="workoutIdx % 3 == 1"class="fa-solid fa-weight-hanging"></i>
                <i v-if="workoutIdx % 3 == 2"class="fa-solid fa-bolt"></i>
            </div>
            <h3>{{ workoutTypes[workoutIdx % 3]}}</h3>
        </button>
    </section>
</template>

<style scoped>
    #grid {
        display: grid;
        grid-template-columns: repeat(3, minmax(0, 1fr));
        gap: 1rem;
    }

    #grid button {
        width: 100%;
    }

    .plan-card {
        display: flex;
        flex-direction: column;
    }

    .plan-card div {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 0.5rem;
    }

    .plan-card div p {
        text-align: left;
    }
    @media (min-width: 640px) {
        #grid {
            grid-template-columns: repeat(4, minmax(0, 1fr));
        }
    }
</style>
