<template>
    <div class=" row">

        <nav class="navbar navbar-expand-lg navbar-dark fixed-top menu-header">
            <div class="container-fluid">
                <a class="navbar-brand" href="/">
                    <img src="../../public/TvLike-transparent.png" width="100" height="80" class="d-inline-block align-text-top"/>
                </a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarCollapse" aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse items-nav" id="navbarCollapse">
                    <ul class="navbar-nav align-items-center mr-auto">
                        <li class="nav-item">
                            <a class="nav-link link-menu" aria-current="page" href="/">
                              <i class="bi bi-house-door-fill"> Home</i>
                            </a>
                        </li>
                        <li class="nav-item dropdown dropend">
                            <a class="nav-link dropdown-toggle link-menu" href="#" id="navbarDropdownMenuLink" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                              <i class="bi bi-star-fill"> Generos Destacados</i>
                            </a>
                            <!-- Lista de opciones para el enlace de peliculas---->
                            <ul class="dropdown-menu menu-list" aria-labelledby="navbarDropdownMenuLink">
                                <li>
                                  <div class="dropdown-item link-destino">
                                    <a :href="destino('Action')">Accion</a>
                                  </div>
                                </li>
                                <li>
                                  <div class="dropdown-item link-destino">
                                    <a :href="destino('Animation')">Animacion</a>
                                  </div>
                                </li>
                                <li>
                                  <div class="dropdown-item link-destino">
                                    <a :href="destino('Comedy')">Comedia</a>
                                  </div>
                                </li>
                                <li>
                                  <div class="dropdown-item link-destino">
                                    <a :href="destino('Horror')">Terror</a>
                                  </div>
                                </li>
                                <li>
                                  <div class="dropdown-item link-destino">
                                    <a :href="destino('Romance')">Romance</a>
                                  </div>
                                </li>
                            </ul>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link link-menu" href="/proximos-estrenos">
                              <i class="bi bi-calendar-event-fill"> Proximos Estrenos</i>
                            </a>
                        </li>
                    </ul>
                    <!-- <div class="me-2 text-end">
                        <ul class="navbar-nav align-items-center mr-auto">
                            <div v-if="!user" class="d-flex session">
                                <li class="nav-item dropdown">
                                    <router-link to="/login" class="nav-link">Iniciar Sesion</router-link>
                                    <router-view/>
                                </li>
                                <li class="nav-item dropdown">
                                    <router-link to="/sign" class="nav-link">Registrarse</router-link>
                                    <router-view/>
                                </li>
                            </div>
                            <div v-else class="d-flex">
                                <li class="nav-item dropdown">
                                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                                        <i class="bi bi-person-circle"></i>
                                    </a>
                                    <ul class="dropdown-menu menu-list">
                                        <li><div @click="perfilUser(user.id)" class="dropdown-item link-destino" style="color: white; cursor:pointer;">{{ user.name}} (ver perfil)</div></li>
                                        <li><div @click="editPerfil(user.id)" class="dropdown-item link-destino" style="color: white; cursor:pointer;">Editar Perfil</div></li>
                                        <li><div @click="logout" class="dropdown-item link-destino" style="color: white; cursor:pointer;">Cerrar Sesion</div></li>
                                    </ul>
                                </li>
                            </div>
                        </ul>
                    </div> -->
                </div>
            </div>
        </nav>
    </div>
</template>

<script>
export default {
  data () {
    return {
      user: this.$store.state.user
    }
  },

  created () {
    if (localStorage.getItem('user-data') !== null) {
      this.user = JSON.parse(localStorage.getItem('user-data'))
    } else {
      this.cargarDataUser()
    }
  },

  methods: {
    cargarDataUser () {
      if (this.$store.state.user !== null) {
        this.user = this.$store.state.user
        this.cargarLocalStorage()
      }
    },

    cargarLocalStorage () {
      localStorage.setItem('user-data', JSON.stringify(this.user))
    },

    destino (genre) {
      return `/peliculas/${genre}/${1}`
    },

    perfilUser (id) {
      this.$router.push(`/user/${id}`)
    },

    editPerfil (id) {
      this.$router.push(`/edit-user/${id}`)
    },

    logout () {
      const token = this.$store.state.token
      this.$store.dispatch('logout_session', token)
      setTimeout(() => {
        localStorage.clear()
        location.replace('/')
      }, 1000)
    }
  }
}

</script>

<style scoped>
    .menu-header {
        background: #1b2557d9;
    }
    .items-nav {
      justify-content: space-around;
    }
    .link-menu {
        font-weight: bold;
        color: #fffffe !important;
    }
    .link-menu:hover {
      color: #344181d9 !important;
    }
    .menu-list {
        background: #464555e8;
    }
    .link-destino {
        cursor:pointer;
        font-weight: bold;
    }
    .link-destino a {
      text-decoration: none;
      color: white;
    }
    .link-destino:hover{
        background: #ABA9BC;
    }
    .link-destino a:hover {
      color: #344181d9;
    }
    li {
        list-style: none;
    }
    @media(min-width: 250px) and (max-width: 991px) {
        .session {
            flex-direction: column;
            align-items: center;
        }
    }
</style>
