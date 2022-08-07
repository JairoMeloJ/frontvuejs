<template>
  <body>
    <div class="">
      <div class="container">
          <div class="row">
              <div class="column">
                  <h3>Lista de clientes </h3>
              </div>
          </div>
      </div>
    </div>
    <center marign-right="200">   
      <transition name="fade">
        <div id="modalCrear" class="modal-dialog modal-dialog-centered" v-if="showModal" >
        <h1>Ingrese los datos!</h1>
         
            Nombre: <input type="text" v-model="this.nombre"/>
            Apellido: <input type="text" v-model="this.apellido"/>
          
          <button class="btn" @click="PostApi(), showModal = false">Guardar</button><button class="btn" @click="showModal = false">Cerrar</button>
          
        </div>
      </transition>

      <button class="btnCrear btn" @click="showModal = true">Crear nuevo cliente...</button>
    </center>
    <div class="page-container">
      <div class="container">
        <div class="row">
          <div class="column">
            <table>
              <thead>
                <tr>
                  <th>#</th>
                  <th>Nombre</th>
                  <th>Apellido</th>
                  <th>Actualizar</th>
                  <th></th>
                  <th>Eliminar</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="todo of todos" v-bind:key="todo.id">
                  <td>{{todo.id}}</td>
                  <td>{{todo.firstName}}</td>
                  <td>{{todo.lastName}}</td>
                    <td><input type="text" v-model="todo.firstName"/></td>
                    <td><input type="text" v-model="todo.lastName"/></td>
                    <td><button class="btn" v-on:click="DeleteApi(todo.id)">Eliminar</button></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div> 
  </body>
  <footer class="site-footer">
    <div class="container">
      <div class="row">
        <div class="col-sm-12 col-md-6">
          <h6>Sobre la pagina</h6>
          <p class="text-justify">Soy <i>Jairo Gabriel Melo Jimenez </i> un joven interesado en la tecnologia y todos sus derivados, en este caso estoy presentando la practica final de mi training, presentando un FrontEnd con VueJs en conjunto con una api de C#.</p>
        </div>
      </div>
      <hr>
    </div>
    <div class="container">
      <div class="row">
        <div class="col-md-8 col-sm-6 col-xs-12">
          <p class="copyright-text">Copyright &copy; 2022 Todos los derechos reservados por 
          <a href="#">Jairo Melo</a>.
          </p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import axios from "axios";
const baseUrl = "https://jariolaapi.azurewebsites.net/users/";
export default {
  name: 'HelloWorld',
  data(){
    return{
      todos:[],
      showModal: false
    }
  },
  methods:
  {
    async GetApi() {
      await axios
        .get(baseUrl)
        .then((resp) => {
          this.todos = resp.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },    
    async PostApi() {
      await axios
        .post(baseUrl,{firstName:this.nombre,lastName:this.apellido })
        .then((resp) => {
          console.log(resp);
          this.nombre='';
          this.apellido='';
          this.GetApi();
        })
        .catch((err) => {
          console.log(err);
        });
    },
    async DeleteApi(id) {
      await axios
        .delete(baseUrl+id)
        .then((resp) => {
          console.log(resp);
          this.GetApi();
        })
        .catch((err) => {
          console.log(err);
        });
    },
    async PutApi(id,FirstName,LastName) {
      await axios
        .put(baseUrl+id,{"id":id,"firstName":this.FirstName,"lastName":this.LastName})
        .then((resp) => {
          console.log(resp);
          this.GetApi();
        })
        .catch((err) => {
          console.log(err);
        });
    }
  },
  mounted(){
    this.GetApi();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html {
  font-size: 18px; 
}
body {
  position: center;
  color:black;
  font-family: "Questrial", sans-serif;
  background-color: #ffec63;
  background-image: linear-gradient(
      45deg,
      #ffd966 25%,
      transparent 25%,
      transparent 75%,
      #ffd966 75%,
      #ffd966
    ),
    linear-gradient(
      -45deg,
      #ffd966 25%,
      transparent 25%,
      transparent 75%,
      #ffd966 75%,
      #ffd966
    );
  background-size: 60px 60px;
  background-position: 0 0;
  animation: slide 4s infinite linear;
}

@keyframes slide {
  from {
    background-position: 0 0;
  }

  to {
    background-position: -120px 60px;
  }
}

.navbar-brand{
  color:white;
  margin-left: 25px;
}
  header h2 {
      font-weight: 600;
      margin: 0;
      display: inline-block;
      border: 3px solid #606c76;
      padding: 5px 20px;
      font-size: 25px;
  }
  h3{
    margin-top: 70px;
  }

  header h2 a{
      color: #606c76;
  }

  .breadcrumb h3 {
      margin: 0;
  }

  .breadcrumb {
      background: transparent;
      padding: 50px 0;
      margin-bottom: 60px;
  }

  header {
      padding: 15px 0;
  }
  .page-container {
      min-height: calc(100vh - 323px);
  }
  .main-menu ul {
      margin: 0;
      padding: 0;
      list-style: none;
  }

  .main-menu ul li {
      display: inline-block;
      margin: 0;
  }

  .main-menu ul li a {
      display: block;
      padding: 11px 20px;
      text-transform: uppercase;
      font-weight: 400;
  }
.modal {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: auto;
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  padding: 1.6rem 3rem;
  border: 3px solid black;
  border-radius: 5px;
  background: white;
  box-shadow: 8px 8px 0 rgba(0, 0, 0, 0.2);
}
.message {
  font-size:1.1rem;
  margin-bottom: 1.6rem;
  margin-top: 0;
}
.btn {
  color:inherit;
    font-family:inherit;
  font-size: inherit;
  background: white;
  padding: 0.3rem 3.4rem;
  border: 3px solid black;
  margin-right: 2.6rem;
  box-shadow: 0 0 0 black;
  transition: all 0.2s;
}

.btn:last-child {
  margin: 0;
}

.btn:hover {
  box-shadow: 0.4rem 0.4rem 0 black;
  transform: translate(-0.4rem, -0.4rem);
}

.btn:active {
  box-shadow: 0 0 0 black;
  transform: translate(0, 0);
}

.options {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
  .site-footer
{
  background-color:#26272b;
  padding:45px 0 20px;
  font-size:15px;
  line-height:24px;
  color:#737373;
}
.site-footer hr
{
  border-top-color:#bbb;
  opacity:0.5
}
.site-footer hr.small
{
  margin:20px 0
}
.site-footer h6
{
  color:#fff;
  font-size:16px;
  text-transform:uppercase;
  margin-top:5px;
  letter-spacing:2px
}
.site-footer a
{
  color:#737373;
}
.site-footer a:hover
{
  color:#3366cc;
  text-decoration:none;
}
.footer-links
{
  padding-left:0;
  list-style:none
}
.footer-links li
{
  display:block
}
.footer-links a
{
  color:#737373
}
.footer-links a:active,.footer-links a:focus,.footer-links a:hover
{
  color:#3366cc;
  text-decoration:none;
}
.footer-links.inline li
{
  display:inline-block
}
.site-footer .social-icons
{
  text-align:right
}
.site-footer .social-icons a
{
  width:40px;
  height:40px;
  line-height:40px;
  margin-left:6px;
  margin-right:0;
  border-radius:100%;
  background-color:#33353d
}
.copyright-text
{
  margin:0
}
</style>
