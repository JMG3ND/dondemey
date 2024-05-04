<template>
    <div>
        <div class="skeleton">
            <header>
                <slot name="header"/>
            </header>
            <aside>
                <slot name="aside"/>
            </aside>
            <main class="skeleton__main">
                <slot name="main" />
            </main>
            <footer>
                <slot name="footer"/>
            </footer>
        </div>
    </div>
</template>

<script setup lang="ts">

</script>

<style lang="scss" scoped>

</style>