<template>
	<el-card class="box-card">
		<div slot="header" class="clearfix">
			<span>请假审核</span>
			<el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>
		</div>
		<el-table :data="leaves" style="width: 100%">
			<el-table-column type="index" width="50"></el-table-column>
			<el-table-column prop="name" label="姓名"></el-table-column>
			<el-table-column prop="reason" label="原因"></el-table-column>
			<el-table-column prop="beizhu" label="备注"></el-table-column>
			<el-table-column prop="time" label="时间"></el-table-column>
			<el-table-column label="操作">
				<template slot-scope="scope">
					<el-button size="mini" @click="dialogVisible=true;">同意</el-button>
					<el-button size="mini" type="danger">驳回</el-button>
				</template>
			</el-table-column>
		</el-table>

		<el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="page" :page-sizes="[10, 20, 30, 40]" :page-size="size" layout="total, sizes, prev, pager, next, jumper" :total="total">
		</el-pagination>

		<el-dialog title="提示" :visible.sync="dialogVisible" width="30%">
			<span>理由充分，批准请假</span>
			<span slot="footer" class="dialog-footer">
		    <el-button @click="dialogVisible = false">取 消</el-button>
		    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
		  </span>
		</el-dialog>

	</el-card>
</template>

<script>
	export default {
		data() {
			return {
				dialogVisible: false,
				size: 10,
				total: 100,
				page: 1,
				leaves: []
			};
		},
		methods: {
			handleSizeChange(s) {
				this.leaves = this.getleaveList(s);
			},
			handleCurrentChange(p) {
				console.log(p);
				this.leaves = this.getleaveList(this.size);
			},
			getleaveList(n) {
				let arr = [];
				let names = ['小明', '小红', '小花', '小李', '小张'];
				let reasons=['身体不适','其他','事假'];
				let beizhus =['望领导批准','希望领导理解','盼批准'];
				let times=['2018-12-18','2018-12-19','2018-12-20','2018-12-21','2018-12-22','2018-12-23','2018-12-24','2018-12-25','2018-12-26','2018-12-27','2018-12-30','2018-12-28','2018-12-29','2018-12-31','2019-01-01','2019-01-02','2019-01-03',]
				for(let i = 0; i < n; i++) {
					let index = Math.floor(Math.random() * names.length);
					let rsn =Math.floor(Math.random() * reasons.length);
					let bz=Math.floor(Math.random() * beizhus.length);
					let ts=Math.floor(Math.random() * times.length);
					let s = {
						id: 1,
						name: names[index],
						reason: reasons[rsn],
						beizhu: beizhus[bz],
						time: times[ts],
					};
					arr.push(s);
				}
				return arr;
			}
		}
	}
</script>

<style>
	.el-pagination {
		margin-top: 20px;
		text-align: center;
	}
</style>