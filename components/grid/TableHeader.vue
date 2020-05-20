<template>
    <el-row class="table-header">
        <template v-if="type=='0'">
            <el-col :span="12" class="title-box">
                <span>{{title}}</span>
            </el-col>

            <el-col :span="12" class="operate-box">
                <slot></slot>
            </el-col>
        </template>
        <template v-if="type=='1'">
            <el-col :span="24" class="operate-box1">
                <slot></slot>
            </el-col>
        </template>
    </el-row>
</template>

<script>
    export default {
        name: "TableHeader",
        props:{
            'title':{
                type: String,
                default: ""
            },
            'type':{
                type: String,
                default:"0"
            }
        },
    }
</script>

<style scoped lang="less">
    .table-header{
        border: 1px solid #ecf0f4;
        background-color: #f3fbff;
        height: 50px;
        line-height: 50px;
        margin-top: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .title-box{
        display: inline-block;
        i{
            padding-left: 10px;
        }
        span{
            padding-left: 10px;
        }
    }
    .operate-box{
        display: inline-block;
        text-align: right;
        padding-right: 10px;
    }
    .operate-box1{
        padding-right: 5px;
        text-align: right;
    }
</style>
