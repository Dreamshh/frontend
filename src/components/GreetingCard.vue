
<template>
    <h1>Добро пожаловать на сайт <span v-if="username"> {{ username }}</span>!</h1>
</template>
<script>
export default {
 name: 'GreetingCard',
 
 props: {
   username: String
 }
 
}
</script>
 
<style>
</style>
