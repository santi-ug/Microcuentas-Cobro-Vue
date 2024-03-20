<template>
    <div class="container">
        <h1 class="titulo">Microcuentas de Cobro</h1>
        <div class="recibo">
            <div class="platos">
                <h1>Agregar Un Plato</h1>
                <div class="platos-item">
                    <label for="nombre">Nombre de Plato:</label>
                    <input type="text" id="nombre" v-model="nombre">
                </div>

                <div class="platos-item">
                    <label for="precio">Precio Plato:</label>
                    <input type="text" id="precio" v-model.number="precio">
                </div>
                <div class="platos-item">
                    <label for="cantidad">Cantidad del Plato:</label>
                    <div class="platos-buttons">
                        <button class="remove-one" @click="eliminarcantidad">-</button>
                        <input type="text" id="cantidad" v-model.number="cantidad">
                        <button class="add-one" @click="agregarcantidad">+</button>
                    </div>
                </div>


                <button class="add-plate" @click="agregarPlato" >Agregar Plato</button>
            </div>
            <div class="factura">
                <h1>Platos Agregados</h1>
                <div class="factura-platos_agregados">
                    <table class="factura-platos-table" >
                        <tbody v-for="(plato, index) in platos" :key="index">

                            <tr>
                                <td>{{ plato.cantidad }}x</td>
                                <td>{{ plato.nombre }}</td>
                                <td>${{ plato.precio }}</td>
                                <button @click="eliminarPlato(index)">X</button>
                            </tr>
                            
                        </tbody>
                    </table>
                </div>
                <div class="factura-precio_total">
                    <h1>Precio Total: <strong> ${{ calcularTotal() }} </strong></h1>
                </div>
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
    color: white;
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
    gap: 1.5rem;
    margin-left: 2rem;
}

.platos > h1 {
    font-size: 1.5rem;
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
    gap: 1rem;
}

.platos-buttons input {
    padding: 0.5rem;
    border-radius: 1rem;
    border: none;
    width: 6.7rem;
    text-align: center;

}

.platos-buttons button {
    padding: 0.5rem 0.8rem;
    border-radius: 100%;
    color: white;
    border: none;
}

.platos-buttons button:first-child {
    background-color: rgb(97, 187, 97);
}

.platos-buttons button:last-child {
    background-color: rgb(255, 155, 155);
}

.add-plate {
    padding: 0.5rem 2rem;
    border-radius: 1rem;
    color: white;
    border: none;
    font-size: 1rem;
    font-weight: 600;
    background-color: rgb(155, 155, 255);
}

.recibo {
    display: flex;
    justify-content: space-evenly;
    gap: 4rem;
    padding: 1rem;
}

.factura {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 1rem;
    margin-right: 4rem;
    font-size: 0.7rem;
}

.factura-platos_agregados {
    display: flex;
    flex-direction: column;
    align-items: end;
    gap: 1rem;
}

.factura-platos_agregados-platos {
    display: flex;
    flex-direction: column;
    gap: 1rem;

}

.factura > h1 {
    color: white;
    font-size: 1.5rem;
}

.factura-precio_total h1 {
    color: white;
    font-size: 1.25rem;
}

.factura-precio_total h1 strong {
    color: rgb(255, 155, 155);
    font-size: 1.5rem;
    margin-left: 1rem;
}

.factura-platos_agregados-plato {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
    border-radius: 1rem;
    color: white;
}

/* RECEIPT */
.factura-platos-table {
    border-collapse: collapse;
}

.factura-platos-table td,
.factura-platos-table button {
    padding: 0.5rem 1rem;
    color: white;
    font-size: 0.8rem;
    font-weight: 600;
    text-align: right;
}

.factura-platos-table button {
    border: none;
    padding: 0.18rem 0.35rem;
    border-radius: 100%;
    background-color: rgb(255, 155, 155);
    transform: translateY(0.45rem);
}



.factura-platos_agregados-plato button {
    padding: 0.2rem 0.4rem;
    border-radius: 50%;
    color: white;
    border: none;
    background-color: rgb(255, 155, 155);
}
</style>
