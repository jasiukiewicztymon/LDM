<template>
    <div @click="checkname" id="main-box" class="absolute left-[50%] overflow-auto -translate-x-[50%] top-[16vw] md:top-[12vw] lg:top-[9vw] w-[90vw] h-[82.5vh] lg:h-[75vh]">
        <div @mousedown="mousedown($event)" @mousemove="mousemove($event)" @mouseleave="this.drag.isDown = false" @mouseup="this.drag.isDown = false" :class="{active: this.drag.isDown}" class="w-[100000px] h-[100000px] p-[20px]">
            <div v-for="table in this.tables" :key="table.id" class="w-[450px] h-[550px] bg-green-400 overflow-hidden overflow-y-auto" :class="[table.top, table.left]" :id="['table-'+table.id]">
                <div class="flex justify-center">
                    <input v-model="table.title" class="p-1 mt-10 w-[70%]">
                </div>
                <h2 class="pt-[10px] ml-[20px] text-[25px]">Datas</h2>
                <div v-for="data in table.data" :key="data.id" class="ml-[20px] pt-3 mb-[5px]" :id="['box-'+data.index+'-'+table.id]">
                    <span class="mr-[10px]">PK</span><input type="checkbox" class="mr-[10px]" v-model="data.pk" @click="checkkeys(table.id, data.index, 0)">
                    <span class="mr-[10px]">FK</span><input type="checkbox" class="mr-[10px]" v-model="data.fk" @click="checkkeys(table.id, data.index, 1)">
                    <input v-model="data.name" class="p-1">
                </div>
                <button class="m-[20px] ">Add data</button>
            </div>
        </div>
    </div>
</template>

<script>
/* eslint-disable */

export default {
    components: {
    },
    data() {
        return {
           drag: {
               isDown: false,
               startX: 0,
               startY: 0,
               scrollLeft: 0,
               scrollTop: 0,
           },
           tables: [
               {
                   id: 0,
                   title: "test",
                   top: "mt-[30px]",
                   left: "ml-[100px]",
                   pk: false,
                   data: [
                       {
                           index: 0,
                           name: 'string',
                           fk: false, 
                           pk: false,
                       },
                       {
                           index: 1,
                           name: '',
                           fk: false, 
                           pk: false,
                       },
                       {
                           index: 2,
                           name: '',
                           fk: false, 
                           pk: false,
                       },
                       {
                           index: 3,
                           name: '',
                           fk: false, 
                           pk: false,
                       },
                       {
                           index: 4,
                           name: '',
                           fk: false, 
                           pk: false,
                       },
                       {
                           index: 5,
                           name: '',
                           fk: false, 
                           pk: false,
                       }
                   ]
               }
           ]
        }
    },
    methods: {
        checkname() {
            if (document.getElementById('plus-info').classList.contains('on')) {
                document.getElementById('main-box').onmousedown = function(e) {
                    console.log(e.offsetX)
                    console.log(e.offsetY)
                }
            }
            else if (document.getElementById('trash-info').classList.contains('on')) {
                console.log('2')
            }
            else if (document.getElementById('pencil-info').classList.contains('on')) {
                console.log('3')
            }
            else if (document.getElementById('slash-lg-info').classList.contains('on')) {
                console.log('4')
            }
        },
        replace() {
            document.getElementById('main-box').scrollTop = 50000;
            document.getElementById('main-box').scrollLeft = 50000;
        },
        mousedown(e) {
            let element = document.getElementById('main-box');

            this.drag.isDown = true;
            this.drag.startX = e.pageX - element.offsetLeft;
            this.drag.startY = e.pageY - element.offsetTop;
            this.drag.scrollLeft = element.scrollLeft;
            this.drag.scrollTop = element.scrollTop;
        },
        mousemove(e) {
            let element = document.getElementById('main-box');
            if (this.drag.isDown) {
                e.preventDefault();
                let x = e.pageX - element.offsetLeft;
                let y = e.pageY - element.offsetTop;
                let wx = (x - this.drag.startX) * 2;
                let wy = (y - this.drag.startY) * 3;
                element.scrollLeft = this.drag.scrollLeft - wx;
                element.scrollTop = this.drag.scrollTop - wy;
            }
        },
        checkkeys(tableid, dataindex, type) {
            if (type === 0) {
                if (this.tables[tableid].data[dataindex].pk == false)
                    this.tables[tableid].data[dataindex].fk = false

                if (this.tables[tableid].data[dataindex].pk == false) {
                    for (let i = 0; i < this.tables[tableid].data.length; i++) {
                        if (i != dataindex)
                            this.tables[tableid].data[i].pk = false
                    }
                }
            }
            else {
                if (this.tables[tableid].data[dataindex].fk == false)
                    this.tables[tableid].data[dataindex].pk = false
            }
        }
    },
    created() {
        window.addEventListener('load', this.replace);
    }
}
</script>

<style lang="sass" scoped>
    @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@500&display=swap')

    $boxbg: #262626
    $text: #fff
    $fontglobal: 'Open Sans', sans-serif
    * 
        font-family: $fontglobal
        #main-box
            border: 0.25vw solid #000
            border-radius: 1vw
</style>
