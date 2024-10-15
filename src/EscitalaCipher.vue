<template>
  <div class="container mt-5">
    <h1 class="mb-4">Escítala Cipher</h1>

    <div class="mb-3">
      <label for="message" class="form-label">Mensaje:</label>
      <textarea id="message" class="form-control" rows="4" v-model="message"></textarea>
    </div>

    <div class="mb-3">
      <label for="key" class="form-label">Valor K:</label>
      <input type="number" id="key" class="form-control" v-model="key" />
    </div>

    <div class="mb-3">
      <label class="form-label">Operación:</label>
      <div>
        <label class="form-check-label">
          <input type="radio" value="encrypt" v-model="operation" class="form-check-input"> Cifrar
        </label>
        <label class="form-check-label">
          <input type="radio" value="decrypt" v-model="operation" class="form-check-input"> Descifrar
        </label>
      </div>
    </div>

    <div class="mb-3">
      <button class="btn btn-primary" @click="performOperation">Realizar Operación</button>
    </div>

    <div class="mb-3">
      <p><strong>Mensaje Cifrado/Descifrado:</strong></p>
      <textarea class="form-control" rows="4" v-model="result" readonly></textarea>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "",
      key: 3, // Valor K
      result: "",
      operation: "encrypt", // Inicialmente cifrar
    };
  },
  methods: {
  performOperation() {
      if (this.operation === "encrypt") {
        this.result = this.performEncryption(this.message, this.key);
      } else if (this.operation === "decrypt") {
        this.result = this.performDecryption(this.message, this.key);
      }
    },
    performEncryption(message, key) {
      const numRows = Math.ceil(message.length / key);
      let grid = new Array(numRows).fill("");

      for (let i = 0; i < message.length; i++) {
        const row = i % numRows;
        grid[row] += message[i];
      }

      return grid.join("");
    },
    performDecryption(encryptedMessage, key) {
      const numRows = Math.ceil(encryptedMessage.length / key);
      const numCols = key;
      const grid = new Array(numRows).fill("");

      for (let i = 0; i < encryptedMessage.length; i++) {
        const col = i % numCols;
        const row = Math.floor(i / numCols);
        const index = col * numRows + row; // Calcular el índice correcto
        grid[index] = encryptedMessage[i];
      }

      return grid.join("");
    }





  },
};
</script>
