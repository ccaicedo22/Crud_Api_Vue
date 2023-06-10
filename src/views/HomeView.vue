<template>
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
          <div class="table-responsive">
              <table class="table table-bordered table-hover">
                  <thead><tr><th>#</th><th>NOMBRE</th><th>DESCRIPCION</th><th>PRECIO</th><th>CANTIDAD</th><th>ACCIONES</th></tr></thead>
                  <tbody class="table-group-divider" id="contenido">
                    <tr v-for="prod, i in products " :key="prod.id">
                        <td>{{ (i+1) }}</td>
                        <td>{{ prod.name }}</td>
                        <td>{{ prod.description }}</td>
                        <td>${{new Intl.NumberFormat('es-mx').format(prod.price) }}</td>
                        <td>{{ prod.stock }}</td>
                        <td>
                            <RouterLink :to="{path:'edit/'+prod.id}" class="btn btn-warning">
                                <i class="fa-solid fa-edit"></i>
                            </RouterLink>&nbsp;
                            <button class ="btn btn-danger" v-on:click="eliminar(prod.id,prod.name)"> 
                                <i class="fa-solid fa-trash"></i>
                            </button>
                        </td>
                    </tr>
                  </tbody>
              </table>
          </div>
      </div>
  </div>
</template>
<script>
    import axios from 'axios';
    import {confirmar} from '../funciones'
    export default{
        data(){
            return { products:null}
        },
        mounted(){
            this.getProducts();
        },
        methods:{
            getProducts(){
                axios.get('http://127.0.0.1:8000/api/productos').then(
                    response =>(
                        this.products = response.data
                    )
                );
            },
            eliminar(id,nombre){
                confirmar(id,nombre);
            }
        }
    }
</script>
