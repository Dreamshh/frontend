
<template>
    <h1>Билеты из: <span v-if="from"> {{ from }}</span></h1>
</template>
<script>
export default {
 name: 'PlaceForm',
 
 props: {
   from: String
 }
 
}
</script>
 
<style>
</style>
