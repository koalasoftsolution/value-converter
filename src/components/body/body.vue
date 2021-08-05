<template>
    <div class="container">
        <ValueConvert></ValueConvert>
        <TextConvert></TextConvert>
    </div>
</template>

<script>
    import ValueConvert from './value_convert/value_convert'
    import TextConvert from './convert_text/convert_text'
    export default {
        name: 'Body',
        components : {
            ValueConvert,
            TextConvert
        }
    }
</script>

<style scoped>
    .converter_area{
        margin: 40px 0px;
        padding: 12px;
        box-shadow: 0px 4px 12px 0px #e8e4e4;
    }
    
    label{
        font-size: 13px;
        font-weight: 700;
        color: gray;
    }

    .container{
        width: 500px;
    }
</style>