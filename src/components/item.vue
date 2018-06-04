<template>
    <div class="name">
        <section class="preview">
            <img src="//thumbs.trulia-cdn.com/pictures/thumbs_3/zillowstatic/ISqdrfht0ic25n1000000000.jpg" alt="1908 Pinsky Ln, North Las Vegas, NV">
        </section>
        <section class="details">
        <ul>
            <li>{{ item.price }}</li>
            <li>{{ item.bedrooms }}</li>
            <li>{{ item.baths }}</li>
            <li>{{ item.area }}</li>
	    </ul>
        </section>
    </div>
</template>

<script>
    export default {
        props: ['item']
    }
</script>
<style scoped>
    .name {
        padding: 10px;
    }
</style>


