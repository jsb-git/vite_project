<script>
export default {
    props: {
        label: {required: true, type: String},
        genre: { required: true, type: String},
        year: {required: false, type: Number},
        id: {required: true, type: String}
    }        
}
</script>

<template>
    <div class="px-1">
        <input type="checkbox" :id="id" @change="$emit('checkbox-changed')" name="movielist" />
        <label :for="id" class="px-1"> {{label}} {{genre}} {{year}}</label>
    </div>
</template>
