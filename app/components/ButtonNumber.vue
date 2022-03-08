<template>
    <Button v-on="$attrs" >
        <Span class="text">{{ buttonValue }}</Span>
    </Button>
</template>

<script>
export default {
    props: {
        buttonValue: {
            type: String
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