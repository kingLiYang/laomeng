<template>
    <div style="padding:20px;overflow-y: scroll;height:100%;">
        <div style="display: flex;justify-content: space-between;">
            <div class="bo">
<!--                // :class="{boActive:isCur===index}" 这个 是 相等的话 添加class 不相等就不添加  -->
<!--                index    是数组的下标    isCur  是 用来比较的一个东西  点击的时候 isCur=index  会把点击的下标赋值给isCur 然后就好了 还能，那么写呢
                    这不是看着他们的炒一波 哦真牛逼   还是 网友厉害   那click逗号这么写是啥意思   index赋值给isCur    后边的  方法    这是个什么操作
                    这个方法   到时候  请求接口   ojk 这么说就明白了   完美 就这个意思   ojk非常优秀大哥
                    大哥
                   你这回车  按习惯了    是的   习惯了
                   在这么写下去我们要写一篇文章了
                   根本不慌  有注释  没问题

    -->
                <span v-for="(item,index) in staData" :class="{boActive:isCur===index}" @click="isCur=index, changeSta(item.name)" >{{item.name}}</span>


            </div>
            <div class="bo1">
                <span>导入</span>
                <span @click="luruList">录入</span>
            </div>

        </div>
        <el-row >
            <el-col>
                <el-row :gutter="24">
                    <el-col :span="24" style="height: 80px; align-items: center;display: flex">
                            <el-dropdown :hide-on-click="false" style="margin-right: 10px;">
                                  <span class="el-dropdown-link">公司名称<i class="el-icon-arrow-down el-icon--right"></i>
                                  </span>
                                <el-dropdown-menu slot="dropdown">
                                    <el-dropdown-item>客户账号</el-dropdown-item>
                                    <el-dropdown-item>货物类型</el-dropdown-item>
                                    <el-dropdown-item>委托书编号</el-dropdown-item>
                                    <el-dropdown-item >运单号码</el-dropdown-item>
                                </el-dropdown-menu>
                           </el-dropdown>
                          <input type="text" >
                        <img src="../../assets/chaxun.png" alt="查询图标" style="margin-left: 10px;margin-top: 0px;width: 23px;
                        height: 23px;">
                        <p style="margin:0 10px;    flex: 1;justify-content: flex-end;display: flex;font-family: cursive" @click="development" >更多操作 &nbsp<i  style="margin: 10px 0 0 0; " :class="sanja ? 'sanjiao' : 'sanjiao2'" ></i></p>
                    </el-col>
                    <el-col :span="24" style=" align-items: center;display: flex;margin: 0;" >
                        <el-form :inline="true" style="margin: 10px 0 0 0; " :class="isMeng ? 'isA' : 'isb'"  >
                            <el-row>
                                <el-col>
                                    <el-form-item label="下单时间"   >
                                        <div class="block"  >
                                            <el-date-picker
                                                v-model="xdtime"

                                                type="datetimerange"
                                                value-format="yyyy-MM-dd HH:mm:ss"
                                                range-separator="至"
                                                start-placeholder="开始日期"
                                                end-placeholder="结束日期">
                                            </el-date-picker>
                                        </div>
                                    </el-form-item>
                                    <el-form-item label="取件时间">
                                        <div class="block" >
                                            <el-date-picker
                                                v-model="time"

                                                type="datetimerange"
                                                value-format="yyyy-MM-dd HH:mm:ss"
                                                range-separator="至"
                                                start-placeholder="开始日期"
                                                end-placeholder="结束日期">
                                            </el-date-picker>
                                        </div>
                                    </el-form-item>

                                    <img src="../../assets/chaxun.png" alt="查询图标" style="margin-left: 10px;margin-top: 8px;width: 23px; height: 23px;">
                                </el-col>
                                <el-col>

                                    <el-form-item label="始发城市">
                                        <el-input v-model="Startcity"  style="width: 115px"></el-input>
                                    </el-form-item>
                                    <el-form-item label="目的城市 " >
                                        <el-input v-model="Endcity"  style="width: 115px"></el-input>
                                    </el-form-item>
                                    <el-form-item label="取件网络">
                                        <el-input v-model="internet"></el-input>
                                    </el-form-item>
                                    <el-form-item label="下单类型">
                                        <el-select v-model="region"  style="width: 200px;">
                                            <el-option key="bbk" label="所有" value="所有"></el-option>
                                            <el-option key="xtc" label="APP" value="APP"></el-option>
                                            <el-option key="imoo" label="客服" value="客服"></el-option>
                                        </el-select>
                                    </el-form-item>
                                    <img src="../../assets/chongzhi.png" alt="查询图标" style="margin-left: 10px;margin-top: 8px;width: 23px; height: 23px;">
                                </el-col>
                            </el-row>
                        </el-form>


                    </el-col>
                    <el-col>
                        <el-table
                            :header-cell-style="{background:'#EFF3F8'}"
                            stripe

                            @cell-click="jumpDetails"
                            :data="tableData"
                            style="width: 100%">
                            <el-table-column type="expand">
                                <template slot-scope="props">
                                   <el-row :gutter="24">
                                       <el-col :span="13" >
                                           <h4 style="border-left: 4px solid #45A2DF">  &nbsp&nbsp订单信息：</h4>
                                              <el-row :gutter="24">
                                                  <el-col :span="12" >
                                                      <div class="bioage">
                                                          <span>始发地：河北-廊坊</span>
                                                           <span>录入人：孟健康</span>
                                                      </div>
                                                      <div class="bioage">
                                                          <span>目的地：山西-临汾</span>

                                                          <span>取件人：孟孟</span>
                                                      </div>
                                                      <div class="bioage">
                                                          <span>温度区间：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span> <span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span></span>


                                                      </div>
                                                      <div  class="bioage">
                                                          <span>包材选择：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span> <span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp件数：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span> <span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>货物尺寸：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span> <span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp重量：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span>&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp温度计: &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>&nbsp&nbsp&nbsp&nbsp冷藏车：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span> <span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>结算方式：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span>&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp保险: &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<span style="background: #eee;padding:5px 25px;border-radius: 5px;">155</span></span>

                                                      </div>




                                                  </el-col>
                                                  <el-col :span="11" :offset="1" >
                                                      <div class="bioage" style="color: #fff">
                                                           无
                                                      </div>
                                                      <div class="bioage">
                                                          <span>下单类型：客户下单</span>

                                                      </div>
                                                      <div class="bioage">
                                                          <span>通知方式：客户下单</span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>是否完成：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">是</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">2019/5/12</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>指令取消：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">天气原因</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">2019/5/12</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>指令完成：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">1110556</span><span style="background: #eee;padding:5px 25px;border-radius: 5px;">2019/5/12</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>下单时间：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">2018年12月5日</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>下单时间：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">2018年12月5日</span></span>

                                                      </div>
                                                      <div  class="bioage">
                                                          <span>&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp备注：<span style="background: #eee;padding:5px 25px;border-radius: 5px;">我是孟健康</span></span>

                                                      </div>

                                                  </el-col>
                                              </el-row>



                                       </el-col>
                                       <el-col :span="10" :offset="1" >
                                            <h4 style="border-left: 4px solid #45A2DF">  &nbsp&nbsp客户信息：</h4>
                                           <div class="bioage">
                                               <span>公司名称：上海科技有限公司</span>
                                           </div>
                                           <div class="bioage">
                                               <span>联系人：孟健康</span>
                                               <span>科室：外科</span>
                                           </div>
                                           <div class="bioage">
                                               <span>联系电话：15001015750</span>
                                               <span>城市、区域：北京</span>
                                           </div>
                                           <div class="bioage">
                                               <span>详细地址：上海科技有限公司</span>
                                           </div>
                                           <h4 style="border-left: 4px solid #45A2DF">  &nbsp&nbsp收件人信息：</h4>
                                           <div class="bioage">
                                               <span>公司名称：上海科技有限公司</span>
                                           </div>
                                           <div class="bioage">
                                               <span>联系人：孟健康</span>
                                               <span>科室：外科</span>
                                           </div>
                                           <div class="bioage">
                                               <span>联系电话：15001015750</span>
                                               <span>城市、区域：北京</span>
                                           </div>
                                           <div class="bioage">
                                               <span>详细地址：上海科技有限公司</span>
                                           </div>
                                       </el-col>
                                   </el-row>

                                </template>
                            </el-table-column>
