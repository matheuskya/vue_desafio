<script setup>
import { ref } from "vue";

// Estrutura para um novo filme
const novoFilme = ref({
    titulo: "",
    diretor: "",
    ano: "",
});

// Lista de filmes
const filmes = ref([]);

// Função para adicionar filme
const adicionarFilme = () => {
    // Validação dos campos
    if (
        !novoFilme.value.titulo ||
        !novoFilme.value.diretor ||
        !novoFilme.value.ano
    ) {
        alert("Por favor, preencha todos os campos!");
        return;
    }

    // Adiciona o filme à lista
    filmes.value.push({
        ...novoFilme.value,
        id: Date.now(), // Identificador único para cada filme
    });
    console.log(filmes);

    // Limpa os campos
    novoFilme.value = {
        titulo: "",
        diretor: "",
        ano: "",
    };
};

// Função para remover filme
const removerFilme = (id) => {
    filmes.value = filmes.value.filter((filme) => filme.id !== id);
};
</script>

<template>
    <div class="container">
        <h1>Cadastro de Filmes</h1>

        <div class="form-container">
            <input
                v-model="novoFilme.titulo"
                placeholder="Título do filme"
                type="text"
            />

            <input
                v-model="novoFilme.diretor"
                placeholder="Nome do diretor"
                type="text"
            />

            <input
                v-model="novoFilme.ano"
                placeholder="Ano de lançamento"
                type="number"
            />

            <button @click="adicionarFilme">Cadastrar Filme</button>
        </div>

        <div class="lista-filmes">
            <h2>Filmes Cadastrados</h2>

            <div v-if="filmes.length === 0" class="mensagem-vazia">
                Nenhum filme cadastrado ainda.
            </div>

            <div
                v-else
                class="filme-item"
                v-for="filme in filmes"
                :key="filme.id"
            >
                <div class="filme-info">
                    <h3>{{ filme.titulo }}</h3>
                    <p>Diretor: {{ filme.diretor }}</p>
                    <p>Ano: {{ filme.ano }}</p>
                </div>
                <button @click="removerFilme(filme.id)" class="btn-remover">
                    Remover
                </button>
            </div>
        </div>
    </div>
</template>
