<template>
  <div>

    <input class="autocomplete" v-model="typed" @blur="verificaBlur($event)">
    <ul class="autocompleteList" v-if="showResult">
      <li v-if="noneFind">Nenhum item encontrado</li>
      <li class="autocompleteItemsList" v-for="result in results" @click="select(result)">{{ result }}</li>
    </ul>


  </div>
</template>

<script>

export default {

  data() {
    return {
      typed: '',
      minSearch: 3,
      showResult: false,
      noneFind: false,
      data: ['Carlos Maria', 'Maria', 'Carlitos', 'Marianita Car' ],

      results: ''

    }
  },

  watch: {
    typed() {
      if (this.typed.length >= this.minSearch) {

        let verifier = this.typed;
        let verify = this.data.filter(function(elem) {
          return elem == verifier
        });

        if (verify.length == 0){
          this.filtro();
        }

      }

      if (this.typed.length < this.minSearch) {
        this.showResult = false;
        this.results = ''
      }
    },



  },

  methods: {
    filtro() {
      let reg = new RegExp(this.typed.split('').join('\\w*').replace(/\W/, ""), 'i');

      let result = this.data.filter(function(elem) {
        if (elem.match(reg)) {
          return elem
        }
      });

      this.results = result;
      this.showResult = true;

      if (result.length == 0) {
        this.noneFind = true;
      } else {
        this.noneFind = false;
      }
    },

    select(result) {
      this.typed = result;
      this.showResult = false;
    },

    verificaBlur(event) {

      let self = this;

      setTimeout(function() {
        let verificador = self.typed;

        let verifica = self.data.filter(function(elem) {
          return elem == verificador
        });

          if (verifica.length == 0) {
            self.typed = '';
          }


      },260);


    }


  }


}
</script>

<style>

.autocomplete {
  box-sizing: border-box;
  display: block;
  width: 100%;
  padding: .375rem .75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  background-image: none;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: .25rem;
  transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}

.autocompleteList {
  z-index: 6;
  box-sizing: border-box;
  width: 100%;
  border-left: 1px solid #ced4da;
  border-right: 1px solid #ced4da;
  border-bottom: 1px solid #ced4da;
  list-style: none;
  margin: 0;
  padding: 0;
  font-size: 14px;
  font-family: Helvetica, sans-serif;
  padding: 12px;
}

.autocompleteItemsList {
  margin: 0;
  padding: 5px;
  cursor: default;
}

.autocompleteItemsList:hover {
  background-color: #eef4ff;
  font-weight: bold;
}

</style>