<!--                            <el-table-column-->
<!--                                type="index"-->
<!--                                label="序号"-->
<!--                                width="45">-->
<!--                            </el-table-column>-->
                            <el-table-column
                                label="订单号"
                                width="100"
                                prop="id"
                                align="center"
                            >
                            </el-table-column>
                            <el-table-column
                                label="货物类型"
                                align="center"

                                prop="name">
                            </el-table-column>
                            <el-table-column
                                label="货物名称"
                                align="center"

                                prop="category">
                            </el-table-column>
                            <el-table-column
                                label="客户账号"
                                align="center"

                                prop="AccoutNumber">
                            </el-table-column>
                            <el-table-column
                                label="收件人"
                                align="center"
                                prop="shoujian">
                            </el-table-column>
                            <el-table-column
                                class-name="curstomNum"
                                label-class-name="aaa"
                                label="要求取件时间"
                                align="center"
                                prop="time"
                               >
                            </el-table-column>
                            <el-table-column
                                align="center"
                                label="时限"

                                prop="shixian">
                            </el-table-column>
                            <el-table-column
                                align="center"
                                label="是否到付"

                                prop="isfu">
                            </el-table-column>

                            <el-table-column
                                class-name="curstomNum"
                                label-class-name="aaa"
                                label="是否通知"
                                align="center">
                                <template slot-scope="scope" >
                                    <span class='work' v-if="scope.row.istz == '是'"> {{scope.row.istz}}</span>
                                    <span class='fire' v-if="scope.row.istz == '否'" ><img src="../../assets/laba.png" alt=""></span>
                                </template>
                            </el-table-column>
                            <el-table-column

                                label="订单状态"
                                align="center"
                                prop="order">
                            </el-table-column>
