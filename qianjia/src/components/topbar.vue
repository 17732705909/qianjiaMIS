<template>
    <!-- 导入卡片 -->
    <el-card class="box-card">
        <!-- 头部 -->
        <div slot="header" class="clearfix">
            <!-- 左侧部分 -->
            <span>
                <a href="#" class="firstnav">
                    <img src="" alt="">
                    <span>千家MIS</span>
                </a> 
                <span> | </span>
                <a href="#" class="secondnav">至哲篇</a>
            </span>
            <!-- 右侧部分 -->
            <div class="fr">
                <el-badge :value="99" class="item">
                    <a href="#"><i class="el-icon-bell"></i></a>
                </el-badge>
                <el-badge :value="99" class="item" type="warning">
                    <a href="#"><i class="el-icon-message"></i></a>
                </el-badge>
                <a href="#"><i class="el-icon-bell"></i></a>
                <a href="#"><i class="el-icon-minus"></i></a>
                <a href="#"><i class="el-icon-close"></i></a>
            </div>
        </div>
        <!-- 内容部分 -->
        <div class="con clearfix">
            <!-- 搜索条部分 -->
            <div class="search">
                <!-- 日期部分 -->
                <div class="block fl">
                    <span class="demonstration">日&nbsp;&nbsp;&nbsp;&nbsp;期</span>
                    <el-date-picker
                        size="small"
                        v-model="date"
                        type="daterange"
                        range-separator="-"
                        start-placeholder="开始日期"
                        end-placeholder="结束日期">
                    </el-date-picker>
                </div>
                <!-- 姓名部分 -->
                <div class="myname fl">
                    姓&nbsp;&nbsp;&nbsp;&nbsp;名&nbsp;&nbsp;&nbsp;&nbsp;<el-input size="small" v-model="myname" placeholder="请输入内容"></el-input>
                </div>
                <!-- 内容部分 -->
                <div class="mycon fl">
                    内&nbsp;&nbsp;&nbsp;&nbsp;容&nbsp;&nbsp;&nbsp;&nbsp;<el-input size="small" v-model="mycon" placeholder="请输入内容"></el-input>
                </div>
                <!-- 按钮部分 -->
                <el-button  size="small">查询</el-button>
                <el-button size="small">清空</el-button>
                <el-button  size="small" class="fr">新增</el-button>
            </div>
            <!-- 信息部分 -->
            <el-card shadow="hover" class="info">
                <!-- 信息头部 -->
                <div class="top">
                    共 <span>2019</span> 条&nbsp;&nbsp;&nbsp;&nbsp;
                    已选 : <span>1234</span>&nbsp;&nbsp;&nbsp;&nbsp;
                    <span>|</span>&nbsp;&nbsp;&nbsp;&nbsp;
                    <!-- 按钮 -->
                    <el-button size="small" type="danger" plain>批量删除</el-button>
                </div>
                <!-- 表格部分 -->
                <el-table
                    class="mytable"
                    border
                    size="mini"
                    ref="multipleTable"
                    :data="tableData"
                    tooltip-effect="dark"
                    style="width: 100%"
                    highlight-current-row
                    @selection-change="handleSelectionChange"
                    @current-change="handleCurrentChange">
                    <!-- 多选框 -->
                    <el-table-column type="selection" width="55"></el-table-column>
                    <!-- 序号 -->
                    <el-table-column type="index" label="序号" width="100"></el-table-column>
                    <!-- 时间 -->
                    <el-table-column label="时间" >
                        <template slot-scope="scope">{{ scope.row.date }}</template>
                    </el-table-column>
                    <!-- 姓名 -->
                    <el-table-column prop="name" label="姓名">
                    </el-table-column>
                    <!-- 内容 -->
                    <el-table-column prop="content" label="内容" show-overflow-tooltip width="600"></el-table-column>
                    <!-- 操作 -->
                    <el-table-column fixed="right" label="操作">
                        <template slot-scope="scope">
                            <el-button @click="handleClick(scope.row)" type="text" size="small">修改</el-button>
                            <span> | </span>
                            <el-button type="text" size="small">删除</el-button>
                        </template>
                    </el-table-column>
                </el-table>
                <!-- 分页部分 -->
                <el-pagination
                    class="pages fr"
                    @size-change="sizeChange"
                    @current-change="currentChange"
                    :current-page="pagenum"
                    :page-sizes="[5, 10]"
                    :page-size="pagesize"
                    layout="total, sizes, prev, pager, next, jumper"
                    :total="total">
                </el-pagination>
            </el-card>
        </div>
    </el-card>
</template>

<script>
    export default {
        data() {
            return {
                date: '',
                myname: '',
                mycon:'',
                count: 2019,
                tableData: [
                    {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }, {
                        date: '示例文字',
                        name: '示例文字',
                        content: '示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字示例文字'
                    }],
                multipleSelection: [],
                currentRow: null,
                pagenum: 1,
                // 页容量
                pagesize: 5,
                // 总条数
                total: 0,
            }
        },
         methods: {
            setCurrent(row) {
                this.$refs.singleTable.setCurrentRow(row);
            },
            handleCurrentChange(val) {
                this.currentRow = val;
            },
            toggleSelection(rows) {
                if (rows) {
                    rows.forEach(row => {
                        this.$refs.multipleTable.toggleRowSelection(row);
                    });
                } else {
                    this.$refs.multipleTable.clearSelection();
                }
            },
            handleSelectionChange(val) {
                this.multipleSelection = val;
            },
            // 每页的条数 pageSize 改变时会触发
            sizeChange(size) {
                this.pagesize = size
                this.getAllList() 
            },
            // 当前页 currentPage 改变时会触发
            currentChange(num) {
                this.pagenum = num
                this.getAllList() 
            },
        }
    }
</script>

<style scoped>
.box-card {
    padding-top:10px;
    padding-left: 30px;
}
.firstnav span {
    font-size: 18px;
    font-weight: 700;
}
.secondnav {
    font-size: 14px;
}
.fr{
    float: right;
}
.fl {
    float: left;
}
.fr .el-badge {
    margin-right: 20px;
}
.fr a:nth-child(3) {
    margin-right: 30px;
}
.fr a:nth-child(4) {
    margin-right: 10px;
}
.clearfix:before, .clearfix:after {
    display: table;
    content: "";
}
.clearfix:after {
    clear: both;
}
.clearfix {
    *zoom : 1;
}
.demonstration, .block, .myname, .mycon {
    margin-right: 20px;
}
.el-date-editor{
    width: 260px;
}
.el-input {
    width: 200px;
}
.search {
    margin-bottom: 30px;
}
.el-button--danger.is-plain {
    background-color: #fff;
    color:#f56c6c;
}
.search button:nth-child(4){
    background-color: #20c09b;
    color: #fff;
}
.top {
    margin-bottom: 20px;
}
.info {
    background-color: #f7f7f7;
}
.mytable {
    margin-bottom: 20px;
}
.cell .el-button--text:first-child {
    color: orange;
}
.cell .el-button--text:last-child {
    color: #da4c36;
}
.pages {
    margin-bottom: 20px;
}
</style>