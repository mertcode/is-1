<template>

    <div class="col">
        <label>{{ data.title }}</label>
        <select class="form-control" :value="value" @change="change">
            <option>{{ data.title }}</option>
            <option v-for="(option, index) in data.options" :key="index" :value="option.value">
                {{option.text}}
            </option>
        </select>
    </div>

</template>

<script>

    export default {
        name: 'SelectBox',
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
            change(e){
                this.$emit('input', e.target.value)
            }
        }
    }

</script>