<template>
  <div class="wrapper" :class="{ 'nav-open': $sidebar.showSidebar }">
    <side-bar
      :background-color="sidebarBackground"
      short-title="Plataforma"
      title="Plataforma"
    >
      <template v-slot:links>
        <!--                                        Menu Usuarios                        -->
        <div v-if="rol == 'usuario'">
          <sidebar-item
            :link="{
              name: 'Agregar informacion',
              icon: 'ni ni-tv-2 text-primary',
              path: '/Agregar',
            }"
          />

          <sidebar-item
            :link="{
              name: 'Datos Agregados',
              icon: 'ni ni-planet text-blue',
              path: '/DatosAgregados',
            }"
          />
          <!-- <sidebar-item
            :link="{
              name: 'Maps',
              icon: 'ni ni-pin-3 text-orange',
              path: '/maps',
            }"
          />
          <sidebar-item
            :link="{
              name: 'User Profile',
              icon: 'ni ni-single-02 text-yellow',
              path: '/profile',
            }"
          />
          <sidebar-item
            :link="{
              name: 'Tables',
              icon: 'ni ni-bullet-list-67 text-red',
              path: '/tables',
            }"
          />
          <sidebar-item
            :link="{
              name: 'Login',
              icon: 'ni ni-key-25 text-info',
              path: '/login',
            }"
          />
          <sidebar-item
            :link="{
              name: 'Register',
              icon: 'ni ni-circle-08 text-pink',
              path: '/register',
            }"
          /> -->
        </div>
        <!--                                        Menu Admin                        -->

        <div v-if="rol == 'admin'">
          <sidebar-item
            :link="{
              name: 'Usuarios',
              icon: 'ni ni-tv-2 text-primary',
              path: '/usuarios',
            }"
          />

          <sidebar-item
            :link="{
              name: 'Marca',
              icon: 'ni ni-planet text-blue',
              path: '/marca',
            }"
          />

          <sidebar-item
            :link="{
              name: 'Modelo',
              icon: 'ni ni-mobile-button text-blue',
              path: '/modelo',
            }"
          />        
          <!-- <sidebar-item
            :link="{
              name: 'Tables',
              icon: 'ni ni-bullet-list-67 text-red',
              path: '/tables',
            }"
          />
          <sidebar-item
            :link="{
              name: 'Login',
              icon: 'ni ni-key-25 text-info',
              path: '/login',
            }"
          />
          <sidebar-item
            :link="{
              name: 'Register',
              icon: 'ni ni-circle-08 text-pink',
              path: '/register',
            }"
          /> -->
        </div>

      </template>
    </side-bar>
    <div class="main-content" :data="sidebarBackground">
      <dashboard-navbar :user="user"></dashboard-navbar>

      <div @click="toggleSidebar">
        <!-- your content here -->
        <router-view></router-view>
        <content-footer v-if="!$route.meta.hideFooter"></content-footer>
      </div>
    </div>
  </div>
</template>
<script>
import DashboardNavbar from "./DashboardNavbar.vue";
import ContentFooter from "./ContentFooter.vue";
import { mapActions } from "vuex";
export default {
  components: {
    DashboardNavbar,
    ContentFooter,
  },
  data() {
    return {
      sidebarBackground: "vue", //vue|blue|orange|green|red|primary,
      user: {},
      rol: "",
    };
  },
  methods: {
    ...mapActions(["obtenerToken", "datosUser"]),
    toggleSidebar() {
      if (this.$sidebar.showSidebar) {
        this.$sidebar.displaySidebar(false);
      }
    },
  },
  created() {
    this.user = this.datosUser();
    this.user.then((value) => {
      (this.rol = value.roles[0].name), console.log(value.roles[0].name);
    });
    // this.convertir()
    // console.log(this.user)
    // console.log(this.user.Prom.nombres)
  },
};
</script>
<style lang="scss"></style>
