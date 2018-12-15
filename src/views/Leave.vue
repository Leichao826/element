<template>
	<el-card class="box-card">
		<div slot="header" class="clearfix">
			<span>请假条</span>
			<el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>
		</div>
		姓名： <input type="text" placeholder="请输入姓名" />
		<br /><br />
		<template>
			部门：
			<el-select v-model="value" placeholder="请选择">
				<el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
				</el-option>
			</el-select>
		</template>
		<br /><br />
		<template>
			原因：
			<el-select v-model="values" placeholder="请选择">
				<el-option v-for="item in reasons" :key="item.values" :label="item.labels" :value="item.values">
				</el-option>
			</el-select>
		</template>
		<br /><br />
		<div class="block">
			<span class="demonstration">日期：</span>
			<el-date-picker v-model="value7" type="daterange" range-separator="至" start-placeholder="开始日期" end-placeholder="结束日期">
			</el-date-picker>
		</div>
		<br /> 时间：
		<el-time-select placeholder="起始时间" v-model="startTime" :picker-options="{
      start: '08:30',
      step: '00:15',
      end: '18:30'
    }">
			</el-time-select>
			<el-time-select placeholder="结束时间" v-model="endTime" :picker-options="{
      start: '08:30',
      step: '00:15',
      end: '18:00',
      minTime: startTime
    }">
				</el-time-select>
				<br /><br /> 备注：
				<el-input type="textarea" :autosize="{ minRows: 2, maxRows: 4}" placeholder="请输入内容" v-model="textarea3">
				</el-input>
				<br /><br /> 紧急联系人：
				<input type="text" placeholder="请输入电话与姓名" />
				<br /><br />
		<el-button type="primary" @click="openFullScreen" v-loading.fullscreen.lock="fullscreenLoading">
	提交
</el-button>
                 <el-button>重置</el-button>
	</el-card>
</template>

<script>
	export default {
		data() {
			return {
				options: [{
					value: '选项1',
					label: '产品部'
				}, {
					value: '选项2',
					label: '销售部'
				}, {
					value: '选项3',
					label: '操作部'
				}, {
					value: '选项4',
					label: '订舱部'
				}],
				value: '',
				reasons: [{
					values: '选项1',
					labels: '身体不适'
				}, {
					values: '选项2',
					labels: '突发事件'
				}, {
					values: '选项3',
					labels: '其他原因'
				}],
				values: '',
				pickerOptions2: {
					shortcuts: [{
						text: '最近一周',
						onClick(picker) {
							const end = new Date();
							const start = new Date();
							start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
							picker.$emit('pick', [start, end]);
						}
					}, {
						text: '最近一个月',
						onClick(picker) {
							const end = new Date();
							const start = new Date();
							start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
							picker.$emit('pick', [start, end]);
						}
					}, {
						text: '最近三个月',
						onClick(picker) {
							const end = new Date();
							const start = new Date();
							start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
							picker.$emit('pick', [start, end]);
						}
					}]
				},

				value7: '',
				startTime: '',
				endTime: '',
				textarea3: '',
				 fullscreenLoading: false,
			}
		},
	methods: { 
		openFullScreen() {
        this.fullscreenLoading = true;
        setTimeout(() => {
          this.fullscreenLoading = false;
        }, 2000);
      },},
      
     
	}
</script>

<style>
</style>