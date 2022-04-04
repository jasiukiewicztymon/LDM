<template>
    <div @click="checkname" id="main-box" class="absolute left-[50%] overflow-auto -translate-x-[50%] top-[16vw] md:top-[12vw] lg:top-[9vw] w-[90vw] h-[82.5vh] lg:h-[75vh]">
        <div id="mainboxset" @click.self="containerbox($event)" @mousedown.self="mousedown($event)" @mousemove.self="mousemove($event)" @mouseleave.self="this.drag.isDown = false" @mouseup="this.drag.isDown = false" :class="{active: this.drag.isDown}" class="w-[100000px] h-[100000px] p-[20px]">
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
            <div class="linepf" v-for="link in this.link" :key="link.id" :id="['l-'+link.id]" :style="{ top: link.val.top, left: link.val.left, width: link.val.width, transform: 'rotate('+link.val.deg+'deg)' }"></div>
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
           index: 0,
           link: false,
           linkindex: [-1, -1],
           tables: [],
           indexid: 0,
           link: [],
           nl: []
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
            console.log(this.tables[id].index)
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
                var id = this.tables.indexOf(table);
                this.link.forEach(e => {
                    if (e.tfid != table.id && e.tpid != table.id)
                        this.nl.push(e)
                })
                this.link = this.nl
                this.nl = []
                this.tables.splice(id, 1)
            }
        },
        checkname() {
            if (document.getElementById('pencil-info').classList.contains('on')) {
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

                this.link.forEach(e => {
                    if ((e.tpid == table && e.vpid == value) || (e.tfid == table && e.vfid == value)) {
                        console.log(e)
                        console.log(table)
                        console.log(value)
                        exist = true;
                    }
                })

                if (!exist) {
                    if (this.linkindex[0] == -1 && this.linkindex[1] == -1) {
                        this.linkindex = [table, value]
                    }
                    else {
                        if (table != this.linkindex[0]) {
                            var pkey = document.getElementById('link-'+table+'-'+value)
                            var fkey = document.getElementById('link-'+this.linkindex[0]+'-'+this.linkindex[1])

                            var mainbox = document.getElementById('mainboxset')

                            this.link.push({
                                pref: pkey,
                                fref: fkey,
                                tpid: table,
                                tfid: this.linkindex[0],
                                vpid: value,
                                vfid: this.linkindex[1],
                                id: this.indexid,
                                mref: mainbox,
                                val: {
                                    width: 0,
                                    left: 0,
                                    top: 0,
                                    deg: 0
                                }
                            })

                            this.indexid++
                            this.linkindex = [-1, -1]

                            console.log(this.link)
                        }
                        else {
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
        setInterval(() => {
            this.link.forEach(e => {
                var l = document.getElementById('l-'+e.id)

                var p = e.pref.getBoundingClientRect(), f = e.fref.getBoundingClientRect(), m = e.mref.getBoundingClientRect()

                var ax = p.left - m.left, ay = p.top - m.top, bx = f.left - m.left, by = f.top - m.top;

                ay += 5, by += 5

                if (ax > bx) {
                    ax -= 430
                }
                else if (ax < bx) {
                    bx -= 430
                }

                var length = Math.hypot(by-ay, bx-ax), deg = Math.atan2(by-ay, bx-ax) * 180 / Math.PI;

                e.val = {
                    width: length + "px",
                    left: ax + "px",
                    top: ay + "px",
                    deg: deg
                }
            });
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
        .linepf
            position: absolute
            background: #000
            opacity: 1,
            height: 2px
            transform-origin: left 50%
            z-index: -1
</style>
