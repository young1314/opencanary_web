<template>
    <div class="table">
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-tickets"></i> 过滤列表</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="container">
            <!-- <div class="handle-box">
                <el-button type="primary" icon="delete" class="handle-del mr10" @click="delAll">批量删除</el-button>
                <el-select v-model="select_cate" placeholder="筛选省份" class="handle-select mr10">
                    <el-option key="1" label="广东省" value="广东省"></el-option>
                    <el-option key="2" label="湖南省" value="湖南省"></el-option>
                </el-select>
                <el-input v-model="select_word" placeholder="筛选关键词" class="handle-input mr10"></el-input>
                <el-button type="primary" icon="search" @click="search">搜索</el-button>
            </div> -->
            <!-- <el-table :data="data" border style="width: 100%" ref="multipleTable" @selection-change="handleSelectionChange">
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column prop="local_time" label="攻击时间">
                </el-table-column>
                <el-table-column prop="src_host" label="攻击来源">
                </el-table-column>
                <el-table-column prop="dst_host" label="目标主机">
                </el-table-column>
                <el-table-column prop="dst_port" label="目的端口">
                </el-table-column>
                <el-table-column prop="logtype" label="日志类型">
                </el-table-column>
                <el-table-column label="操作" width="180">
                    <template slot-scope="scope">
                        <el-button size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
                        <el-button size="small" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
                    </template>
                </el-table-column>
            </el-table> -->

  <el-table
    :data="data"
    style="width: 100%"
    :default-sort = "{prop: 'local_time', order: 'descending'}"
    >
    <el-table-column type="expand">
      <template slot-scope="props">
        <el-form label-position="left" inline class="demo-table-expand">
          <el-form-item v-if="props.row.hostname" label="HOSTNAME: ">
            <span>{{ props.row.hostname }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.username" label="USERNAME: ">
            <span>{{ props.row.username }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.password" label="PASSWORD: ">
            <span>{{ props.row.password }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.path" label="PATH: ">
            <span>{{ props.row.path }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.useragent" label="USERAGENT: ">
            <span>{{ props.row.useragent }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.session" label="SESSION: ">
            <span>{{ props.row.session }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.localversion" label="LOCALVERSION: ">
            <span>{{ props.row.localversion }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.remoteversion" label="REMOTEVERSION: ">
            <span>{{ props.row.remoteversion }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.inin" label="IN: ">
            <span>{{ props.row.inin }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.mac" label="MAC: ">
            <span>{{ props.row.mac }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.proto" label="PROTO: ">
            <span>{{ props.row.proto }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.ttl" label="TTL: ">
            <span>{{ props.row.ttl }}</span>
          </el-form-item>
          <el-form-item v-if="props.row.window" label="WINDOW: ">
            <span>{{ props.row.window }}</span>
          </el-form-item>
        </el-form>
      </template>
    </el-table-column>
    <el-table-column
      label="攻击时间"
      prop="local_time"
      sortable
      >
    </el-table-column>
    <el-table-column
      label="攻击来源"
      prop="src_host"
      sortable
      >
    </el-table-column>
    <el-table-column
      label="来源端口"
      prop="src_port"
      sortable
      >
    </el-table-column>
    <el-table-column
      label="攻击类型"
      prop="logtype"
      sortable
      >
    </el-table-column>
    <el-table-column
      label="探针节点"
      prop="node_id"
      sortable
      >
    </el-table-column>
    <el-table-column
      label="目标主机"
      prop="dst_host"
      sortable
      >
    </el-table-column>
    <el-table-column
      label="目标端口"
      prop="dst_port"
      sortable
      >
    </el-table-column>

  </el-table>

            <div class="pagination">
                <el-pagination @current-change="handleCurrentChange" layout="prev, pager, next" :total="1000">
                </el-pagination>
            </div>
        </div>

        <!-- 
        <el-dialog title="编辑" :visible.sync="editVisible" width="30%">
            <el-form ref="form" :model="form" label-width="50px">
                <el-form-item label="日期">
                    <el-date-picker type="date" placeholder="选择日期" v-model="form.date" value-format="yyyy-MM-dd" style="width: 100%;"></el-date-picker>
                </el-form-item>
                <el-form-item label="姓名">
                    <el-input v-model="form.name"></el-input>
                </el-form-item>
                <el-form-item label="地址">
                    <el-input v-model="form.address"></el-input>
                </el-form-item>

            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button @click="editVisible = false">取 消</el-button>
                <el-button type="primary" @click="saveEdit">确 定</el-button>
            </span>
        </el-dialog>
        编辑弹出框 -->

        <!-- 删除提示框 -->
        <el-dialog title="提示" :visible.sync="delVisible" width="300px" center>
            <div class="del-dialog-cnt">删除不可恢复，是否确定删除？</div>
            <span slot="footer" class="dialog-footer">
                <el-button @click="delVisible = false">取 消</el-button>
                <el-button type="primary" @click="deleteRow">确 定</el-button>
            </span>
        </el-dialog>
    </div>
</template>

<script>
    export default {
        name: 'basetable',
        data() {
            return {
                url: '/log/list/',
                tableData: [],
                cur_page: 1,
                multipleSelection: [],
                select_cate: '',
                select_word: '',
                del_list: [],
                is_search: false,
                editVisible: false,
                delVisible: false,
                form: {
                    name: '',
                    date: '',
                    address: ''
                },
                idx: -1
            }
        },
        created() {
            this.getData();
        },
        computed: {
            data() {
                return this.tableData.filter((d) => {
                    let is_del = false;
                    for (let i = 0; i < this.del_list.length; i++) {
                        if (d.name === this.del_list[i].name) {
                            is_del = true;
                            break;
                        }
                    }
                    if (!is_del) {
                        if (d.local_time.indexOf(this.select_cate) > -1 &&
                            (d.dst_host.indexOf(this.select_word) > -1 ||
                                d.dst_port.indexOf(this.select_word) > -1)
                        ) {
                            return d;
                        }
                    }
                })
            }
        },
        methods: {
            // 分页导航
            handleCurrentChange(val) {
                this.cur_page = val;
                this.getData();
            },
            // 获取 easy-mock 的模拟数据
            getData() {
                // 开发环境使用 easy-mock 数据，正式环境使用 json 文件
                if (process.env.NODE_ENV === 'development') {
                    this.url = process.env.API_HOST+'/log/list/';
                };
                this.$axios.post(this.url, {
                    page: this.cur_page,
                    white: 1
                }).then((res) => {
                    this.tableData = res.data.list;
                })
            },
            search() {
                this.is_search = true;
            },
            // formatter(row, column) {
            //     return row.local_time;
            // },
            filterTag(value, row) {
                return row.tag === value;
            },
            handleEdit(index, row) {
                this.idx = index;
                const item = this.tableData[index];
                this.form = {
                    name: item.name,
                    date: item.date,
                    address: item.address
                }
                this.editVisible = true;
            },
            handleDelete(index, row) {
                this.idx = index;
                this.delVisible = true;
            },
            delAll() {
                const length = this.multipleSelection.length;
                let str = '';
                this.del_list = this.del_list.concat(this.multipleSelection);
                for (let i = 0; i < length; i++) {
                    str += this.multipleSelection[i].name + ' ';
                }
                this.$message.error('删除了' + str);
                this.multipleSelection = [];
            },
            handleSelectionChange(val) {
                this.multipleSelection = val;
            },
            // 保存编辑
            saveEdit() {
                this.$set(this.tableData, this.idx, this.form);
                this.editVisible = false;
                this.$message.success(`修改第 ${this.idx+1} 行成功`);
            },
            // 确定删除
            deleteRow(){
                this.tableData.splice(this.idx, 1);
                this.$message.success('删除成功');
                this.delVisible = false;
            }
        }
    }

</script>

<style scoped>
    .handle-box {
        margin-bottom: 20px;
    }

    .handle-select {
        width: 120px;
    }

    .handle-input {
        width: 300px;
        display: inline-block;
    }
    .del-dialog-cnt{
        font-size: 16px;
        text-align: center
    }
</style>
