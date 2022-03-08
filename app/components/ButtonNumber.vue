<template>
    <Button @tap="fnEnter" >
        <Span class="text">{{ buttonValue }}</Span>
    </Button>
</template>

<script>
export default {
    props: {
        buttonValue: {
            type: String
        }
    },
    methods: {
        fnEnter() {
            this.$emit('fnEnter', this.buttonValue)
        }
    }
}
</script>

<style lang="scss" scoped>
    Button {
        .text {
            text-align: center;
            font-size: 21px;
        }
    }
</style>