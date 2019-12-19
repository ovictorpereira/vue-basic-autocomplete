<template>
    <div class="autocomplete">
        <input 
            class="autocomplete-input"
            :class="inputClass"
            ref="inputAutocomplete"
            :value="typeof(value) == 'string' ? value : value[trackby]"
            @focus="updateData()"
            @input="updateData()"
            @paste="updateData()"
            @keydown="dropSelection($event)"
            @blur="onBlur()"
            :placeholder="placeholder"
            :disabled="disabled"
        >
        <div class="autocomplete-list" v-if="filteredItems">
            <ul v-if="filteredItems.length > 0" :style="`max-height: ${listMaxHeight}px`">
                <li v-for="(item, index) in filteredItems" :key="index"
                    :class="highlight == index ? 'highlight-class' : ''"
                    @mousedown="sendValue(item)"
                    @mouseenter="highlight = index"
                    @mouseleave="highlight = -1"
                >
                    <span v-if="trackby != ''">{{item[trackby]}}</span>
                    <span v-if="trackby == ''">{{item}}</span>
                </li>
            </ul>
            <ul v-if="filteredItems.length === 0">
                <li class="text-muted">{{noneFind}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            value: {
                default: ''
            },
            options: {
                type: Array,
                required: true
            },
            trackby: {
                type: String,
                default: ""
            },
            minlength: {
                type: Number,
                default: 1
            },
            noneFind: {
                type: String,
                default: "No matching results"
            },
            'input-class': {
                type: String,
                default: ""
            },
            placeholder: {
                type: String,
                default: ""
            },
            disabled: {
                type: Boolean,
                default: false
            },
            'list-max-height': {
                type: String,
                default: "300"
            }
        },
        data () {
            return {
                highlight: -1,
                filteredItems: false
            }
        },
        methods: {
            updateData() {
                const inputAutocomplete = this.$refs.inputAutocomplete.value;
                this.$emit('input', inputAutocomplete)

                if (inputAutocomplete.length == 0 && this.minlength == 0) {
                    this.filteredItems = this.options
                    return
                }

                if (inputAutocomplete.length >= this.minlength) {
                    let result;
                    this.trackby != '' ?
                        result = this.options.filter(i => i[this.trackby] == inputAutocomplete) :
                        result = this.options.filter(i => i == inputAutocomplete)
                   
                    result.length == 0 ?
                        this.filterItems() :
                        this.sendValue(result[0])
                } 
                else {
                    this.filteredItems = false
                }
            },
            filterItems () {
                let result;
                let reg = new RegExp(this.$refs.inputAutocomplete.value.split('').join('\\w*').replace(/\W/, ""), 'i')

                this.trackby != '' ?
                    result = this.options.filter(i => { if (i[this.trackby].match(reg)) return i }) :
                    result = this.options.filter(i => { if (i.match(reg)) return i })

                this.filteredItems = result
            },
            onBlur () {
                let result;
                this.trackby != '' ?
                result = this.options.filter(i => i[this.trackby] ==  this.$refs.inputAutocomplete.value) :
                result = this.options.filter(i => i ==  this.$refs.inputAutocomplete.value)

                if (result.length === 0) {
                    this.$refs.inputAutocomplete.value = ''
                    this.filteredItems = false
                    this.$emit('input', '')
                }
            },
            sendValue (data) {
                this.highlight = -1
                this.filteredItems = false
                this.$emit('input', data)
            },
            dropSelection (e) {
                if (e.keyCode == 38) this.previous()
                if (e.keyCode == 40) this.next()
                if (e.keyCode == 13) this.enterClick()
            },
            enterClick() {
                if (this.filteredItems != false && this.filteredItems.length > 0) this.sendValue(this.filteredItems[this.highlight])
            },
            previous() {
                if (this.filteredItems != false && this.highlight > 0) --this.highlight
            },
            next () {
                let s = this.highlight,
                    l = parseInt(this.filteredItems.length)
                if (this.filteredItems != false && s < l) this.highlight++
            }
        }
    }
</script>

<style>
.autocomplete {
    position: relative;
}

.autocomplete-input {
    overflow: hidden;
    width: 100%;
}
.autocomplete-list {
    z-index: 9999;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    border: 1px solid #ced4da;
    border-top: none;
    background-color: white;
}

.autocomplete-list ul {
    overflow: auto;
    list-style-type: none;
    margin: 0;
    padding: 0;
}
.autocomplete-list ul li {
    padding: 6px;
    cursor: default;
    font-size: 0.92rem;
    display: list-item;
    text-align: left;
}

.highlight-class {
    background-color: #efefef;
    font-weight: bold;
}

.text-muted {
    color: #6c757d!important;
}

</style>