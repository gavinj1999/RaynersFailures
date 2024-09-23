<script setup>
import {
  format,
  compareAsc,
  formatDistanceToNow,
  differenceInDays,
} from "date-fns";


const basePromise = 1500000;
const builds = [
  {
    date: "23/07/2024",
    total: 0,
  },
];

function numberWithCommas(x) {
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}

const housing = [
  {
    targetHouses: numberWithCommas(basePromise),
    buildTotal: builds.reduce((n, { total }) => n + total, 0),
    monthlyTarget: basePromise / 60,
    daysUntil: 365 * 5,
    dailyTarget: (
      (basePromise - builds.reduce((n, { total }) => n + total, 0)) /
      (365 * 5)
    ).toFixed(2),
    weeks: (365 * 5) / 7,
    housesBuilt: 0 + builds.reduce((n, { total }) => n + total, 0),
    unbuilt:
      ((basePromise - builds.reduce((n, { total }) => n + total, 0)) /
        (365 * 5)) *
      differenceInDays(new Date(), new Date("2024/07/05")).toFixed(2),
    diff: differenceInDays(new Date(), new Date("2024/07/05")),
    housesOutOfSchedule: numberWithCommas(
      basePromise - builds.reduce((n, { total }) => n + total, 0)
    ),
    newSchedule: (
      (basePromise - builds.reduce((n, { total }) => n + total, 0)) /
      (365 * 5 - differenceInDays(new Date(), new Date("2024/07/05")))
    ).toFixed(2),
  },
];

</script>
<template>
    <div class="h-screen bg-center bg-no-repeat bg-cover"
      style=" background-image: url('./src/assets/img/smoke.jpeg');">
    <div class="flex flex-col items-center justify-center h-screen">
      <div class="px-8 py-4 text-xl font-bold text-white bg-red-500 rounded-md opacity-60">
Angelas Promise
      </div>
      <div class="px-8 py-8 my-8 text-xl font-medium text-white bg-red-500 rounded-md opacity-60">
        <div class="opacity-100 div">
           <div class="flex items-stretch py-1">
            <div class="px-2">Target Houses: </div>
            <div class="px-2">{{ housing[0].targetHouses }}</div>
           </div>           
           <div class="flex items-center py-1">
            <div class="px-2">Days in Office: </div>
            <div class="px-2">{{ housing[0].diff.toFixed(0) }}</div>
           </div>
           <div class="flex items-center py-1">
            <div class="px-2">Builds Per Day: </div>
            <div class="px-2">{{ housing[0].dailyTarget }}</div>
           </div>
           <div class="flex items-center py-1">
            <div class="px-2">Builds behind target: </div>
            <div class="px-2">{{ housing[0].unbuilt.toFixed(0) }}</div>
           </div>
           <div class="flex items-center py-1">
            <div class="px-2">New Builds Per Day: </div>
            <div class="px-2">{{ housing[0].newSchedule }}</div>
           </div>
        </div>
            
      </div>
      <div class="px-8 py-2 text-xl font-medium text-red-500 transition-colors bg-white rounded-md hover:bg-red-500 hover:text-white">
        <a :href="'http://twitter.com/share?text=Labours Housebuilding promise, ' + housing[0].unbuilt.toFixed(0) +' behind schedule after '+ housing[0].diff +' days in Government&%20https://pbs.twimg.com/media/GTobX5sXMAAxXbU.png&url=https://thefailurelist.co.uk/&hashtags=LabourFail,LabourSumsNeverAddUp,CarnivalOfFools'">Tweet</a>
      </div>
 
    </div>
    
    </div>
</template>