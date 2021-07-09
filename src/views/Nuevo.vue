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
                       <label for="" class="control-label col-sm-2">NOMBRE</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="NOMBRE" id="NOMBRE" v-model="form.NOMBRE">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">APELLIDO_PATERNO</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="APELLIDO PATERNO" id="APELLIDO_PATERNO" v-model="form.APELLIDO_PATERNO">
                            </div>
                        </div>
                        <div class="col">
                          <label for="" class="control-label col-sm-5">APELLIDO MATERNO</label>
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
                              <label for="" class="control-label col-sm-2">ESTADO</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="ESTADO" id="ESTADO" v-model="form.ESTADO">
                              </div>
                        </div>
                    </div><br><br>
                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="guardar()" >Guardar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>
            </div>
        <!-- <Footer /> -->
    </div>
</template>
<script>
import Header from '@/components/Header.vue'
//import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"Nuevo",
    data:function(){
        return {
            form:{
                "USUARIO" : "",
                "NOMBRE": "", 
                "APELLIDO_PATERNO":"",
                "APELLIDO_MATERNO" :"",
                "PASS" : "",
                "ESTADO" : ""
            }
        }
    },
    components:{
        Header,
        //Footer
    },
    methods:{
        guardar(){
            this.form.token = localStorage.getItem("token");
            axios.post("https://apirest-tablausuario/usuario",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Hecho","Usuario creado","success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }   
    }
}
</script>
<style scoped>
.left{
    text-align:  left;
}
</style>