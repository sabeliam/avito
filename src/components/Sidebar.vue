<template>
    <aside>
        <div class="categories">
            <select v-model="selectedCategory">Все категории</select>
            <select v-for="category in categories" :key="category" :value="category"> {{ category }} </select>
        </div>
    </aside>
</template>

<script>
export default {
    
}
</script>