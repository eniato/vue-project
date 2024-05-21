<template>
    <div class="calculadora">
    <div>
        <h1>Calculadora VueJS</h1>
        <label for="primeiroNumero" class="numero1">Número 1:</label>
        <input type="number" id="primeiroNumero" v-model="estado.primeiroNumero" @input="calcularResultado">
    </div>
    <div>
        <label for="segundoNumero" class="numero1">Número 2:</label>
        <input type="number" id="segundoNumero" v-model="estado.segundoNumero" @input="calcularResultado">
    </div>
    <div>
        <label for="operacaoMatematica" class="operação">Operação:</label>
        <select id="operacaoMatematica" class="operação1" v-model="estado.operacaoMatematica" @change="calcularResultado">
        <option value="soma">Somar</option>
        <option value="subtracao">Subtrair</option>
        <option value="multiplicacao">Multiplicar</option>
        <option value="divisao">Dividir</option>
        </select>
    </div>
    <div>
        <h2 class="resultado">Resultado: {{ estado.resultado }}</h2>
    </div>
    </div>
</template>



<script setup>
import { reactive } from 'vue';

const estado = reactive({
    primeiroNumero: '',
    segundoNumero: '',
    operacoes: {
        soma: (a, b) => a + b,
        subtracao: (a, b) => a - b,
        multiplicacao: (a, b) => a * b,
        divisao: (a, b) => (b !== 0 ? a / b : 'Divisão por zero'),
    },
    resultado: 0,
});

const calcularResultado = () => {
    const { primeiroNumero, segundoNumero, operacaoMatematica } = estado;
    estado.resultado = estado.operacoes[operacaoMatematica](parseFloat(primeiroNumero), parseFloat(segundoNumero));
};
</script>



<style scoped>
.calculadora {
    max-width: 300px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0px 11px 5px 9px rgba(247,247,247,1);
}
.calculadora div {
    margin-bottom: 10px;
}

.numero1 {
    margin-right: 10px
}

.operação1 {
    width: 100%;
    margin-top: 10px;
    padding: 5px;
}

.operação {
    margin-right: 20px;
}

input {
    width: 100%;
    padding: 5px;
    border: 0;
    border-bottom: 2px solid rgb(200, 200 , 200);
    margin-bottom: 40px;
    outline: 0;
}

input:focus{
    border-bottom: 2px solid #424242;
}

.resultado {
    margin-top: 20%
}

* {
    background-color: rgb(236, 236, 236);
}
</style>
