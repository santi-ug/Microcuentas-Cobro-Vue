<template>
    <div class="container">
        <h1 class="titulo">Microcuentas de Cobro</h1>
        <div class="recibo">
            <div class="platos">
                <div class="platos-item">
                    <label for="">Nombre de Plato</label>
                    <input type="text">
                </div>
            
        
                <div class="platos-item">
                    <label for="">Precio Plato</label>
                    <input type="text">
                </div>
            
        
                <div class="platos-buttons">
                    <button class="add-one">Add</button>
                    <button class="remove-one">Remove</button>
                </div>

                <button class="add-plate">Agregar Plato</button>
            </div>
            <div class="factura">
                <div class="factura-platos_agregados"></div>
                <div class="factura-precion_total"></div>
            </div>
        </div>
    </div>
</template>

<script></script>

<style scoped>
.container {
    background-color: rgb(68, 68, 68);
    border-radius: 2rem;
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
