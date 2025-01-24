<template>
      <div class="personCard">
        <img :src="require(`../assets/${person.id}.jpg`)" />
      </div>
</template>
<script>
    export default {
        name: 'PersonCard',
        props: {
            person: {
                type: Object,
                default: null
            }
        }
    }
</script>
<style>
    .personCard {
        display:flex;
        justify-content: center;
        border: 1px solid black;
        border-radius: 10px;
        background-color: blanchedalmond;
        padding: 10px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);
    }
</style>
