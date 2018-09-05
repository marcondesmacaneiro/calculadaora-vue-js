<template>
  <div class="calculadora">
    <span class="display">{{corrente || 0}}</span>
    <span @click="limpar()" class="btn">C</span>
    <span @click="sinal()" class="btn">+/-</span>
    <span @click="porcento()" class="btn">%</span>
    <span @click="divisao()" class="btn operador">/</span>
    <span @click="adicionarValor('7')" class="btn">7</span>
    <span @click="adicionarValor('8')" class="btn">8</span>
    <span @click="adicionarValor('9')" class="btn">9</span>
    <span @click="multiplicacao()" class="btn operador">*</span>
    <span @click="adicionarValor('4')" class="btn">4</span>
    <span @click="adicionarValor('5')" class="btn">5</span>
    <span @click="adicionarValor('6')" class="btn">6</span>
    <span @click="subtracao()" class="btn operador">-</span>
    <span @click="adicionarValor('1')" class="btn">1</span>
    <span @click="adicionarValor('2')" class="btn">2</span>
    <span @click="adicionarValor('3')" class="btn">3</span>
    <span @click="adicao()" class="btn operador">+</span>
    <span @click="adicionarValor('0')" class="btn zero">0</span>
    <span @click="ponto()" class="btn">.</span>
    <span @click="igual()" class="btn operador">=</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      corrente: '',
      anterior: null,
      operador: null,
      operadorClicado: false
    }
  },
  methods: {
    limpar() {
      this.corrente = ''
    },
    sinal() {
      this.corrente =
        this.corrente.charAt(0) === '-'
          ? this.corrente.slice(1)
          : `-${this.corrente}`
    },
    porcento() {
      this.corrente = `${parseFloat(this.corrente) / 100}`
    },
    adicionarValor(numero) {
      if (this.operadorClicado) {
        this.corrente = ''
        this.operadorClicado = false
      }
      this.corrente = `${this.corrente + numero}`
    },
    ponto() {
      if (this.corrente.indexOf('.') === '-1') {
        this.adicionarValor('.')
      }
    },
    divisao() {
      this.operador = (a, b) => a / b
      this.setAnterior()
    },
    multiplicacao() {
      this.operador = (a, b) => a * b
      this.setAnterior()
    },
    subtracao() {
      this.operador = (a, b) => a - b
      this.setAnterior()
    },
    adicao() {
      this.operador = (a, b) => a + b
      this.setAnterior()
    },
    igual() {
      this.corrente = this.operador(
        parseFloat(this.anterior),
        parseFloat(this.corrente)
      )
      this.anterior = null
    },
    setAnterior() {
      this.anterior = this.corrente
      this.operadorClicado = true
    }
  }
}
</script>

<style scoped>
.calculadora {
  margin: 0 auto;
  width: 400px;
  font-size: 2em;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
}
.operador {
  background-color: orange;
  color: white;
}
</style>
