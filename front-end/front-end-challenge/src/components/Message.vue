<template>
 <div class="message-container">
 <p>{{msg}}</p>
  
 </div>
</template>

<script>
export default {
    name: 'message',
    props: {
        msg: String
    }
}
</script>

<style scoped>
 p {
    background-color: green;
    color: black;
    text-align: center;
    margin-top: 10px;
    padding-left: 0px;
    height: 40px;
 }
</style>