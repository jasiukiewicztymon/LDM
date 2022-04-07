<template>
    <div @click="checkname" id="main-box" class="absolute left-[50%] overflow-auto -translate-x-[50%] top-[16vw] md:top-[12vw] lg:top-[9vw] w-[90vw] h-[82.5vh] lg:h-[75vh]">
        <div id="mainboxset" @click.self="containerbox($event)" @mousedown.self="mousedown($event)" @mousemove.self="mousemove($event)" @mouseleave.self="this.drag.isDown = false" @mouseup="this.drag.isDown = false" :class="{active: this.drag.isDown}" class="w-[100000px] h-[100000px] p-[20px]">
            <div :style="{ top: table.t + 'px', left: table.l + 'px' }" @mousemove="boxmousemove($event, table)" @mouseleave="table.drag.isDown = false" @mouseup="table.drag.isDown = false" @click="box(table)" v-for="table in this.tables" :key="table.id" class="w-[485px] h-[550px] bg-[#41bf82] overflow-hidden overflow-y-auto absolute" :id="['table-'+table.id]">
                <div class="w-[100%] h-[100%]" @mousedown="boxmousedown($event, table)">
                    <div class="flex justify-center">
                        <input v-model="table.title" class="p-1 mt-10 w-[70%]">
                    </div>
                    <h2 class="pt-[30px] ml-[20px] text-[25px] text-white">Datas</h2>
                    <div v-for="data in table.data" :key="data.id" class="ml-[20px] pt-3 mb-[5px]" :id="['box-'+data.indexs+'-'+table.id]">
                        <span class="mr-[10px] text-white">PK</span><input type="checkbox" class="mr-[10px]" v-model="data.pk" @click="checkkeys(table, data, 0)">
                        <span class="mr-[10px] text-white">FK</span><input type="checkbox" class="mr-[10px]" v-model="data.fk" @click="checkkeys(table, data, 1)">
                        <span class="mr-[10px] text-white">UK</span><input type="checkbox" class="mr-[10px]" v-model="data.uk" @click="checkkeys(table, data, 2)">
                        <input v-model="data.name" class="p-1 w-[200px] content-input mr-[40px]">
                        <button class="deldatabtn" @click="delval(table, data, data.indexs)"><img src="../assets/trash.svg"></button>
                        <div class="link" @click="linktables(table, data, data.indexs)" :id="['link-'+table.id+'-'+data.indexs]"></div>
                    </div>
                    <div class="p-[20px] text-white" @click="addval(table)">Add data</div>
                </div>
            </div>
            <div class="linepf" v-for="link in this.link" :key="link.id" :id="['l-'+link.id]" :style="{ top: link.val.top, left: link.val.left, width: link.val.width, transform: 'rotate('+link.val.deg+'deg)' }"></div>
        </div>
    </div>
</template>

<script>
/* eslint-disable */
import { ref } from 'vue'

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
        delval(t, data, id) {
            console.log('⚠ : ' + t.id + ", " + data.indexs + "\n")
            if (t.data.length > 1) {
                this.link.forEach(e => {
                    console.log("💫:\n" + e.tpid + ": " + t.id + "\n" + e.vpid + ": " + data.indexs + "\n" + e.tfid + ": " + t.id + "\n" + e.vfid + ": " + data.indexs)
                    if (!((e.tpid == t.id && e.vpid == data.indexs) || (e.tfid == t.id && e.vfid == data.indexs))) {
                        this.nl.push(e)
                    }
                })
                this.link = this.nl
                this.nl = []

                t.data.splice(t.data.indexOf(data), 1)
            } 
        },
        addval(t) {
            // ✔
            t.data.push({
                indexs: ref(t.index),
                name: '',
                fk: false,
                pk: false,
                uk: false,
            })
            console.log('💢 : ' + t.index)
            t.index++;
        },
        containerbox(e) {
            // ✔
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
                           indexs: ref(0),
                           name: 'hello world',
                           fk: false, 
                           pk: false,
                           uk: false,
                       }
                   ]
               })
               console.log('💥 : ' + this.index)
               this.index++;
            }
        },
        box(table) {
            // ✔
            if (document.getElementById('trash-info').classList.contains('on')) {
                this.link.forEach(e => {
                    if (e.tfid != table.id && e.tpid != table.id)
                        this.nl.push(e)
                })
                this.link = this.nl
                this.nl = []
                this.tables.splice(this.tables.indexOf(table), 1)
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
        checkkeys(t, dataindex, type) {
            // ✔
            if (type === 0) {
                if (t.data[t.data.indexOf(dataindex)].pk == false) {
                    t.data[t.data.indexOf(dataindex)].fk = false;
                    t.data[t.data.indexOf(dataindex)].uk = false;
                }
                if (t.data[t.data.indexOf(dataindex)].pk == false) {
                    for (let i = 0; i < t.data.length; i++) {
                        if (i != t.data.indexOf(dataindex))
                            t.data[i].pk = false
                    }
                }
            }
            else if (type === 2) {
                if (t.data[t.data.indexOf(dataindex)].uk == false) {
                    t.data[t.data.indexOf(dataindex)].pk = false;
                    t.data[t.data.indexOf(dataindex)].fk = false;
                }

                // delete all the links with this value

                this.link.forEach(e => {
                    if ((e.tpid != t.id && e.vpid != t.data.indexOf(dataindex)) || (e.tfid != t.id && e.vfid != t.data.indexOf(dataindex))) {
                        this.nl.push(e)
                    }
                })

                this.link = this.nl
                this.nl = []
            }
            else {
                if (t.data[t.data.indexOf(dataindex)].fk == false) {
                    t.data[t.data.indexOf(dataindex)].pk = false;
                    t.data[t.data.indexOf(dataindex)].uk = false;
                }
            }
        },
        linktables(t, v, id) {
            var table = t.id, value = t.data.indexOf(v);
            if (document.getElementById('slash-lg-info').classList.contains('on')) {
                var exist = false;

                this.link.forEach(e => {
                    if ((e.tpid == table && e.vpid == value) || (e.tfid == table && e.vfid == value)) {
                        exist = true;
                    }
                })

                if (!exist && (this.tables[table].data[value].pk == true || this.tables[table].data[value].fk == true)) {
                    if (this.linkindex[0] == -1 && this.linkindex[1] == -1) {
                        this.linkindex = [table, id]
                    }
                    else {
                        if (table != this.linkindex[0]) {
                            var pkey = document.getElementById('link-'+table+'-'+id)
                            var fkey = document.getElementById('link-'+this.linkindex[0]+'-'+this.linkindex[1])

                            var mainbox = document.getElementById('mainboxset')

                            this.link.push({
                                pref: pkey,
                                fref: fkey,
                                tpid: ref(table),
                                tfid: ref(this.linkindex[0]),
                                vpid: ref(id),
                                vfid: ref(this.linkindex[1]),
                                id: ref(this.indexid),
                                mref: ref(mainbox),
                                val: {
                                    width: 0,
                                    left: 0,
                                    top: 0,
                                    deg: 0
                                }
                            })

                            this.indexid++
                            this.linkindex = [-1, -1]
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
                e.pref = document.getElementById('link-'+e.tpid+'-'+e.vpid)
                e.fref = document.getElementById('link-'+e.tfid+'-'+e.vfid)
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

                p = null, f = null, m = null;
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
