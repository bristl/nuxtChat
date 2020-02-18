<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
    >
      <v-card min-width="400">
        <v-card-title><h1>Nuxt чат</h1></v-card-title>
        <v-card-text>
          <v-form
            ref="form"
            v-model="valid"
            lazy-validation
          >
            <v-text-field
              v-model="name"
              :counter="16"
              :rules="nameRules"
              label="Name"
              required
            ></v-text-field>

            <v-text-field
              v-model="room"
              :rules="roomRules"
              label="Room number"
              required
            ></v-text-field>

            

            <v-btn
              :disabled="!valid"
              color="success"
              class="mr-4"
              @click="submit"
            >
              Enter
            </v-btn>
          </v-form>
        </v-card-text>
    </v-card>
      
    </v-flex>
  </v-layout>
</template>


<script>
  import {mapMutations} from 'vuex'
  export default {
    layout: 'empty',
    head: {
      title: 'Welcome to nuxt chat'
    },
    sockets: {
    connect() {
      console.log('CLIENT socket connected')
    }
  },
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Enter your name',
        v => (v && v.length <= 16) || 'Name must be less than 16 characters',
      ],
      room: '',
      roomRules: [
        v => !!v || 'Enter a room',
      ],
    }),

    methods: {
      ...mapMutations(['setUser']),
      submit () {
        if (this.$refs.form.validate()) {
          const user = {
            name: this.name,
            room: this.room
          };

          this.$socket.emit('userJoined', user, data => {
            if (typeof data === 'string') {
              console.error(data)
            } else {
              user.id = data.userId
              this.setUser(user)
              this.$router.push('/chat')
            }
          })
        }


        
      },
    },
  }
</script>
