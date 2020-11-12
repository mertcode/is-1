<template>

    <div class="col">
        <label :for="data.name">{{ data.title }}</label>
        <select class="form-control" v-model="localValue" :name="data.name">
            <option v-for="(option, index) in data.options" :key="index" :value="option.value">
                {{option.text}}
            </option>
        </select>
    </div>

</template>

<script>

    export default {
        name: 'Select',
        props: {
            data: {
                type: Object,
                required: true
            }
        },
        data(){
            return {
                localValue: ''
            }
        },
        created(){
            this.$watch('localValue', (value) => {
                this.$emit('input', value)
            })
        }
    }

</script>