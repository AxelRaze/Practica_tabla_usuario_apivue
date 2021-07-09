<template>
    <div>
        <Header/>
        <div class="container izquierda">
            <button class="btn btn-primary" v-on:click="nuevo()" >Nuevo usuario</button>
                <br><br>
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">USUARIO</th>
                        <th scope="col">NOMBRE</th>
                        <th scope="col">APELLIDO_PATERNO</th>
                        <th scope="col">APELLIDO_MATERNO</th>
                        <th scope="col">PASS</th>
                        <th scope="col">ESTADO</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="usuario in Listausuario" :key="usuario.ID_USUARIO" v-on:click="editar(usuario.ID_USUARIO)">
                        <th scope="row">{{ usuario.ID_USUARIO}}</th>
                        <td>{{ usuario.USUARIO }}</td>
                        <td>{{ usuario.NOMBRE }}</td>
                        <td>{{ usuario.APELLIDO_PATERNO }}</td>
                        <td>{{ usuario.APELLIDO_MATERNO }}</td>
                        <td>{{ usuario.PASS }}</td>
                        <td>{{ usuario.ESTADO }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <Footer/>
    </div>
</template>
<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default{
    name: "Dashboard",
    data(){
        return{
            Listausuario:null,
            pagina:1
        }
    },
    components:{
        Header,
        Footer
    },
    methods:{
            editar(id){
                this.$router.push('/editar/' + id);
            },
            nuevo(){
                this.$router.push('/nuevo');
            }
    },
    mounted:function(){
        let direccion = "https://apirest-tablausuario/usuario?page=" + this.pagina;
        axios.get(direccion).then(data=> {
            this.Listausuario = data.data;
        })
    }
}
</script>
<style scoped>
.izquierda{
        text-align: left;
    }
</style>