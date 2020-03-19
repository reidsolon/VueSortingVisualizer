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
            <div class="array--container col-12">
                <template v-for="(bar,i) in data.arrayBar">
                    <Bar 
                        :key="i" 
                        :value="bar">{{bar}}
                    </Bar>
                </template>
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

            
            var firstIndex   = 0
            var secondIndex  = 1
            var totalTicks   = 0

            const interval   = setInterval( () => {
                var array        = [...this.data.arrayBar]
                this.doAnimation(array[firstIndex], array[secondIndex])
                
                if(array[firstIndex] > array[secondIndex]) {
                    
                    var temp  = array[firstIndex]
                    array[firstIndex]   = array[secondIndex]
                    array[secondIndex]  = temp
                    this.data.arrayBar = [...array]
                }
                

                firstIndex++
                secondIndex++
                
                if(firstIndex == this.data.arrayBar.length - totalTicks) {
                    this.data.sortedArray.unshift(array[firstIndex])
                    firstIndex  = 0
                    secondIndex = 1
                    totalTicks++
                }

                if(totalTicks == this.data.arrayBar.length - 1) {
                    clearInterval(interval)
                    console.log('done')
                }
                // this.data.arrayBar = [...array]
            }, 500)

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
                setTimeout(() => {
                    document.querySelector('.BAR_'+firstElement).style.backgroundColor = '#6cdb7b'
                    document.querySelector('.BAR_'+secondElement).style.backgroundColor = '#6cdb7b'
                }, 100)
                

                // setTimeout(()=> {
                //     this.setNormalColor(firstElement, secondElement)
                // }, 140)
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
.array-container {text-align:center !important;}
</style>