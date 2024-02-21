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
    totalKCal: 0,
    fatProtienUnits: 0,
    fpuRounded: 0,
    extendedBolusDuration: "-",
    carbsPerFPU: 10,
    extendedBolusInsulin: 0
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
watch(()=> warsawApproach.totalKCal, () => {
    warsawApproach.fatProtienUnits = warsawApproach.totalKCal / 100
})
watch(() => warsawApproach.fatProtienUnits, () => {
    warsawApproach.fpuRounded = Math.round(warsawApproach.fatProtienUnits)
})
watch(()=> warsawApproach.fpuRounded, () => {
    if(warsawApproach.fpuRounded == 1) warsawApproach.extendedBolusDuration = "3 hours"
    else if(warsawApproach.fpuRounded == 2) warsawApproach.extendedBolusDuration = "4 hours"
    else if(warsawApproach.fpuRounded == 3) warsawApproach.extendedBolusDuration = "5 hours"
    else if(warsawApproach.fpuRounded == 4) warsawApproach.extendedBolusDuration = "8 hours"
})
watch(() => warsawApproach.fatProtienUnits, () => {
    warsawApproach.extendedBolusInsulin = warsawApproach.fatProtienUnits * warsawApproach.carbsPerFPU / warsawApproach.carbRatio
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
    <div>Fat-Protien Units (FPU): {{ warsawApproach.fatProtienUnits }}</div>
    <div>FPU Rounded: {{ warsawApproach.fpuRounded }}</div>
    <div>Duration of Extended Bolus: {{ warsawApproach.extendedBolusDuration }}</div>
    <div>Carbs per FPU (g)</div>
    <input v-model.number="warsawApproach.carbsPerFPU">
    <div>Extended Bolus (u): {{ warsawApproach.extendedBolusInsulin }}</div>

</template>