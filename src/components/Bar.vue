<template>
    <div class="barContainer" :style="'height:'+value+'px' " :class="'BAR_'+value">
    </div>
</template>
<script>
    export default {
        props: {
            value: Number,
        },
        data() {
            return {
                data: {
                    barValue: this.value
                }
            }
        }

    }
</script>
<style scoped>
.barContainer{background-color: #6399f1; display: inline-block; margin-left: 3px; width: 10px}
</style>