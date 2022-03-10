<template>
 <ul class="planes-list">
   <li
     v-for="plane in planes"
     :key="plane.id"
   >
     {{ plane.model }}
     <br>
     {{ plane.company }}
     <br>
     {{ plane.prod_date }}
   </li>
 </ul>
</template>
 
<script>
export default {
 name: 'PlanesList',
 
 props: {
   planes: Array
 }
}
</script>
 
<style>
.planes-list li {
 text-align: left;
}
</style>