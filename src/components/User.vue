<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: {{ name }}</p>
    <p>{{ getDateAndTime(createdAt) }}</p>
    <p>{{ helloToMixin }}</p>
    <v-btn @click="changeName()">이름 변경</v-btn>
    <hr>
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <UserDetail 
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
        ></UserDetail>
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
          @child="parents"
        >
        </UserEdit>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import UserDetail from "./UserDetail.vue"
import UserEdit from "./UserEdit.vue"
import { dateFormat } from "../mixins/dateFormat"

export default {
  components: {
    UserDetail,
    UserEdit
  },
  data () {
    return {
      name: "Hoza",
      address: "Seoul",
      phone: "1234-5678",
      hasDog: true,
      createdAt: null,
    }
  },
  computed: {
    helloToMixin() {
      return this.mixinData + " 안녕하세요."
    }
  },
  created () {
    this.createdAt = new Date()
  },
  methods: {
    parents (user) {
      this.name = user.name
      this.address = user.address
      this.phone = user.phone
      this.hasDog = user.hasDog
      console.log("OK")
    },
    // getDateAndTime(date) {
    //   if (date !== null) {
    //     let hour = date.getHours()
    //     let minutes = date.getMinutes()
    //     let fullDate =  `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`
    //     return `${fullDate} ${hour}:${minutes}`
    //   } else {
    //     return null
    //   }
    // }
  },
  mixins: [dateFormat]
}
</script>