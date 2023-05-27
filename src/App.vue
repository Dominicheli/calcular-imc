<script lang="ts" setup>
import { reactive, ref } from 'vue';
import IcGithub from './icons/IcGithub.vue'
import IcLinkedin from './icons/IcLinkedin.vue'

interface ICalculate {
  height: number,
  weight: number,
  total: number,
  imc: string
}

const calculate = reactive<ICalculate>({
  height: 0,
  weight: 0,
  total: 0,
  imc: ''
})
const hasError = ref(false)

function calculateIMC() {
  if(calculate.height === 0 || calculate.weight === 0) {
    hasError.value = true
    return
  }

  hasError.value = false
  calculate.total = calculate.weight / (calculate.height * calculate.height)
  switch (true) {
    case calculate.total < 18.5:
      calculate.imc = "Abaixo do peso";
      break;
    case calculate.total < 25:
      calculate.imc = "Peso normal";
      break;
    case calculate.total < 30:
      calculate.imc = "Sobrepeso";
      break;
    case calculate.total < 40:
      calculate.imc = "Obesidade";
      break;
    default:
      calculate.imc = "Obesidade grave";
  }
}
</script>

<template>
  <div class="w-screen h-screen bg-slate-200 flex flex-col justify-center items-center">
    <div class="flex flex-col items-center gap-6 border-4 border-teal-700 rounded-2xl p-14 bg-slate-100">

      <h1 class="block text-teal-700 text-3xl font-bold mb-2 text-center">Calcular IMC</h1>
      <div class="flex flex-col">

        <label for="height" class="block text-teal-700 text-sm font-bold mb-2">Altura:
          <div class="flex items-center border-b border-teal-500 py-2">
            <input
v-model="calculate.height" type="number" name="height"
              class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
              placeholder="Exemplo: 1,70">
            <div
class="flex-shrink-0 bg-teal-500 border-teal-500 text-sm border-4 text-white py-1 px-2 rounded"
              type="button">
              m
            </div>
          </div>
          <p class="text-gray-400">Exemplo: 1,70m</p>
        </label>


        <label for="weight" class="block text-teal-700 text-sm font-bold mb-2">Peso:
          <div class="flex items-center border-b border-teal-500 py-2">
            <input
v-model="calculate.weight" type="number" name="weight"
              class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
              placeholder="Exemplo: 60">
            <div class="flex-shrink-0 bg-teal-500 border-teal-500 text-sm border-4 text-white py-1 px-2 rounded">
              kg
            </div>
          </div>
          <p class="text-gray-400">Exemplo: 60 kg</p>
        </label>


      </div>
      <div class="flex flex-col items-center">
        <p v-if="hasError" class="text-red-500">Digite sua altura e peso para calcular</p>


        <p v-if="calculate.total !== 0 && !hasError">
          Seu IMC é: {{ calculate.total.toFixed(2) }}
          <strong>{{ calculate.imc }}</strong>
        </p>

      </div>
      <button
class="bg-teal-500  transition duration-150 text-white rounded p-2 w-full shadow-lg"
        @click="calculateIMC">Calcular</button>
    </div>

    <div class="flex flex-col items-center mt-2 text-teal-900">
      <span><strong>Feito por:</strong>  Felipe O. Dominicheli</span>
      <div class="flex gap-2 mt-2">
        <a href="https://github.com/Dominicheli" target="_blank" class="w-10 h-10 bg-white rounded-full flex justify-center items-center">
          <IcGithub />
        </a>
        <a href="https://www.linkedin.com/in/felipe-dominicheli-264499130/" target="_blank" class="w-10 h-10 bg-white rounded-full flex justify-center items-center">
          <IcLinkedin />
        </a>
      </div>
    </div>
  </div>
</template>


