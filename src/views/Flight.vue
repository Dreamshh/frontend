<template>
 <section>
   <place-form :from="savedPlace" />
   <v-row>
     <v-form
     @submit.prevent="submitPlace"
     ref="form"
     class="my-2"
   >
     <v-row>
       <v-col cols="3" class="mx-auto">
         <v-text-field
           label="Введите пункт вылета"
           v-model="from"
           name="from"
           placeholder="Spb"
         />
       </v-col>
     </v-row>
 
   </v-form>
     <v-col cols="6" class="mx-auto">
       <flight-item-card
         v-for="flightItem in flightItems"
         :key="flightItem.identifier"
         :flight-item="flightItem"
         class="my-2"
       />
       <v-btn color="primary" class="mb-3 mr-3" @click='$router.push("/flight/create/")'>Добавить рейс</v-btn>
       <br>
       <v-btn
            color="accent"
            class="mb-3 mr-3"
            @click="$router.push(`/`)"
            >На главную</v-btn
          >
     </v-col>
   </v-row>
 </section>
</template>
 
<script>
import FlightItemCard from '@/components/FlightItemCard.vue'
import PlaceForm from '@/components/PlaceForm'
 
export default {
 components: { FlightItemCard, PlaceForm },
 name: 'Flight',
 
 data: () => ({
   flightItems: [],
   from: '',
 }),
 
 methods: {
   submitPlace () {
     // сохраним username в localStorage
      localStorage.setItem('from', this.from)
      this.savedPlace = this.from
     // сохраним его в отдельную переменную,
     // для дальнейшей передачи в компоненту
     // GreetingCard
 
     // очистим форму
     this.$refs.form.reset()
     this.getFlightItems()
   },
   async getFlightItems () {
     try {
       // выполним запрос на получение списка всех
       // фотографий земли
       const response = await this.axios
         .get(`http://127.0.0.1:8000/flights/all?from=${this.savedPlace}`)
 
       // если статус ответа не 200, то выкинем
       // ошибку
       if (response.status !== 200) {
         throw new Error(response.error)
       }
 
       // пройдёмся по полученному массиву данных и
       // приведём его к тому виду, с которым будет
       // удобно работать
       const flightItems = response.data.map((flightItem) => {
         let date = new Date(flightItem.departure)
 
         // собираем дату в нужном виде
         let year = date.getFullYear()
 
         let month = String(date.getMonth() + 1).length > 1
           ? date.getMonth() + 1
           : `0${date.getMonth() + 1}`
 
         let day = String(date.getDate()).length > 1
           ? date.getDate()
           : `0${date.getDate()}`
         let hour = String(date.getHours()).length > 1
           ? date.getHours()
           : `0${date.getHours()}`
         let min = String(date.getMinutes()).length > 1
           ? date.getMinutes()
           : `0${date.getMinutes()}`

          flightItem.departure = `${year}/${month}/${day} ${hour}:${min}`

         date = new Date(flightItem.arrival)
 
         year = date.getFullYear()
 
         month = String(date.getMonth() + 1).length > 1
           ? date.getMonth() + 1
           : `0${date.getMonth() + 1}`
 
         day = String(date.getDate()).length > 1
           ? date.getDate()
           : `0${date.getDate()}`
         hour = String(date.getHours()).length > 1
           ? date.getHours()
           : `0${date.getHours()}`
         min = String(date.getMinutes()).length > 1
           ? date.getMinutes()
           : `0${date.getMinutes()}`
 
         flightItem.arrival = `${year}/${month}/${day} ${hour}:${min}`
 
         return flightItem
       })
 
       this.flightItems = flightItems
     } catch (e) {
       console.error('AN API ERROR', e)
     }
   }
 },
 
 created () {
   if (localStorage.getItem('from')) 
     this.from = localStorage.getItem('from')
     this.savedPlace = this.from
   this.getFlightItems()  
 }
}
</script>
 
<style>
</style>
