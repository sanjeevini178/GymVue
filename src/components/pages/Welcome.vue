<script setup>

    defineProps({
        handleChangeDisplay: Function
    })
 </script>

<template>
    <section id="welcome">
        <div class="benefits">
            <h2>Complete this program<br/> if you want to...</h2>
            <div>
                <p>✅ Follow a simple routine with proven results. </p>
                <p>✅ Get fit, strong and healthy at your own pace! </p>
                <p>✅ Learn more about gym, training and technique. </p>
            </div>
        </div>
        <div>
            <h3>Training Plan</h3>
            <p>This training plan has a structure known as the 
                <strong>Bro Split</strong>
            </p>
            <h5><i>Push &rarr; Pull &rarr; Legs &rarr; Repeat &rarr;</i></h5>
        </div>
        <div class="card challenge">
            <h3>🔥 Your challenge</h3><p> COmplete all the workouts and track your progress along the way!</p>
            <p>Do you accept?</p>
            <button @click="() => handleChangeDisplay(2)">Begin &rarr;</button>
        </div>
    </section>
</template>

<style scoped>
    #welcome,
    .challenge,
    .benefits {
        display: flex;
        flex-direction: column; 
    }

    #welcome {
        gap: 1.5rem;
    }

    .benefits {
        gap: 0.5rem;
    }

    .challenge {
        gap: 0.25rem;
    }

    @media (min-width: 640px) {
        #welcome {
            gap: 2rem;
            padding: 1rem 0;
        }

        .benefits {
            gap: 1rem;
        }
    }
</style>
