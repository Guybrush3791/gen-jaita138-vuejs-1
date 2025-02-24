<template>
  <div class="container" :class="{ 'dark-mode': isDarkMode }">
    <!-- Greeting Section -->
    <section class="greeting-card">
      <h1 class="main-title">Ciao, Mondo!!</h1>
      <div class="values-display">
        <span class="value-box">X: {{ x }}</span>
        <span class="value-box">Value: {{ value }}</span>
      </div>
      <button class="primary-btn" @click="myFun">Click Me!</button>
    </section>

    <!-- Counter Section -->
    <section class="counter-card">
      <h2 class="section-title">Counter: {{ clickCounter }}</h2>
      <button class="action-btn" @click="clickCounterEvent">Increase Counter</button>
    </section>

    <!-- Toggle Section -->
    <section class="toggle-card">
      <h2 class="section-title" v-if="hideHello">Hello, World!</h2>
      <h2 class="section-title" v-else>Ciao, Mondo!</h2>
      <button class="toggle-btn" @click="hideHelloFun">
        {{ hideHello ? 'Show Italian' : 'Show English' }}
      </button>
    </section>

    <!-- Array Section -->
    <section class="array-card">
      <h2 class="section-title">My First Array</h2>
      <div class="array-list">
        <p v-for="value in myArr" :key="value" class="array-item">Value: {{ value }}</p>
      </div>
      <button class="add-btn" @click="addElem(myArr.length * 2)">Add Element</button>
    </section>

    <!-- Form Section -->
    <section class="form-card">
      <h2 class="section-title">User Input: {{ userText || 'No text yet' }}</h2>
      <form @submit.prevent="onSubmit" class="input-form">
        <input
          type="text"
          placeholder="Enter your text here"
          v-model="userText"
          class="text-input"
        />
        <button type="submit" @click="sendToBackEnd" class="submit-btn">Submit</button>
      </form>
    </section>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.greeting-card,
.counter-card,
.toggle-card,
.array-card,
.form-card {
  background: #ffffff;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.main-title {
  color: #2c3e50;
  font-size: 2rem;
  margin-bottom: 15px;
}

.section-title {
  color: #34495e;
  font-size: 1.5rem;
  margin-bottom: 15px;
}

.values-display {
  display: flex;
  gap: 15px;
  margin-bottom: 15px;
}

.value-box {
  background: #ecf0f1;
  padding: 8px 12px;
  border-radius: 4px;
}

.array-list {
  margin: 15px 0;
}

.array-item {
  background: #f8f9fa;
  padding: 8px;
  margin: 5px 0;
  border-radius: 4px;
}

.input-form {
  display: flex;
  gap: 10px;
}

.text-input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

.primary-btn,
.action-btn,
.toggle-btn,
.add-btn,
.submit-btn {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: transform 0.2s;
}

.primary-btn {
  background: #3498db;
  color: white;
}

.action-btn {
  background: #2ecc71;
  color: white;
}

.toggle-btn {
  background: #9b59b6;
  color: white;
}

.add-btn {
  background: #e67e22;
  color: white;
}

.submit-btn {
  background: #e74c3c;
  color: white;
}

button:hover {
  transform: translateY(-2px);
}

button:active {
  transform: translateY(0);
}

.dark-mode {
  background-color: #333;
  color: #fff;
}

.dark-mode .greeting-card,
.dark-mode .counter-card,
.dark-mode .toggle-card,
.dark-mode .array-card,
.dark-mode .form-card {
  background: #444;
  box-shadow: 0 2px 4px rgba(255, 255, 255, 0.1);
}

.dark-mode .main-title,
.dark-mode .section-title {
  color: #eee;
}

.dark-mode .value-box {
  background: #555;
  color: #eee;
}

.dark-mode .array-item {
  background: #666;
  color: #eee;
}

.dark-mode .text-input {
  background: #555;
  color: #eee;
  border: 1px solid #777;
}
</style>

<script setup>
import { ref } from 'vue'

console.log('Hello, World!')

// let/const per creare variabili
let x = 10
console.log('x', x)
x = 20
console.log('x', x)

const value = 150
console.log('value', value)
// value = 100 // error: value e' una costante
// console.log('value', value)

function myFun() {
  console.log("Hello, I'm 'myFun' function!")
}
const myFun2 = () => {
  console.log("Hello, I'm 'myFun2' function!")
}

myFun()
myFun2()

const clickCounter = ref(0)
const clickCounterEvent = () => {
  clickCounter.value++
}

const hideHello = ref(true)
const hideHelloFun = () => {
  hideHello.value = !hideHello.value
}

const myArr = ref([10, 20])
console.log('myArr', myArr.value)
for (let x = 0; x < myArr.value.length; x++) {
  const value = myArr.value[x]
  console.log('value', value)
}
const addElem = (value) => {
  myArr.value.push((value + 1) * 10)
}

const userText = ref('')
const sendToBackEnd = () => {
  console.log('userText', userText.value)
  userText.value = ''
}

const isDarkMode = ref(true)
</script>
