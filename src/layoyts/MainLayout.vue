<template>
    <div class="empty-layout">
      <nav class="navbar blue lighten-1">
      <div class="nav-wrapper">
        <ul class="right">
          <li>
            <a
              class="dropdown-trigger black-text"
              href="#"
              data-target="dropdown"
              ref="dropdown"
            >
            <span class="login-name">Пользователь</span> {{name}}
              <i class="material-icons right">arrow_drop_down</i>
            </a>

            <ul id='dropdown' class='dropdown-content'>
              <li class="divider" tabindex="-1"></li>
              <li>
                <router-link to="/login" class="black-text">
                  <i class="material-icons">assignment_return</i>Выйти
                </router-link>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </nav>
    <div class="page-title">
      <h3>Профиль</h3>
    </div>

    <form class="form" @submit.prevent="submitForm">
      <div class="input-field">
        <input
            id="description"
            type="text"
            v-model="name"
            :class="{invalid: ($v.name.$dirty && !$v.name.required)}"
        >
        <label for="description">Имя</label>
        <small class="helper-text invalid"
        v-if="$v.name.$dirty && !$v.name.required"
        >Введите имя</small>
      </div>

      <button class="btn waves-effect waves-light" type="submit">
      Обновить
      <i class="material-icons right">send</i>
      </button>
    </form>
  </div>
</template>

<script>
import {mapGetters, mapActions} from 'vuex'
import {required} from 'vuelidate/lib/validators'

export default {
    name: 'loginRegistr',
    data: () => ({
      name: ''
    }),
    validations: {
        name: {required},
    },
    async mounted() {
      M.Dropdown.init(this.$refs.dropdown)

      if(this.$store.getters.info) {
        await this.$store.dispatch('fetchInfo')
      }  
      
      this.name = this.info.name
     
      setTimeout(() =>  M.updateTextFields())
    },
    computed: {
    name() {
      return this.$store.getters.info.name
    },
    ...mapGetters(['info'])
  },
  methods: {
    ...mapActions(['updateInfo']),
      async submitForm() {
            if(this.$v.$invalid) {
                this.$v.$touch()
                return
            }

            try {
              await this.updateInfo({
                name: this.name
              })
            } catch(e) {
                console.log(e)
            }

        }
    }
}
</script>

<style lang="scss">
  .page-title {
    text-align: center;
  }

  .form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  } 

  .login-name {
    color: #fff;
    font-size: 20px;
    margin: 0 29px 0 0px;
  }

  .dropdown-trigger.black-text {
    font-size: 20px;
    font-weight: 500;
}
</style>