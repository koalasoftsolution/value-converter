<template >
    <div class="converter_area">
            <div class="heading_area">
                <div class="row">
                    <div class="col-md-12">
                        <div class="heading">
                            <h6>Enter The Value</h6> 
                        </div>
                    </div>
                </div>
            </div>

            <div class="converter_field_area">
                <form  v-on:submit.prevent="resetNumber">
                    <div class="form-group">
                        <label>Decimal : </label>
                        <input type="text" class="form-control form-control-sm" v-model="convert_number.decimal">
                    </div>

                    <div class="form-group mt-1">
                        <label>Binary : </label>
                        <input type="text" class="form-control form-control-sm" v-model="convert_number.binary">
                    </div>

                    <div class="form-group mt-1">
                        <label>Octal : </label>
                        <input type="text" class="form-control form-control-sm" v-model="convert_number.octal">
                    </div>

                    <div class="form-group mt-1">
                        <label>Hexadecimal : </label>
                        <input type="text" class="form-control form-control-sm" v-model="convert_number.hexadecimal">
                    </div>

                    <div class="form-group mt-2 row">
                        <div class="col-md-8">
                            <span v-if="invalidNumber" class="text-danger">
                                Invalid Input.
                            </span>
                        </div>
                        <div class="col-md-4 text-end">
                            <button type="submit" class="btn btn-sm btn-danger">Reset</button>
                        </div>
                        
                    </div>
                </form>
            </div>
        </div>
</template>


<script>
    function invalidBinary(text) {
        let text1 = text.toString();
        for (let t of text1) {
           if (t !== '0' && t !== '1') return true;
        }
        return false;
    }

    function invalidOctal(text) {
        let text1 = text.toString();
        for (let t of text1) {
           if (parseInt(t) < 0 || parseInt(t) > 7) return true;
        }
        
        return false;
    }

    
    function invalidHaxa(text) {
        let text1 = text.toString();
        for (let t of text1) {
           if (
               (t < '0' || t > '9') &&
               (t < 'A' || t > 'F') &&
               (t < 'a' || t > 'a')
           ) {
                return true;
           }
        }

        return false;
    }

    export default {
        name: 'Body',
        data() {
            return {
                convert_number: {
                    decimal : 0,
                    binary : 0,
                    octal : 0,
                    hexadecimal : 0,
                },
                invalidNumber : false,
            }
        },

        watch: {
            "convert_number.decimal": function(value) {
                let decimal = parseInt(value) || 0;
                this.convert_number.decimal = decimal;
                this.convert_number.binary = decimal.toString(2);
                this.convert_number.octal = decimal.toString(8);
                this.convert_number.hexadecimal = decimal.toString(16);
            },

            "convert_number.binary": function(value) {
                 
                 if (invalidBinary(value)) {
                     this.invalidNumber = true;
                 } else {
                     this.invalidNumber = false;
                 }
                let decimal = parseInt(value, 2) || 0;
                this.convert_number.decimal = decimal;
                this.convert_number.binary = value || 0;
                this.convert_number.octal = decimal.toString(8);
                this.convert_number.hexadecimal = decimal.toString(16);
            },

            "convert_number.octal": function(value) {
                
                 let decimal = parseInt(`0${value}`, 8);
                 if (invalidOctal(value)) {
                     this.invalidNumber = true;
                 } else {
                     this.invalidNumber = false;
                 }
                 console.log(this.invalidNumber);
                 
                this.convert_number.decimal = decimal;
                this.convert_number.binary = decimal.toString(2);
                this.convert_number.octal = value ? value : 0;
                this.convert_number.hexadecimal = decimal.toString(16);
            },

            "convert_number.hexadecimal": function(value) {
                
                 let decimal = parseInt(`0x${value}`, 16) || 0;
                 if (invalidHaxa(value)) {
                     this.invalidNumber = true;
                 } else {
                     this.invalidNumber = false;
                 }

                this.convert_number.decimal = decimal;
                this.convert_number.binary = decimal.toString(2);
                this.convert_number.octal = decimal.toString(8);
                this.convert_number.hexadecimal = value || 0;
         
            }
        },

        methods: {
            resetNumber(){
                this.convert_number.decimal = 0;
                this.convert_number.binary = 0;
                this.convert_number.octal = 0;
                this.convert_number.hexadecimal = 0;
            }
        },
    }
</script>