<template>
    <div class="flexslider">
        <ul class="slides">
            <slot></slot>
            <li v-for="(src, index) in images" :key="'i' + index"><img :src="src"></li>
            <li v-for="(item, index) in items" :key="index">  
                <div v-if="typeof item == 'string'" v-html="item"></div>
                <component :is="item" v-bind="{options, index}" v-else></component>
            </li>
        </ul>
    </div>
</template>

<script>


if(!window.jQuery) window.jQuery = require('jquery');

if(!window.jQuery.fn.flexslider) require('flexslider');


export default {

    props: {
        images: {
            type: Array,
            default: () => []
        },
        items: {
            type: Array,
            default: () => []
        },
        options: {
            type: Object,
            default: () => { return {} }
        }
    },

    mounted(){
        window.jQuery(this.$el).flexslider(this.options);
    }
}
</script>

<style lang="scss">
    @import "~flexslider/flexslider.css";
</style>