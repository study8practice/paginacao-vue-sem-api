<template>
  <div>
    <div class="list">
      <div class="produto" v-for="(produto, index) in paginacaoProdutos" :key="index">
        {{ produto }}
      </div>
    </div>

    <button @click="prev()">anterior</button>
    <button @click="goTo(1)">primeiro</button>
    <ul>
      <li v-for="(pagina, i) in paginas" :key="i"
      @click="goTo(pagina)">
        {{pagina}}
      </li>
    </ul> 
    
    <button @click="next()">proximo</button>
    <button @click="goTo(paginasTotal)">última</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      page: 1,
      produtos: [ "produto 1", "produto 2", "produto 3", "produto 4", "produto 5",  "produto 6", "produto 7", "produto 8", "produto 9", "produto 10", "produto 11", "produto 12", "produto 13", "produto 14", "produto 15", "produto 16", "produto 17", "produto 18", "produto 19", "produto 20", "produto 1", "produto 2", "produto 3", "produto 4", "produto 5",  "produto 6", "produto 7", "produto 8", "produto 9", "produto 10", "produto 11", "produto 12", "produto 13", "produto 14", "produto 15", "produto 16", "produto 17", "produto 18", "produto 19", "produto 20", "produto 4", "produto 5",  "produto 6", "produto 4", "produto 5",  "produto 6"],
      produtosPorPagina: 6,
    }
  },
  methods: {
    next() {
      this.page++;

      const lastPage = this.page > this.paginasTotal;
      if (lastPage) {
        this.page = this.paginasTotal;
      };
    },
    prev(){
      this.page--;

      const firstPage = this.page < 1;
      if (firstPage) {
        this.page++;
      };
    },
    goTo(pg) {
    // se for passado uma pagina menor que 1, ele vai cai nesse if.
    if (pg < 1) {
      pg = 1;
    }

    this.page = +pg;
    // se você colocar apenas page, ele não vai ser um numero, quando você coloca um + ele vira um numero.

    // se for passado uma pagina maior que o total de pagina ele cai nesse if.
    if (pg > this.produtosTotal) {
      this.page = this.produtosTotal;
    }
  },
  },
  computed: {
    paginas() {
      const range = 5;
      const offset = Math.floor(range / 2) + 1;
      const pagesArray = [];

      for (let i = 1; i <= this.paginasTotal; i++) {
        pagesArray.push(i);
      }
      
      pagesArray.splice(0, this.page - offset);
      pagesArray.splice(range, this.paginasTotal);

      return pagesArray;
    },
    produtosTotal(){
      return this.produtos.length;
    },
    paginasTotal() {
      const total = this.produtosTotal / this.produtosPorPagina;
      return total !== Infinity ? Math.ceil(total) : 0;
    },
    paginacaoProdutos(){
      let page = this.page - 1;
      // estou tirando 1, porque o array começa em 0.
    let start = page * this.produtosPorPagina;
    let end = start + this.produtosPorPagina;

    return this.produtos.slice(start, end);
    }
  }
};
</script>

<style scoped>
li {
  display: inline-block;
}

li {
  padding: 2px 8px;
  border-radius: 2px;
  margin: 4px;
  cursor: pointer;
}
</style>
