<template>
  <div class="add">
    <h2 class="display-1 font-weight-bold mb-3" style="text-align: center;">Редактировать рейс</h2>
    <br>
    <v-form
      @submit.prevent="update"
      ref="addForm"
      class="my-2"
    >
      <v-row>
        <v-col cols="3" class="mx-auto">
          <v-select
            label="Самолет"
            v-model="addForm.plane"
            :items="planes"
            item-text="model"
            item-value="id"
            return-object
            single-line
            >
          </v-select>
          <v-text-field
            v-model="addForm.number"
            item-text='this.flight_cur.number'
            label="Номер"
          ></v-text-field>
          <v-text-field
            v-model="addForm.gate"
            item-text='this.flight_cur.gate'
            label="Гейт"
          ></v-text-field>
          <v-text-field
            v-model="addForm.wherefrom"
            item-text='this.flight_cur.wherefrom'
            label="Откуда"
          ></v-text-field>
          <v-text-field
            v-model="addForm.whereto"
            item-text='this.flight_cur.whereto'
            label="Куда"
          ></v-text-field>
          <v-text-field
            v-model="addForm.arrival"
            item-text='this.flight_cur.arrival'
            label="Отлет"
          ></v-text-field>
          <v-text-field
            v-model="addForm.departure"
            item-text='this.flight_cur.departure'
            label="Прилет"
          ></v-text-field>
          <v-btn color="primary" type="submit">ОК</v-btn>
        </v-col>
      </v-row>
    </v-form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'FlightUpd',
  data: () => ({
    flight_id: 0,
    flight_cur: {
      number: '',
      departure: '',
      arrival: '',
      whereto:'',
      wherefrom:'',
      gate:'',
      plane: "",
    },
    addForm: {
      number: '',
      departure: '',
      arrival: '',
      whereto:'',
      wherefrom:'',
      gate:'',
      plane: "",
    }
  }),
  created () {
    this.PlanesList()
    this.flight_id = this.$route.params.flight_id
    this.axios
      .get(`http://127.0.0.1:8000/flights/${this.flight_id}/`)
      .then((res) => {
        console.log(res)
        this.flight_cur = res.data
        this.addForm.number = this.flight_cur.number
        this.addForm.departure = this.flight_cur.departure
        this.addForm.arrival = this.flight_cur.arrival
        this.addForm.whereto = this.flight_cur.whereto
        this.addForm.wherefrom = this.flight_cur.wherefrom
        this.addForm.gate = this.flight_cur.gate
        this.addForm.plane = this.flight_cur.plane
        console.log(this.flight_cur)
      })
  },
  methods: {
    async PlanesList () {
      try {
        const response = await axios
            .get('http://127.0.0.1:8000/planes/all')
        if (response.status !== 200) {
          throw new Error(response.status)
        }
        this.planes = response.data
        // for (let i = 0; i < res.data.length; i++) {
         // let label = data[i].id
       //   let id = data[i].id
          //this.planes.push({ label: label, code: id })
     //   }
        return response.data
      } catch (e) {
        console.error('AN API ERROR', e)
      }
    },
    async update () {
      await this.axios
        .put(`http://127.0.0.1:8000/flights/${this.flight_id}/`, this.addForm)
        .then((res) => {
          console.log(res)
          this.$refs.addForm.reset()
          this.$router.push('/flight/')
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>