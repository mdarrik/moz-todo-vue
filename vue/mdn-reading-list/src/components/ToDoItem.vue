<template>
    <div><input type="checkbox" :id="id" :checked="isChecked" /><label :for="id">{{label}}</label></div>
</template>
<script>
import uniqueId from 'lodash.uniqueid'
export default {
    props: {
        label: {required: true, type: String},
        checked: {default: false, type: Boolean}
    },
    data() {
        return {
           isChecked : this.checked,
           id: uniqueId('todo-')
        }
    },
}
</script>  