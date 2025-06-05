<template>
    <label class="label"> <!--Fusion des classes-->
        <input type="checkbox" @change="onChange">
        {{ label }} <!--J'utilise directement label-->
    </label>

</template>

<script setup>
const props = defineProps({ // props ce que reçoit le composant de ce qui descend de App.vue
    label: String
})

const emits = defineEmits(["check", "uncheck"]) // Ce qu'on envoie vers le parent
const onChange = (event) => { // on utilise les évènement avec le defineEmits
    if (event.currentTarget.checked) {
        emits("check", event.currentTarget) // currentTarget fait référence à la checkbox
    } else {
        emits("uncheck", event.currentTarget)
    }
}
</script>