<template>

    <div class="grid md:grid-cols-2 gap-4">
        <div class="shadow-md bg-blue-100 p-4 text-center rounded">
            <h2 class="text-3xl font-bold text-blue-900 mb-4">Cases</h2>
            <div class="text-xl mb-4">
                <span class="font-bold">New: </span>
                {{numberWithCommas(stats.NewConfirmed)}}
            </div>
            <div class="text-xl mb-4">
                <span class="font-bold">Total: </span>
                {{numberWithCommas(stats.TotalConfirmed)}}
            </div>
        </div>
        <div class="shadow-md bg-blue-200 p-4 text-center rounded">
            <h2 class="text-3xl font-bold text-blue-900 mb-4">Deaths</h2>
            <div class="text-xl mb-4">
                <span class="font-bold">New: </span>
                {{numberWithCommas(stats.NewDeaths)}}
            </div>
            <div class="text-xl mb-4">
                <span class="font-bold">Total: </span>
                {{numberWithCommas(stats.TotalDeaths)}}
            </div>
        </div>
    </div>
   
</template>
<script>
export default {
    name: 'DataBoxes',
    props:['stats'
    ],
    methods:{
        numberWithCommas(x){
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");

    },
    },
}
</script>