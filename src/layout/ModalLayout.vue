<template>
    <div id="backdrop" @click.self="closeModal" :style="{display: visible ? 'flex' : 'none'}">
        <card id="modalCard" class="card" :title="modalTitle">
            <slot></slot>
        </card>
    </div>
</template>
<script>
export default{
    props: {
        visible: Boolean,
        modalTitle: String
    },
    methods: {
        closeModal() {
            this.$emit("update:visible", false);
        }
    }
}
</script>
<style>
#modal-container{
    display: flex;
    z-index: 2;
}

#backdrop{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

#modalCard {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
    width: auto;
    max-width: 90%;
}
</style>