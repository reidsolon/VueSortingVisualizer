<template>
    <div class="container-fluid">
        <ActionBar
            @generateArray="generateArray()"
            @bubbleSort="bubble()"
            @arrayLength="generateNewArray"
        >
            <template slot="range-slider">
                <div class="form-group">
                    <input v-model="data.arraySize" @input="generateArray()" min="5" max="80" type="range" class="form-control-range">
                </div>
            </template>
        </ActionBar>
        <div class="row ">
            <div class="col-12">
                <div class="mx-auto array--container">
                    <template v-for="(bar,i) in data.arrayBar">
                        <Bar 
                            :key="i" 
                            :value="bar">{{bar}}
                        </Bar>
                    </template>
                </div>
                
            </div>
        </div>
    </div>
</template>
<script>

import ActionBar from './ActionBar'
import Bar from './Bar'

export default {
    components: {
        Bar,
        ActionBar,
    },
    data() {
        return {
            data: {
                arrayBar: [],
                arraySize: 40,
                sortedArray: []
            }
        }
    },
    methods: {
        bubble() { 
            clearInterval(interval)
            var valid        = false
            var firstIndex   = 0
            var secondIndex  = 1
            var totalTicks   = 0
            var temp_array   = [...this.data.arrayBar]

            const interval = setInterval( () => {
                var array        = [...this.data.arrayBar]
                
                temp_array.sort((a, b) => { return a - b })
                this.doAnimation(array[firstIndex], array[secondIndex])
                if(array[firstIndex] > array[secondIndex]) {
                    this.swapAnimmation(array[firstIndex], array[secondIndex])
                    var temp  = array[firstIndex]
                    array[firstIndex]   = array[secondIndex]
                    array[secondIndex]  = temp
                }
                firstIndex++
                secondIndex++
                
                if(firstIndex == this.data.arrayBar.length - totalTicks) {
                    firstIndex  = 0
                    secondIndex = 1
                    totalTicks++

                    for(let i = 0 ; i < array.length ; i++) {
                        if(array[i] != temp_array[i]) {
                            valid = false
                        } 
                    }

                    if(valid) {
                        console.log('wow')
                    }
                }

                if(totalTicks == this.data.arrayBar.length - 1) {
                    clearInterval(interval)
                }

                this.data.arrayBar = array
                
            }, 50)

            interval
        },
        generateNewArray(
            value
        ) {
            console.log(value)
        },
        generateArray(
            size = parseInt(this.data.arraySize), 
            length = 500
        ) {
            if(
                size,
                length
            ) {
                var array = []
                for(var i = 0; i < size ; ++i)
                {   
                    var random   = Math.floor(Math.random() * length) + 1
                    var newValue = Math.floor(Math.random() * length) + 1
                    if(array.includes(newValue)) {
                        newValue = random
                    }

                    array[i] = newValue
                }
 
                if(array.length === size) {
                    this.data.arrayBar = array
                }
            }
        },

        doAnimation(
            firstElement,
            secondElement
        ) {
            if(firstElement, secondElement) {
                document.querySelector('.BAR_'+firstElement).style.backgroundColor = '#6cdb7b'
                document.querySelector('.BAR_'+secondElement).style.backgroundColor = '#6cdb7b'

                setTimeout(() => {
                    this.setNormalColor(firstElement, secondElement)
                }, 50)
            }
        },

        swapAnimmation(firstElement,secondElement) {
            if(firstElement,secondElement) {
                document.querySelector('.BAR_'+firstElement).style.backgroundColor = 'red'
                document.querySelector('.BAR_'+secondElement).style.backgroundColor = 'red'
            }
        },

        setNormalColor(firstElement, secondElement) {
            if(firstElement,secondElement) {
                document.querySelector('.BAR_'+firstElement).style.backgroundColor = '#6399f1'
                document.querySelector('.BAR_'+secondElement).style.backgroundColor = '#6399f1'
            }
        }

    
    },
    mounted() {
        this.generateArray()
    }
}
</script>
<style scoped>
.array--container{text-align:center !important;}
</style>