<template>
    <div class="column">
        <h2>{{ title }}</h2>
        <slot>
            Aucune quête 
        </slot>
    </div>
</template>

<script>
export default {
    props: {
        title: String
    }
};
</script>

<style scoped> </style>