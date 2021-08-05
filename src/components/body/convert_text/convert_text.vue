<template >
    <div class="converter_area">
            <div class="heading_area">
                <div class="row">
                    <div class="col-md-12">
                        <div class="heading">
                            <h6>Enter The Text</h6> 
                        </div>
                    </div>
                </div>
            </div>

            <div class="converter_field_area">
                <form action="">
                    <div class="form-group">
                        <label>Text : </label>
                        <textarea class="form-control form-control-sm" cols="10" rows="3" placeholder="Enter the text" v-model="convert_text.text"></textarea>
                    </div>

                    <div class="form-group mt-1">
                        <label>Binary : </label>
                        <textarea class="form-control form-control-sm" cols="10" rows="3" placeholder="Enter the binary number" v-model="convert_text.binary"></textarea>
                    </div>

                    <div class="form-group mt-2 row">
                        <div class="col-md-8">
                            <span v-if="invalidBinary" class="text-danger">
                                Invalid Input.
                            </span>
                        </div>
                        <div class="col-md-4 text-end">
                            <button class="btn btn-sm btn-danger">Reset</button>
                        </div>
                        
                    </div>
                </form>
            </div>
        </div>
</template>


<script>
    function textToBinary(text) {
        let charCodeArray = [];
        for (let t of text) {
            charCodeArray.push(t.charCodeAt(t));
        }

        let binaryArray = charCodeArray.map(function (c) {
             return c.toString(2);
        });

        return binaryArray;
    }

    function binaryToText(txt) {
        let text = '';
        for(let t of txt){
            let char = String.fromCharCode(parseInt(t, 2));
            text = text.concat(char);
        }
        return text;
    }

    export default {
        name: 'convert_text',
        data() {
            return {
                convert_text: {
                    text : '',
                    binary : '',
                },
                invalidBinary : false,
            }
        },

        watch: {
            "convert_text.text": function(value) {
                if (value.length === 0) {
                    this.convert_text.binary = '';
                }else{
                    let result = textToBinary(value);
                    this.convert_text.binary = result.join(' ');
                }
            },

            "convert_text.binary": function(value) {
                if (value.length === 0) {
                    this.convert_text.text = '';
                }else{
                    let textArray = value.split(' ');
                    let result2 = binaryToText(textArray);
                    this.convert_text.text = result2;
                }
            },
        }
    }
</script>