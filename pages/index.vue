<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8>
      <v-card min-width="400">
        <v-card-title>
          <h1>Nuxt Chat</h1>
        </v-card-title>
        <v-card-text>
          <v-form
            ref="form"
            v-model="valid"
            lazy-validation
          >
            <v-text-field
              v-model="name"
              :counter="10"
              :rules="nameRules"
              label="Name"
              required
            ></v-text-field>

            <v-text-field
              v-model="room"
              :rules="roomRules"
              label="Введите комнату"
              required
            ></v-text-field>

            <v-btn
              :disabled="!valid"
              color="primary"
              class="mr-4"
              @click="submit"
            >
              Войти
            </v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
  import { mapMutations } from 'vuex';
  export default {
    layout: 'empty',
    head: {
      title: 'Добро пожаловать!'
    },
    sockets: {
      connect: function () {
        console.log('socket connected')
      },
      customEmit: function (data) {
        console.log('this method was fired by the socket server. eg: io.emit("customEmit", data)')
      }
    },
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Введите имя',
        v => (v && v.length <= 10) || 'Имя не должно превышать 10 символов',
      ],
      room: '',
      roomRules: [
        v => !!v || 'Введите комнату',
      ]
    }),

    methods: {
      ...mapMutations(['setUser']),
      submit () {
        this.$refs.form.validate()
        const user = {
          name: this.name,
          room: this.room
        };
        this.setUser(user);
        this.$router.push('/chat');
      }
    },
  }
</script>
