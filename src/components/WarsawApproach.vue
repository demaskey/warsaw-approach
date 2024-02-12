<script setup lang="ts">
import { reactive, watch } from 'vue'

const warsawApproach = reactive({
    carbRatio: 15,
    insulinSensitivityFactor: 50,
    carbs: 0,
    fat: 0,
    protien: 0,
    fatKCal:0,
    protienKCal:0,
    totalKCal: 0
})

watch(() => warsawApproach.fat, () => {
    warsawApproach.fatKCal = warsawApproach.fat * 9
})
watch(() => warsawApproach.protien, () => {
    warsawApproach.protienKCal = warsawApproach.protien * 4
})
watch(() => warsawApproach.fatKCal, () => {
    warsawApproach.totalKCal = warsawApproach.fatKCal + warsawApproach.protienKCal
})
watch(()=> warsawApproach.protienKCal, () => {
    warsawApproach.totalKCal = warsawApproach.fatKCal + warsawApproach.protienKCal
})
</script>

<template>
    <div>Carb ratio:</div>
    <input v-model.number="warsawApproach.carbRatio"> grams of carbs to 1 unit of insulin
    <div>Insulin Sensitivity Factor:</div>
    <input v-model.number="warsawApproach.insulinSensitivityFactor"> mg/dL
    <div>Carbs (g)</div>
    <input v-model.number="warsawApproach.carbs">
    <div>Fat (g)</div>
    <input v-model.number="warsawApproach.fat">
    <div>Protien (g)</div>
    <input v-model.number="warsawApproach.protien">
    <div>Fat (kcal): {{ warsawApproach.fatKCal }}</div>
    <div>Protien (kcal): {{ warsawApproach.protienKCal }}</div>
    <div>Total (kcal): {{ warsawApproach.totalKCal }}</div>

</template>