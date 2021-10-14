<template>
    <div class="page-success">
        <div class="columns is-multiline"> 
            <div class="column is-12">
                <h1 class="title has-text-success has-text-centered">Thank you for shopping !</h1>

                <p class="has-text-centered has-text-black">Your order will be processed within 48 hours</p>
                <router-link to="/my-account" class="button ml-5 align-center">
            <strong>Your orders</strong></router-link
          >
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Success',
    mounted() {
        document.title = 'Success | Accessory'
    },
}
</script>