<template>
    <div class="column">
        <h2 class="column__title">{{ title }}</h2>
        <div class="column__list">
            <slot>
                <p class="column__empty">Aucune quête</p>
            </slot>
        </div>
    </div>
</template>
<script>
export default {
    props: { // Propriété reçue du parent (App.vue)
        title: String
    }
};
</script>
<style scoped>
    .column {
    background: linear-gradient(180deg, rgba(0,0,0,0.15), rgba(0,0,0,0.05)), var(--color-ocean-light);
    border: 2px solid rgba(0,0,0,0.35);
    border-radius: 6px;
    padding: 1rem 1rem 1.5rem;
    min-height: 200px;
    box-shadow:
        inset 0 1px 0 rgba(255,255,255,0.08),
        0 10px 20px rgba(0,0,0,0.35);
    position: relative;
    }

    .column::before {
    content: '';
    position: absolute;
    inset: 0;
    border-radius: 6px;
    border-top: 6px solid var(--accent, var(--color-brass));
    pointer-events: none;
    }

    .column.col-available { --accent: #3aa6a0; }
    .column.col-progress  { --accent: var(--color-brass); }
    .column.col-done       { --accent: var(--color-emerald); }
    .column.col-failed     { --accent: var(--color-rust); }

    .column__title {
    font-family: var(--font-utility);
    font-variant: small-caps;
    letter-spacing: 0.05em;
    color: var(--color-parchment);
    text-align: center;
    margin: 0.25rem 0 1.25rem;
    padding-bottom: 0.6rem;
    border-bottom: 1px solid rgba(255,255,255,0.15);
    }

    .column__list {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
    }

    .column__empty {
    font-family: var(--font-body);
    font-style: italic;
    text-align: center;
    color: rgba(236,223,180,0.5);
    padding: 1.5rem 0;
    }
</style>