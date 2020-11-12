<template>

    <div class="col">

        <label :for="data.name">{{ data.title }}</label>
        <input 
            class="form-control" 
            :placeholder="data.title" 
            :type="data.type" 
            v-model="localValue"
            :name="data.name"
        >
        
    </div>

</template>

<script>

    export default {
        name: 'Date',
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