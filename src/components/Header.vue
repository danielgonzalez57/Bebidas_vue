<script setup>
    import { computed } from 'vue';
    import { RouterLink, useRoute } from 'vue-router'
    import { useBebidasStore } from '../stores/bebidas'

    const route = useRoute();
    const store = useBebidasStore();

    const paginaInicio = computed(() => route.name === 'inicio')

    const handleSubmit = () => {

        store.obtenerRecetas()

    }
</script>

<template>
    <div>
        <header 
            class="bg-slate-800"
            :class="{header : paginaInicio}"
        >
            <div class="mx-auto container px-5 py-16">
                <div class="flex justify-between items-center">
                    <div>
                        <RouterLink :to="{name: 'inicio'}">
                            <img class="w-32" src="/img/logo.svg">
                        </RouterLink>
                    </div>

                    <nav class="flex gap-4">
                        <Router-link 
                            :to="{name: 'inicio'}"
                            class="text-white uppercase font-bold"
                            active-class="text-blue-500"
                        >
                            Inicio
                        </Router-link>
                        <Router-link 
                            :to="{name: 'favoritos'}"
                            class="text-white uppercase font-bold"
                            active-class="text-blue-500"
                        >
                            Favoritos
                        </Router-link>
                    </nav>
                </div>

                <form
                    class="md:w-1/2 2xl:w-1/3 bg-blue-600 my-32 p-10 rounded-lg shadow space-y-6"
                    v-if="paginaInicio"
                    @submit.prevent="handleSubmit"
                >

                    <div class="space-y-4">
                        <label 
                        class="block text-white uppercase font-extrabold text-lg"
                        for="ingrediente">Nombre o Ingredientes</label>
                        <input 
                        type="text"
                        id="ingrediente"
                        class="p-3 w-full rounded-lg focus:outline-none"
                        placeholder="Nombre o Ingredientes: ej. Vodka, Tequila, ect"
                        v-model="store.busqueda.nombre"
                        >
                    </div>

                    <div class="space-y-4">
                        <label 
                        class="block text-white uppercase font-extrabold text-lg"
                        for="ingrediente">Categoria</label>
                        <select 
                        type="text"
                        id="ingrediente"
                        class="p-3 w-full rounded-lg focus:outline-none"
                        v-model="store.busqueda.categoria"
                        >
                            <option value="">-- Seleccione --</option>
                            <option
                                v-for="categoria in store.categorias"
                                :key="categoria.strCategory"
                                :value="categoria.strCategory"
                            >{{ categoria.strCategory }}</option>
                        </select> 
                    </div>

                    <input
                        type="submit"
                        value="Buscar Recetas"
                        class="bg-blue-900 hover:bg-blue-950 cursor-pointer text-white font-extrabold w-full p-2 rounded-lg uppercase"
                    />
                </form>
            </div>
        </header>
    </div>
</template>

<style>
    .header{
        background-image: url('/img/bg.jpg');
        background-size: cover;
        background-position: center;
    }
</style>