<template>
    <div class="container">
        <h1 class="titulo">Microcuentas de Cobro</h1>
        <div class="recibo">
            <div class="platos">
                <div class="platos-item">
                    <label for="nombre">Nombre de Plato</label>
                    <input type="text" id="nombre" v-model="nombre">
                </div>

                <div class="platos-item">
                    <label for="precio">Precio Plato</label>
                    <input type="text" id="precio" v-model.number="precio">
                </div>
                <div class="platos-item">
                    <label for="cantidad">Cantidad Plato</label>
                    <input type="text" id="cantidad" v-model.number="cantidad">
                </div>
                <div class="platos-buttons">
                    <button class="add-one" @click="agregarcantidad">Add</button>
                    <button class="remove-one" @click="eliminarcantidad">Remove</button>
                </div>

                <button class="add-plate" @click="agregarPlato" >Agregar Plato</button>
            </div>
            <div class="factura">
                <div class="factura-platos_agregados"></div>
                <div class="factura-precion_total"></div>
            </div>
        </div>
    </div>
</template>

<script>
    import { ref } from 'vue';

    export default {
        setup() {
            const nombre = ref("");
            const cantidad = ref(0);
            const precio = ref(0);
            const platos = ref([]);

            const agregarcantidad = () => {
                cantidad.value +=1
            }
            const eliminarcantidad = () => {
                if (cantidad.value > 0) {
                    cantidad.value -= 1;
                }else{
                    alert("Debe existir al menos un plato");
                }
            }
            const agregarPlato = () => {
                if (nombre.value && cantidad.value && precio.value > 0) {
                    platos.value.push({
                        nombre: nombre.value,
                        cantidad: cantidad.value,
                        precio: precio.value
                    });
                    // Limpiar los campos después de agregar un plato
                    nombre.value = "";
                    cantidad.value = 0;
                    precio.value = 0;
                }else if(nombre.value && cantidad.value > 0 && precio.value == 0){
                    platos.value.push({
                        nombre: nombre.value,
                        cantidad: cantidad.value,
                        precio: "Contesía"
                    });
                    // Limpiar los campos después de agregar un plato
                    nombre.value = "";
                    cantidad.value = 0;
                    precio.value = 0;
                }else {
                    alert("Por favor, complete todos los campos correctamente.");
                }
            };

            const eliminarPlato = (index) => {
                platos.value.splice(index, 1);
            };

            const calcularTotal = () => {
                let total = 0;
                platos.value.forEach(plato => {
                    if (!isNaN(plato.precio)){
                        total += plato.precio * plato.cantidad;
                    }

                });
                return total;
            };

            return {
                nombre, cantidad, precio, platos, agregarPlato, eliminarPlato, calcularTotal, agregarcantidad, eliminarcantidad
            };
        }
    };
</script>

<style scoped>
.container {
    background-color: rgb(68, 68, 68);
    border-radius: 2rem;
    justify-content: center;
    align-items: center;
}
.titulo {
    text-align: center;
    color: white;
    padding: 1rem;
    font-weight: 600;
}

.platos {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 1rem;
    margin-left: 2rem;
}

.platos-item {
    display: flex;
    justify-content: space-between;
    gap: 5rem;
}

.platos-item input {
    padding: 0.5rem;
    border-radius: 1rem;
    border: none;
}

.platos-buttons {
    display: flex;
    justify-content: space-between;
}

.platos-buttons button {
    padding: 0.5rem 4.8rem;
    border-radius: 1rem;
    color: white;
    border: none;
}

.platos-buttons button:first-child {
    background-color: rgb(155, 255, 155);
}

.platos-buttons button:last-child {
    background-color: rgb(255, 155, 155);
}

.add-plate {
    padding: 0.5rem 2rem;
    border-radius: 1rem;
    color: white;
    border: none;
    background-color: rgb(155, 155, 255);
}

.recibo {
    display: flex;
    justify-content: space-between;
    padding: 1rem;
}
</style>
