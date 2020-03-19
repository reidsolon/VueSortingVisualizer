<template>
    <div class="row">
        <div class="col-12 action--container">
            <button class="btn btn-default" @click="$emit('generateArray')"> Generate Array </button>
            <slot name="range-slider"></slot>
            <button class="btn btn-default" @click="$emit('bubbleSort')"> Bubble Sort </button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            data: {
                arrayLength: 0,
            }
        }
    }
}
</script>
<style scoped>

</style>