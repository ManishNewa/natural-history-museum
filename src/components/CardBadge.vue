<template>
    <div class="card-badge">
        <slot />
    </div>
</template>

<script>
export default {
    name: 'CardBadge',
}
</script>

<style lang="scss" scoped>
.card-badge {
    position: absolute;
    height: 40px;
    width: 50px;
    top: -20px;
    right: -20px;
}
</style>