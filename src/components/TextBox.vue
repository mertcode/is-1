<template>

    <div class="col">
        <label>{{ data.title }}</label>
        <input :type="data.type" class="form-control" :placeholder="data.title" :value="value" @input="onInput">
    </div>

</template>

<script>

    export default {
        name: 'TextBox',
        props: {
            data: {
                type: Object,
                required: true
            },
            value: {
                type: String,
                required: true
            }
        },
        methods: {
            onInput(e){
                this.$emit('input', e.target.value)
            }
        }
    }

</script>