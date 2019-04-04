<template>
    <transition-group class="list-item" name='flip-list' tag='ul' mode='in-out'>
        <li class='flip-list-item' :key="item.serial_number" v-for="item in TableData"
            @click="getItem(item)">
            <background-box class="latest-img-background">
                <convenience-image slot="content_box" alignment="max-contain"
                                   :src-nor="item.person.photo.length>300?'data:image/jpeg;base64,'+item.person.photo:item.person.photo"
                                   :src-err="defaultImg"/>
            </background-box>
        </li>
    </transition-group>
</template>

<script>
    export default {
        name: 'ListAnimation',
        props: {
            singerData: {},
            TableLen: Number
        },
        data: function () {
            return {
                defaultImg:require('../assets/photo_default.png')
            }
        },
        computed: {
            TableData: function () {
                let _this = this;
                if (_this.singerData.length <= _this.TableLen) {
                    return _this.singerData;
                } else if (_this.singerData.length > _this.TableLen) {
                    _this.singerData.splice(_this.TableLen, 1);
                }
                return _this.singerData;
            }
        },
        methods: {
            getItem(item) {
                this.$emit('item', item);
            }
        },
        mounted() {
        }
    }
</script>

<style>
    .list-item {
        display: flex;
        flex-direction: column;
        align-content: space-around;
        width: 60%;
        height: 100%;
        overflow:hidden
    }
    .latest-img-background {
        width: 100%;
        height: 80%;
        vertical-align: middle;
        display: inherit;
        padding-top: 10px;
        padding-bottom: 10px;
    }
    .flip-list-leave-active {
        /*position: absolute;*/
    }

    .flip-list-enter-active {
        transition: all 1.2s;
    }

    .flip-list-move {
        transition: transform 1.2s;
    }

    .flip-list-item {
        width: 100%;
        max-height: 25%;
        min-height: 25%;
        flex-grow: 1;
        position: relative;
    }

    .flip-list-enter {
        transition: all 1.2s;
        opacity: 0;
        transform: translateY(-100%);
    }

    .flip-list-enter-to {
        transition: all 1.2s;
    }

    .flip-list-leave-to {
        transition: all 1.2s;
        opacity: 0;
        transform: translateY(100%);
    }

    @keyframes slide-out {
        from {
            transform: translateY(0);
        }
        to {
            transform: translateY(0);
            height: 0;
        }
    }
</style>
