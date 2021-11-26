<template>
  <div class="col-xl-6 offset-xl-3">
      <div v-if="ready">
          <p v-for="user,i in info"
              :key="i">
              {{user.username}} {{user.type}}
          </p>
      </div>
      <div v-if="!ready">
          <h4><div class="letter">Введите ваше имя</div></h4>
          <form @submit.prevent="addUser">
              <div class="form-group row">
                  <input type="text" class="form-control col-9" v-model="username"
                      placeholder="Пиши здесь">
                  <input @click="logIn" type="submit" value="Войти" class="btn btn-sm btn-info ml-1">
              </div>
          </form>
      </div>
      <h2 v-else>
          <button class="letter btn-15 custom-btn">{{username}}</button>
      </h2>
      <div class="card bg-info" v-if="ready">
          <div class="card-header text-white">
              <h4> 1000 - 7 <span class="float-right">{{connections}} подключено</span></h4>
          </div>
          <ul class="list-group list-group-flush text-right">
              <small v-if="typing" class="text-white">{{typing}} is typing</small>
              <li class="list-group-item" v-for="message,i in messages"
                  :key="i">
                  <span :class="{'float-left':message.type === 1}">
                      {{message.message}}
                      <small>:{{message.user}}</small>
                  </span>
              </li>
          </ul>
          <div class="card-body">
              <form @submit.prevent="send">
                  <div class="form-group">
                      <input type="text" class="form-control" v-model="newMessage"
                          placeholder="Писать сюда">
                  </div>
              </form>
          </div>
      </div>
      <div>
      {{username}}
      </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      username: '',
    }
  },
  methods: {
    logIn() {
      this.$router.push('/about')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
