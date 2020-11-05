<template>
  <div>
    <Header />
    <div class="container">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">Evento</th>
            <th scope="col">Boletos Disponibles</th>
            <th scope="col">Descripcion</th>
            <th scope="col">Accion</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="ticket in Listadetickets" :key="ticket.id">
            <td>{{ticket.event_name}}</td>
            <td>{{ticket.quantity}}</td>
            <td>{{ticket.description}}</td>
            <td><button type="button" class="btn btn-success">Reservar</button></td>
          </tr>
        </tbody>
      </table>
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import axios from 'axios';

export default {
  name: "Dashboard",
  data(){
      return{
          Listadetickets: null,
          pagina: 1,

      }
  },
  components: {
    Header,
    Footer,
  },
  mounted: function(){
      let direccion = "http://localhost:8000/api/tickets?page="+this.pagina;
      axios.get(direccion).then(data =>{
          this.Listadetickets = data.data;
      })
  }
};
</script>

<style lang="stylus" scoped></style>