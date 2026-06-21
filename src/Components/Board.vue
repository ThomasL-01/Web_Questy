<template>
    <div class = "quest-table">   
        <slot>
                Emplacement des colonnes
        </slot>
    </div>
</template>

<script >
export default {
}
</script>
<style scoped>
    .quest-table {
    margin: 0 auto 2rem;
    max-width: 1500px;
    padding: 1.5rem;
    border-radius: 8px;
    background:
        repeating-linear-gradient(90deg, rgba(0,0,0,0.08) 0 2px, transparent 2px 26px),
        linear-gradient(160deg, #6b4423, #4a2e16);
    box-shadow:
        0 18px 35px rgba(0,0,0,0.5),
        inset 0 0 0 6px rgba(0,0,0,0.25),
        inset 0 0 0 8px var(--color-brass);
    }
</style>