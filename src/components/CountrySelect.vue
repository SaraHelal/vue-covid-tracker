<template>
            
    <select v-model="selected" @change="onChange()" class="form-select block w-full rounded mt-10 p-3 border"> 
        <option value="0" >Select Country</option>
        <option v-for="country in countries" :value="country.ID" v-bind:key ="country.ID" > {{ country.Country}}</option>
    </select>
  
</template>
<script>
export default {
    name: 'CountrySelect',
    data(){
        return {
        selected: 0

        }
    },
    props: ['countries'],
    methods:{
        onChange(){
            const country = this.countries.find((item)=>item.ID === this.selected);
            console.log(country);
            this.$emit('get-country', country);
        }
    }
    
}
</script>