<template>
    <div class="d-flex align-items-center justify-content-end mt-4">
        <button type="button" class="btn btn-light d-flex align-items-center justify-content-center" @click="clear">
            <svg width="1.5em" height="1.5em" viewBox="0 0 16 16" class="bi bi-x mr-1" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
            </svg>
            Clear
        </button>

        <button type="submit" class="btn btn-light ml-2 d-flex align-items-center justify-content-center" @click.prevent="submit">
            <svg width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-search mr-2" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M10.442 10.442a1 1 0 0 1 1.415 0l3.85 3.85a1 1 0 0 1-1.414 1.415l-3.85-3.85a1 1 0 0 1 0-1.415z"/>
                <path fill-rule="evenodd" d="M6.5 12a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zM13 6.5a6.5 6.5 0 1 1-13 0 6.5 6.5 0 0 1 13 0z"/>
            </svg>
            Search
        </button>
    </div>
</template>

<script>
    export default {
        name: 'FormActions',
        methods: {
            clear(){
                this.$emit('clear')
            },
            submit(){
                this.$emit('submit')
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>