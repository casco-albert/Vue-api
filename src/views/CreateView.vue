<template>
    <div class="row mt-3">
        <div class="col-md-6 offset-md-3">
            <div class="card">
                <div class="card-header bg-dark text-white text-center">Crear Productos</div>
                <div class="card-body">
                    <form @submit.prevent="guardar">
                        <div class="input-group mb-3">
                            <span class="input-group-text"><i class="fa-solid fa-gift"></i></span>
                            <input type="text" v-model="name" id="nombre" class="form-control"
                            maxlength="50" placeholder="Nombre" required>
                        </div>
                        <div class="input-group mb-3">
                            <span class="input-group-text"><i class="fa-solid fa-comment"></i></span>
                            <input type="text" v-model="description" id="descripcion" class="form-control"
                            maxlength="150" placeholder="Descripcion" required>
                        </div>
                        <div class="input-group mb-3">
                            <span class="input-group-text"><i class="fa-solid fa-dollar-sign"></i></span>
                            <input type="number" v-model="price" id="precio" class="form-control"
                            placeholder="Precio" step="0.01" required>
                        </div>
                        <div class="d-grid col-6 mx-auto">
                            <button type="submit" class="btn btn-success"><i class="fa-solid fa-floppy-disk"></i> Guardar</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { show_alerta, enviarSolicitud } from '../funciones';

export default {
    data() {
        return {
            name: '',
            description: '',
            price: '',
            url: 'http://127.0.0.1:8000/api/products'
        };
    },
    methods: {
        guardar() {
            if (this.name.trim() === '') {
                show_alerta('Escribe el nombre', 'warning', 'nombre');
            } else if (this.description.trim() === '') {
                show_alerta('Escribe la descripcion', 'warning', 'descripcion');
            } else if (this.price === '') {
                show_alerta('Escribe el precio', 'warning', 'precio');
            } else {
                const parametros = {
                    name: this.name.trim(),
                    description: this.description.trim(),
                    price: this.price
                };
                enviarSolicitud('POST', parametros, this.url, 'Producto Guardado!!!');
            }
        }
    }
};
</script>
