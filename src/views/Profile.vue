<template>
    <div>
        <nav class="navbar orange lighten-1">
      <div class="nav-wrapper">
        <ul class="right hide-on-small-and-down">
          <li>
            <a
                class="dropdown-trigger black-text"
                href="#"
                data-target="dropdown"
                ref="dropdown"
            >
              {{name}}
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
        <main class="app-content">
            <div class="app-page">

                <div>
                <div class="page-title">
                    <h3>Профиль</h3>
                </div>

                <form class="form">
                    <div class="input-field">
                    <input
                        id="description"
                        type="text"
                    >
                    <label for="description">Имя</label>
                    <span
                            class="helper-text invalid">name</span>
                    </div>

                    <button class="btn waves-effect waves-light" type="submit">
                    Обновить
                    <i class="material-icons right">send</i>
                    </button>
                </form>
                </div>

            </div>
        </main>
    </div>
</template>

<script>
export default {
  name: 'profile'
}
</script>