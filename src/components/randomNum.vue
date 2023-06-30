<script setup lang="ts">
import { ref, type Ref } from 'vue'

//arrays of reactive type due to updating of values
const numbers: Ref = ref([]);
const combinations: Ref = ref([]);

//generate an array of random numbers
function create() {
    generateNumbers();
}

function generateNumbers() {
    numbers.value = []; //reset array so that we don't keep adding to it
    const numCount = 8; // Number of random numbers to generate
    const min = 1; // Minimum random number
    const max = 25; // Maximum random number
    const generatedNumbers = new Set(); // Track the generated numbers and ensure no duplicates bc why not
    //higher chance of getting 21 this way

    while (generatedNumbers.size < numCount) {
        const randomNum = Math.floor(Math.random() * (max - min + 1)) + min;
        generatedNumbers.add(randomNum);
    }

    numbers.value = Array.from(generatedNumbers); // Convert the set to an array

}

function findCombinations() {
    combinations.value = []; //freshness Reset the combinations array before finding new combinations

    //use set to make sure we don't have duplicate combinations
    const visited = new Set();

    for (let i = 0; i < numbers.value.length; i++) {
        for (let j = i + 1; j < numbers.value.length; j++) {
            //get the numbers at the current positions
            const num1 = numbers.value[i];
            const num2 = numbers.value[j];

            if (num1 + num2 === 21) {
                const combination = [i + 1, j + 1].sort(); // Store the positions of the numbers with index starting at 1
                if (!visited.has(combination)) {
                    combinations.value.push(combination);
                    visited.add(combination);
                }
            }
        }
    }
}

//generate numbers on page load
create()

</script>

<template>
    <div class="title-container">
        <h1 class="title">Matching Numbers</h1>
    </div>
    <div class="container">
        <div class="content-container">
            <p class="numbers-container">{{ numbers.join(', ') }}</p>
            <button class="button-generate" @click="generateNumbers">Generate New Array</button>
            <button class="button" @click="findCombinations">Find Combinations</button>
        </div>
        <div class="combinations-container">
            <p style="font-weight: bold; text-align:center" v-if="numbers.length > 0">
                Combinations:
            </p>
            <ul v-if="combinations.length > 0">
                <li v-for="(combination, index) in combinations" :key="index">
                    {{ combination[0] }} & {{ combination[1] }}
                </li>
            </ul>
            <p v-else-if="numbers.length > 0">No combinations found</p>
            <p v-else>No numbers available</p>
        </div>
    </div>
</template>
  
 
<style>



.title-container {
    text-align: center;
    margin-bottom: 10px;
    padding-bottom: 10px;
    width: 95%;
    border-bottom: 2px solid #E8E8E8;
}

.title {
    font-size: 24px;
    font-weight: bold;
}

.container {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    padding: 20px;
    height: 100%;
    /* Adjusted to take up full height */
}


.combinations-container {
    margin-top: 5px;
    align-items: center;
}
ul {
    list-style-type: none;
    padding: 0;
}
.content-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: white;
    max-width: 400px;
}

.numbers-container {
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5px;
    width: 300px;
    margin: 10px;
    font-size: 18px;
    border-radius: 5px;
    border: 2px solid #BDBDBD;
}

.button-generate {
    font-size: 14px;
    background-color: #5E72E4;
    color: white;
    padding: 5px 5px;
    margin: 5px;
    min-width: 200px;
    /* Set a minimum width for the button */
    border: 2px #5E72E4 solid;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.3s;
}

.button-generate:hover {
    background-color: #3949AB;
    transform: scale(1.05);
}

/* silver #BDBDBD */
.button {
    font-size: 14px;
    color: #5E72E4;
    background-color: white;
    margin: 5px;
    min-width: 200px;
    padding: 5px 5px;
    border: 2px #5E72E4 solid;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.3s;

}

.button:hover {
    background-color: #F5F5F5;
    transform: scale(1.05);
}


/* Responsive styles */
@media (max-width:800px) {

    .button-generate,
    .button {
        width: 40%;
    }
}

@media (max-width: 400px) {

    .button-generate,
    .button {
        width: 60%;
        font-size: 12px;
        padding: 8px 8px;
    }
}
</style>