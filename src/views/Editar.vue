<template>
        <div>
          <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Usuario</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="USUARIO" id="USUARIO" v-model="form.USUARIO">
                       </div>
                    </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Nombre</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="NOMBRE" id="NOMBRE" v-model="form.NOMBRE">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">Apellido paterno</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="APELLIDO_PATERNO" id="APELLIDO_PATERNO" v-model="form.APELLIDO_PATERNO">
                            </div>
                        </div>
                        <div class="col">
                          <label for="" class="control-label col-sm-5">Apellido materno</label>
                          <div class="col-sm-7">
                              <input type="text" class="form-control" name="APELLIDO_MATERNO" id="APELLIDO_MATERNO" v-model="form.APELLIDO_MATERNO">
                          </div>
                        </div> 
                    </div>
                    <div class="form-group left row">
                         <div class="col">
                            <label for="" class="control-label col-sm-2">Password</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="PASS" id="PASS" v-model="form.PASS">
                            </div>
                          </div>
                         <div class="col">
                              <label for="" class="control-label col-sm-2">Estado</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="ESTADO" id="ESTADO" v-model="form.ESTADO">
                              </div>
                        </div>
                    </div><br><br>
                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="editar()" >Editar</button>
                      <button type="button" class="btn btn-danger margen" v-on:click="eliminar()" >Eliminar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>
            </div>
          <!-- <Footer />   -->
        </div>
</template>
<script>
import Header from '@/components/Header.vue';
//import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
    name:"Editar",
    components:{
        Header,
        //Footer
    },
    data:function(){
        return {
            form:{
            "ID_USUARIO":"",
            "USUARIO" : "",
            "NOMBRE": "", 
            "APELLIDO_PATERNO":"",
            "APELLIDO_MATERNO" :"",
            "PASS" : "",
            "ESTADO" : ""
            }
        }
    },
    methods:{
        editar(){
            axios.put("https://apirest-tablausuario/usuario",this.form)
            .then( data =>{
                console.log(data);
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        eliminar(){
            var enviar = {
                "ID_USUARIO" : this.form.ID_USUARIO,
                "token" : this.form.token
            };
            axios.delete("https://apirest-tablausuario/usuario", { headers : enviar})
            .then( datos => {
                console.log(datos);
            this.$router.push("/dashboard");
            });
        }
    },
    mounted:function(){
        this.form.ID_USUARIO = this.$route.params.id;
        axios.get("https://apirest-tablausuario/usuario?id="+ this.form.ID_USUARIO)
        .then( datos => {
            this.form.USUARIO = datos.data[0].USUARIO;
            this.form.NOMBRE = datos.data[0].NOMBRE;
            this.form.APELLIDO_PATERNO = datos.data[0].APELLIDO_PATERNO;
            this.form.APELLIDO_MATERNO = datos.data[0].APELLIDO_MATERNO;
            this.form.PASS = datos.data[0].PASS;
            this.form.ESTADO = datos.data[0].ESTADO;
            this.form.token = localStorage.getItem("token");
            console.log(this.form);
        })
    }  
}
</script>
<style scoped>
.left{
    text-align: left;
};
.margen{
    margin-left: 15px;
    margin-right: 15px;;
}
</style>