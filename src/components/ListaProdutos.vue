<template>
  <article>
    <div class="column-left"></div>

    <div class="column-center">
      <div class="box" v-if="!loading">
        <table>
          <caption>
            Lista de Produtos
          </caption>
          <thead>
            <tr>
              <th>Foto</th>
              <th>Nome</th>
              <th>Descrição</th>
              <th>Valor</th>
              <th></th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="produto in produtos" :key="produto.id">
              <td>
                <img
                  :src="this.url + 'storage/' + produto.imagem"
                  :alt="produto.nome"
                />
              </td>
              <td>{{ produto.nome }}</td>
              <td>{{ produto.descricao }}</td>
              <td>R$ {{ produto.valor }}</td>
              <td>
                <button @click="deleteProduto(produto.id, produto.nome)">
                  Excluir Produto
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div v-else>
            <SpinnerCir/>
      </div>
    </div>

    <div class="column-right"></div>
  </article>
</template>

<script>
import axios from "axios";

import SpinnerCir from "./SpinnerCir.vue";


export default {
  name: "ListaProdutos",
  components: {
    SpinnerCir,
   
},
  data() {
    return {
      produtos: null,
      url: "http://127.0.0.1:8000/",
      loading: true,
    };
  },
  methods: {
    getProdutos() {
      this.loading = true;
      axios
        .get(`${this.url}api/getProducts`)
        .then((response) => {
          if (response.status == 200) {
            this.produtos = response.data;
          } else {
            alert("Algo deu errado Erro" + response.status);
            console.log(response.status);
          }
        })
        .catch((erro) => {
          alert("Algo deu errado Erro" + erro);
          console.log(erro);
        })
        .finally(() => {
          this.loading = false;
        });
    },
    deleteProduto(id_produto, nome_produto) {
      
      axios
        .delete(`${this.url}api/deleteProduct/${id_produto}`)
        .then((response) => {
          //alert("Produto" + nome_produto  +  response.data);
          console.log(response.data);
        })
        .catch((erro) => {
          alert(" Erro a excluir produto" + nome_produto + erro);
          console.log(erro);
        })
        .finally(() => {
          this.getProdutos();
        });
    },
  },
  created() {
    this.getProdutos();
  },
};
</script>

<style scoped>
article {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

article .column-center {
  background-color: rgb(176, 171, 171);
  width: 60%;
  height: 100%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 10px;
  padding: 2px;
  margin-top: 20px;
}
.box {
  border-collapse: collapse;
  width: 100%;
  padding-bottom: 10px;
}

.box table {
  border-collapse: collapse;
  border-spacing: 0;
  width: 100%;
  /* border: 1px solid #ddd; */
}

.box caption {
  font-size: 30px;
}
.box thead {
  background-color: black;
  color: white;
}
.box th {
  text-align: center;
  padding: 8px;
  font-size: 25px;
}
.box td {
  text-align: center;
  padding: 8px;
  font-size: 20px;
  border-block-end: 2px solid black;
}

.box img {
  width: 50px;
  height: 50px;
}

.box button {
  margin-bottom: 10px;
  color: white;
  font-weight: bold;
  height: 40px;
  width: 100%;
  border-radius: 4px;
  background-color: rgb(227, 48, 39);
  border: none;
}
.box button:active {
  background-color: #a84340;
  box-shadow: 0 2px #666;
  transform: translateY(2px);
}

@media screen and (max-width: 800px) {
  article .colunm-left .column-right {
    visibility: hidden;
  }
  article .column-center {
    background-color: rgb(176, 171, 171);
    width: 100%;
  }
}
</style>