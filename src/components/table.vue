<template>
  <div class="clearfix content">
		<div class="cont_fl">
			<el-row>
				<el-col>
				    <el-menu
				      default-active="1"
				      class="el-menu-vertical-demo"
				      background-color="#545c64"
				      text-color="#fff"
				      active-text-color="#ffd04b">
					  <el-menu-item index="1">
					    <i class="el-icon-location"></i>
					    <span slot="title">导航一</span>
					  </el-menu-item>
				      <el-menu-item index="2">
				        <i class="el-icon-menu"></i>
				        <span slot="title">导航二</span>
				      </el-menu-item>
				      <el-menu-item index="3">
				        <i class="el-icon-document"></i>
				        <span slot="title">导航三</span>
				      </el-menu-item>
				      <el-menu-item index="4">
				        <i class="el-icon-setting"></i>
				        <span slot="title">导航四</span>
				      </el-menu-item>
				    </el-menu>
				  </el-col>
			</el-row>
		</div>
    <div class="cont_fr">
		<div class="box">
		  <el-button type="primary" size="mini">批量授权</el-button>
		  <el-input
		    style="width: 70%"
		    v-model="search"
		    size="mini"
		    placeholder="输入关键字搜索"
		  />
		</div>
		
		<el-table :data="tableData" border ref="multipleTable" style="width: 100%">
		  <el-table-column type="selection" width="55"> </el-table-column>
		  <el-table-column prop="order" label="IP" sortable>
		  </el-table-column>
		  <el-table-column prop="source" label="主机名" width="110">
		  </el-table-column>
		  <el-table-column prop="iaas" label="系统类型" width="110">
		  </el-table-column>
		  <el-table-column prop="tenantName" label="网络区域"> </el-table-column>
		  <!-- <el-table-column prop="state" label="订单状态"> </el-table-column> -->
		  <el-table-column prop="estTime" label="创建时间" sortable>
		  </el-table-column>
		  <el-table-column prop="modTime" label="修改时间" sortable>
		  </el-table-column>
		  <el-table-column label="操作">
		    <template slot-scope="scope">
		      <el-button
		        size="mini"
		        type="danger"
		        @click="handleDelete(scope.$index, scope.row)">授权</el-button>
		    </template>
		  </el-table-column>
		</el-table>
		<el-pagination
		  style="float: right"
		  background
		  @size-change="handleSizeChange"
		  @current-change="handleCurrentChange"
		  :current-page.sync="currentPage"
		  :page-sizes="[10, 20, 30, 40]"
		  :page-size="4"
		  layout="sizes, prev, pager, next"
		  :total="100"
		>
		</el-pagination>
	</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rows: [],
      dialogTableVisible: false,
      list: [1],
      search: "",
      currentPage: 1,
      info:null,
      head: [
        {
          order: "订单单号",
          source: "订单来源",
          iaas: "IASS类型",
          tenantName: "租户名",
          state: "订单状态",
          estTime: "创建时间",
          modTime: "修改时间",
        },
      ],
      tableData: [
        {
          order: "ORD20201100011",
          source: "ITA",
          iaas: "开发",
          tenantName: "小红",
          state: "实施中",
          estTime: "2020-11-10",
          modTime: "2020-11-10",
        },
        {
          order: "ORD20201100022",
          source: "ITA",
          iaas: "开发",
          tenantName: "小黄",
          state: "实施中",
          estTime: "2020-11-10",
          modTime: "2020-11-10",
        },
        {
          order: "ORD20201100033",
          source: "ITA",
          iaas: "测试",
          tenantName: "小黑",
          state: "实施中",
          estTime: "2020-11-10",
          modTime: "2020-11-10",
        },
        {
          order: "ORD20201100044",
          source: "ITA",
          iaas: "开发",
          tenantName: "小七",
          state: "实施中",
          estTime: "2020-11-10",
          modTime: "2020-11-10",
        },
        {
          order: "ORD20201100011",
          source: "ITA",
          iaas: "开发",
          tenantName: "小红",
          state: "实施中",
          estTime: "2020-11-10",
          modTime: "2020-11-10",
        },
        {
          order: "ORD20201100022",
          source: "ITA",
          iaas: "开发",
          tenantName: "小黄",
          state: "实施中",
          estTime: "2020-11-10",
          modTime: "2020-11-10",
        },
        {
          order: "ORD20201100033",
          source: "ITA",
          iaas: "测试",
          tenantName: "小黑",
          state: "实施中",
          estTime: "2020-11-10",
          modTime: "2020-11-10",
        },
		{
		  order: "ORD20201100033",
		  source: "ITA",
		  iaas: "测试",
		  tenantName: "小黑",
		  state: "实施中",
		  estTime: "2020-11-10",
		  modTime: "2020-11-10",
		},
      ],
    };
  },
  // created() {
  // 	setTimeout(() => {
  // 		let heig = $(document.body).height()
		// console.log(heig)
  // 		$(".cont_fl").css({
  // 			height: heig + "px"
  // 		});
  // 	},10)
  // },
  methods: {
    handleLook(index, row) {
      $(".dialog-box div").empty();
      console.log($(".dialog-box div").text());
      this.dialogTableVisible = true;
      console.log(index);
      console.log(row);
      this.rows.push(row);
    },
    formatter(row, column) {
      return row.address;
    },
    handleEdit(index, row) {
      console.log(index, row);
    },
    handleDelete(index, row) {
      console.log(index,row)
      this.$axios.get("/#/api/detail/?productID=122").then(function(res){
        console.log(res)
      })
       this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    },
  },
};
</script>

<style>
.content{
	min-height: calc(100vh);
	display: flex;
}
.box {
  width: 30%;
  margin-bottom: 20px;
  float: right;
}
.el-table th.gutter {
  display: table-cell !important;
}
.el-button + .el-button {
  margin-left: 0;
}
.dialog-box_item {
  padding: 15px 5px;
  border-bottom: 1px solid #eee;
}
.cont_fl{
	width: 15%;
	float: left;
	background-color: rgb(84, 92, 100);
}
.el-menu{
	border-right: none !important;
}
.cont_fr{
	width: 80%;
	float: left;
	margin-left: 30px;
	margin-top: 30px;
}
</style>
