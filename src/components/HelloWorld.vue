<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <strong>Input:</strong> <input v-model="input" />
    <br />
    <strong>Copy:</strong>
    <div>
      {{ output }}
    </div>
  </div>
</template>

<script>
const alphabet = "abcdefghijklmnopqrstuvwxyz";
export default {
  name: "HelloWorld",
  data: function() {
    return {
      input: ""
    };
  },
  props: {
    msg: String
  },
  computed: {
    output() {
      return Array.from(Array(this.input.length).keys())
        .map(index => {
          let code = this.input.charCodeAt(index);
          if ([8200, 8192, 8194, 8198, 8197, 8196].includes(code)) {
            return " ";
          }
          let codeHex = code.toString(16).toUpperCase();
          let charIndex = parseInt(codeHex.slice(-2), 16);
          return alphabet[charIndex - 138];
        })
        .join("")
        .replace(/  +/g, " ");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
