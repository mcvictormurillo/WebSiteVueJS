<template>
  <li>
    <h2>
        <a :href="artist.url"> {{artist.name}} </a> <br />
        <img :src="artist.image[2]['#text']"/>
        
    </h2> 
</li>
</template>
<script>

export default {
    name:'artist',
    props: ['artist']
}
</script>

<style lang="stylus" scoped>
li 
    display: block;
    margin: 10px 0;

</style>