<!--                            <el-table-column-->
<!--                                label="录入人"-->
<!--                                align="center"-->
<!--                                prop="lururen">-->
<!--                            </el-table-column>-->
                            <el-table-column
                                label="下单方式"

                                align="center"
                                prop="xiadan">
                            </el-table-column>
                            <el-table-column

                                align="center"
                                label="取件网络"
                                prop="net">
                            </el-table-column>
<!--                            <el-table-column-->
<!--                                label="取件人"-->
<!--                                align="center"-->
<!--                                prop="qujianren">-->
<!--                            </el-table-column>-->
                            <el-table-column
                                align="center"
                                label="操作">
                                <template slot-scope="scope">
                                    <el-button  size="small"  style="color: #1ab394;border: 1px solid #1ab394" plain >再一单</el-button>
                                </template>
                            </el-table-column>
                        </el-table>
                    </el-col>

                </el-row>
            </el-col>
        </el-row>
        <div class="pagination">
            <el-pagination
                :page-sizes="[20,50, 100, 500, 2000]"
                :page-size="20"
                :current-page='cur_page'
                layout="total, sizes, prev, pager, next, jumper"
                :total="ccc"
            ></el-pagination>
        </div>
<!--        //点击取件时间出来的弹框-->
        <el-dialog
            title="修改取件时间"
            :visible.sync="allotDialogVisible1"
            width="20%">
            <div>
                <div class="block" >
                    <el-date-picker
                        v-model="value1"
                        type="datetime"

                        style="width:100%"
                        placeholder="选择日期时间">s
                    </el-date-picker>
                </div>
                <el-form ref="form" label-width="80px" style="margin:10px 0 0 0">
                    <el-form-item label="原因类型">
                        <el-select v-model="region" placeholder="请选择">
                            <el-option label="客户原因" value="客户原因"></el-option>
                            <el-option label="内部原因" value="内部原因"></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="内容描述">
                        <el-input type="textarea"  ></el-input>
                    </el-form-item>
                </el-form>
            </div>
            <span slot="footer" class="dialog-footer">
                 <el-button type="primary" size="mini" >save</el-button>
            </span>
        </el-dialog>
<!--        点击是否通知-->
        <el-dialog
            title="请录入通知方式"
            :visible.sync="tongzhiFangshi"
            width="20%">
            <div>

                <el-form ref="form"  style="margin:10px 0 0 0">

                    <el-form-item >
                        <el-input></el-input>
                    </el-form-item>
                </el-form>
            </div>
            <span slot="footer" class="dialog-footer">
                 <el-button type="primary" size="mini" >save</el-button>
            </span>
        </el-dialog>
    </div>

</template>

<script>
    export default {
        name: "orderManagement",
        data() {
            return {
                value1:'',
                cur_page: 1,//当前页
                limit: 20, //每页多少条
                ccc: 500, //总tiao数
                staData: [{name:"所有"},{name:"指令下达"},{name:"指令取消"},{name:"指令安排"},{name:"完成"}],
                isCur: 0,
                xdtime:'',
                sanja:false,
                time:'',
                region:'',Startcity:'',
                Endcity:'',
                internet:'',
                isMeng: false,
                tongzhiFangshi:false,
                tableData: [
                    {
                    id: '12987122',
                    name: '药品',
                    category: '试剂',
                    AccoutNumber: '1205665',
                    shoujian: '孟健康',
                    time: '2019/12/15',
                    shixian: '71H',
                    isfu:'是',
                    istz:'是',
                    order:'指令下达',
                    lururen: '孟孟',
                    xiadan:'app',
                    net:'杭州',
                    qujianren:'小孟'
                },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '否',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '老孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '是',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '否',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '是',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '否',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '是',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '否',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '是',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },
                    {
                        id: '565464545',
                        name: '冰排',
                        category: '试剂',
                        AccoutNumber: '454545',
                        shoujian: '孟健康',
                        time: '2019/12/15',
                        shixian: '71H',
                        isfu: '是',
                        istz: '是',
                        order: '指令下达',
                        lururen: '孟孟',
                        xiadan: 'app',
                        net: '杭州',
                        qujianren: '小孟'
                    },],
                allotDialogVisible1:false,

            }
        },
        methods:{
            //点击表格里边td的时候
            jumpDetails(row,column,cell,event){

                if(column.label == '要求取件时间'){


                    this.allotDialogVisible1=true
                }else if(column.label == '操作'){

                    this.$router.push({
                        path: "/OrderEntry",
                        query: { id: row.id }
                    });
                }else if(row.istz == "否"){
                   this.tongzhiFangshi =true
                }
            },

            luruList(){
                this.$router.push({
                path: "/OrderEntry",

            });

            },
            changeSta(val){
                // 点击谁  就给谁加class   zajia  不会了
                console.log(val)
            },
            development(){

                this.isMeng=!this.isMeng
                this.sanja = !this.sanja



            }
        }
    }

