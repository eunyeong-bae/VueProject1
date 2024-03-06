<template>
    <div>
        <img :src="product.image" class="room-img"/>
        <h4 @click="$emit('openModal', product.id)">{{ product.title }}</h4>
        <p>{{ product.price }}원</p>
        <p>{{ product.content }}</p>
    </div>
</template>

<script>
export default {
    name: 'CardList',
    props: {
        product: Object,
    }, 
}
</script>

<style>

</style>