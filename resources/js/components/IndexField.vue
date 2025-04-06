<template>
    <span>{{ field.value }}</span>
</template>

<script>
export default {
    props: {
        resourceName: String,
        field: Object
    }
}
</script>