</script>
<style>
    .el-dialog__body {
    padding: 10px 20px 0;
    color: #606266;
    font-size: 14px;
}

    .el-input__inner{
        height:35px;
    }
    .el-dialog__title {
        line-height: 16px;
        font-size: 18px;
        color: #303133;
        font-weight: 800;
        font-family: cursive;
    }
    .el-form-item {
        margin-bottom: 15px;
    }

    .demo-table-expand {
        font-size: 0;
    }
    .demo-table-expand label {
        width: 90px;
        color: #99a9bf;
    }
    .demo-table-expand .el-form-item {
        margin-right: 0;
        margin-bottom: 0;
        width: 50%;
    }
    /*.el-table th, .el-table tr {*/
    /*    background-color: #eee;*/
    /*}*/
    .el-table--striped .el-table__body tr.el-table__row--striped td {
        background: #F9FAFD;
    }
    .el-table .cell{
        font-size: 10px;
    }

    .curstomNum:not(.aaa) .cell {
        color: #649EFE !important;

    }
    .curstomNum:not(.aaa) .cell:hover {
        cursor: pointer;
    }
</style>
<style scoped>
    .bioage{
        margin:20px 0
    }
    .bioage span{
        margin-right: 20px;
    }
    .bo{
        background: #fff;
        /*border: 1px solid #dcdfe6;*/
        /*-webkit-box-shadow: 0 2px 4px 0 rgba(0,0,0,.12), 0 0 6px 0 rgba(0,0,0,.04);*/
        /*box-shadow: 0 2px 4px 0 rgba(0,0,0,.12), 0 0 6px 0 rgba(0,0,0,.04);*/
        display: flex;
        align-items: center;

    }
    .isA{
        display: block;
    }
    .isb{
        display: none;
    }
    .sanjiao{
        width: 0;
        border-width: 7px;
        border-style: solid;
        border-color: #666 transparent transparent transparent;

        position: relative;


    }
    .sanjiao2{
        width: 0;
        border-width: 7px;
        border-style: solid;
        border-color:  transparent transparent #666 transparent ;

        position: relative;
        top:-10px;
    }
    input{
        -webkit-appearance: none;
        background-color: #fff;
        background-image: none;
        border-radius: 4px;
        border: 1px solid #dcdfe6;
        box-sizing: border-box;
        color: #606266;
        display: inline-block;
        font-size: inherit;
        height: 40px;
        line-height: 40px;
        outline: none;
        padding: 0 15px;
        transition: border-color .2s cubic-bezier(.645,.045,.355,1);

    }
    .bo1{
        flex:1;
        border-bottom: 1px solid #eee;
        background: #fff;
        align-items: center;
        justify-content: flex-end;
        display: flex;
    }
    .bo1 span{
        padding:15px;
        font-family: cursive;
    }
    .bo span{
        padding: 15px;
        border-bottom: 1px solid #eee;
        font-family: cursive;
    }
    .bo span:first-of-type{
        padding: 15px 30px;
        border-left: none;
    }
    .boActive{
        border-right:1px solid #45A2DF;
        border-left: 1px solid #45A2DF;
        border-bottom: none!important;
        background: #45A2DF!important;
        color: #fff;
    }
    .fire{
        /*width:15px;*/
        /*height:15px;*/
        /*background: green;*/
        /*border-radius: 50%;*/
        /*display: inline-block;*/
        /* background-image: url("../../assets/laba.png"); */
        /* width: 15px; */
        /* height: 15px; */
        /* background: green; */
        /* border-radius: 50%; */
        /* display: inline-block; */
        /* width:21px;
        height: 21px;
        display: block;
        background-repeat: no-repeat;
        position: relative;
        left: 46px; */

    ;
    }
</style>
