<template>
    <div @click="checkname" id="main-box" class="absolute left-[50%] overflow-auto -translate-x-[50%] top-[16vw] md:top-[12vw] lg:top-[9vw] w-[90vw] h-[82.5vh] lg:h-[75vh]">
        <div @click.self="containerbox($event)" @mousedown.self="mousedown($event)" @mousemove.self="mousemove($event)" @mouseleave.self="this.drag.isDown = false" @mouseup="this.drag.isDown = false" :class="{active: this.drag.isDown}" class="w-[100000px] h-[100000px] p-[20px]">
            <div :style="{ top: table.t + 'px', left: table.l + 'px' }" @mousemove="boxmousemove($event, table)" @mouseleave="table.drag.isDown = false" @mouseup="table.drag.isDown = false" @click="box(table)" v-for="table in this.tables" :key="table.id" class="w-[485px] h-[550px] bg-[#41bf82] overflow-hidden overflow-y-auto absolute" :id="['table-'+table.id]">
                <div class="w-[100%] h-[100%]" @mousedown="boxmousedown($event, table)">
                    <div class="flex justify-center">
                        <input v-model="table.title" class="p-1 mt-10 w-[70%]">
                    </div>
                    <h2 class="pt-[30px] ml-[20px] text-[25px] text-white">Datas</h2>
                    <div v-for="data in table.data" :key="data.id" class="ml-[20px] pt-3 mb-[5px]" :id="['box-'+data.index+'-'+table.id]">
                        <span class="mr-[10px] text-white">PK</span><input type="checkbox" class="mr-[10px]" v-model="data.pk" @click="checkkeys(table.id, data.index, 0)">
                        <span class="mr-[10px] text-white">FK</span><input type="checkbox" class="mr-[10px]" v-model="data.fk" @click="checkkeys(table.id, data.index, 1)">
                        <span class="mr-[10px] text-white">UK</span><input type="checkbox" class="mr-[10px]" v-model="data.uk" @click="checkkeys(table.id, data.index, 2)">
                        <input v-model="data.name" class="p-1 w-[200px] content-input mr-[40px]">
                        <button class="deldatabtn" @click="this.tables[table.id].data.length > 1 ? this.tables[table.id].data.splice(this.tables[table.id].data.indexOf(data), 1) : this.tables[table.id].data.splice(this.tables[table.id].data.indexOf(data), 0)"><img src="../assets/trash.svg"></button>
                        <div class="link" @click.self="linktables(table.id, data.index)" :id="['link-'+table.id+'-'+data.index]"></div>
                    </div>
                    <div class="m-[20px] text-white" @click="addval(table.id)">Add data</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
/* eslint-disable */
const axios = require('axios')

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
           index: 0,
           link: false,
           linkindex: [-1, -1],
           tables: [],
           link: [],
        }
    },
    methods: {
        addval(id) {
            this.tables[id].data.push({
                index: this.tables[id].index,
                name: '',
                fk: false,
                pk: false,
                uk: false,
            })
            this.tables[id].index++;
        },
        containerbox(e) {
            if (document.getElementById('plus-info').classList.contains('on')) {
                this.tables.push({
                   id: this.index,
                   index: 1,
                   title: "Title",
                   t: e.offsetY,
                   l: e.offsetX,
                   drag: {
                        isDown: false,
                        startX: 0,
                        startY: 0,
                        scrollLeft: 0,
                        scrollTop: 0,
                    },
                   data: [
                       {
                           index: 0,
                           name: 'hello world',
                           fk: false, 
                           pk: false,
                           uk: false,
                       }
                   ]
               })

               this.index++;
            }
        },
        box(table) {
            if (document.getElementById('trash-info').classList.contains('on')) {
                this.tables.splice(this.tables.indexOf(table), 1)
            }
        },
        checkname() {
            if (document.getElementById('pencil-info').classList.contains('on')) {
                console.log('3')
            }
            else if (document.getElementById('arrow-bar-up-info').classList.contains('on')) {

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
                let wx = (x - this.drag.startX);
                let wy = (y - this.drag.startY);
                element.scrollLeft = this.drag.scrollLeft - wx;
                element.scrollTop = this.drag.scrollTop - wy;
            }
        },
        boxmousedown(e, table) {
            table.drag.isDown = true

            table.drag.startX = e.clientX;
            table.drag.startY = e.clientY;
        },
        boxmousemove(e, table) {
            if (table.drag.isDown) {
                e.preventDefault();
                let x = table.drag.startX - e.clientX
                let y = table.drag.startY - e.clientY

                table.t -= y;
                table.l -= x;

                table.drag.startX = e.clientX
                table.drag.startY = e.clientY
            }
        },
        checkkeys(tableid, dataindex, type) {
            if (type === 0) {
                if (this.tables[tableid].data[dataindex].pk == false) {
                    this.tables[tableid].data[dataindex].fk = false;
                    this.tables[tableid].data[dataindex].uk = false;
                }

                if (this.tables[tableid].data[dataindex].pk == false) {
                    for (let i = 0; i < this.tables[tableid].data.length; i++) {
                        if (i != dataindex)
                            this.tables[tableid].data[i].pk = false
                    }
                }
            }
            else if (type === 2) {
                if (this.tables[tableid].data[dataindex].uk == false) {
                    this.tables[tableid].data[dataindex].pk = false;
                    this.tables[tableid].data[dataindex].fk = false;
                }
            }
            else {
                if (this.tables[tableid].data[dataindex].fk == false) {
                    this.tables[tableid].data[dataindex].pk = false;
                    this.tables[tableid].data[dataindex].uk = false;
                }
            }
        },
        linktables(table, value) {
            if (document.getElementById('slash-lg-info').classList.contains('on')) {
                var exist = false;

                for (var i = 0; i < this.link.length; i++) {
                    if ((this.link[i][0][0] == table & this.link[i][0][1] == value) || (this.link[i][1][0] == table & this.link[i][1][1] == value)) {
                        exist = true;
                        break;
                    }
                }

                if (!exist) {
                    if (this.linkindex[0] == -1 && this.linkindex[1] == -1) {
                        this.linkindex = [table, value]
                    }
                    else {
                        if (table != this.linkindex[0]) {
                            this.link.push([[this.linkindex[0], this.linkindex[1]], [table, value]]);

                            // draw the line
                            var pkey = document.getElementById('link-'+table+'-'+value)
                            var fkey = document.getElementById('link-'+this.linkindex[0]+'-'+this.linkindex[1])

                            this.linkindex = [-1, -1]
                        }
                    }
                }
            }
        },
    },
    created() {
        window.addEventListener('load', this.replace);
        setInterval(() => {
            if (!document.getElementById('slash-lg-info').classList.contains('on')) {
                this.linkindex[0] = -1
                this.linkindex[1] = -1
            }
        })
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
        .deldatabtn
            width: 30px
            height: 30px
            top: 2px
            left: -12px
            position: relative
            img
                filter: invert(100%)
        .link
            background: transparent
            width: 15px
            height: 15px
            border: 3px solid white
            border-radius: 50%
            position: relative
            top: -24px
            left: 425px
</style>
