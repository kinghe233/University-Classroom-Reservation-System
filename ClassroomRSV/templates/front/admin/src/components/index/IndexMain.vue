<template>
			<el-main style="padding: 10px 20px;
				background: url();
						boxShadow: 0 0 6px rgba(0,0,0,0);
        		">
    		<bread-crumbs :title="title" class="bread-crumbs"></bread-crumbs>
		<router-view class="router-view" style="height:auto;background: transparent;"></router-view>
	</el-main>
</template>

<script>
	import menu from "@/utils/menu";
	export default {
		data() {
			return {
				menuList: [],
				role: "",
				currentIndex: -2,
				itemMenu: [],
				title: '',
			};
		},
		mounted() {
			let menus = menu.list();
			this.menuList = menus;
			this.role = this.$storage.get("role");
		},
		created() {
			this.init();
		},
		methods: {
			init(){
				this.$nextTick(()=>{
				})
			},
			menuHandler(menu) {
				this.$router.push({
					name: menu.tableName
				});
				this.title = menu.menu;
			},
			titleChange(index, menus) {
				this.currentIndex = index
				this.itemMenu = menus;
				console.log(menus);
			},
			homeChange(index) {
				this.itemMenu = [];
				this.title = ""
				this.currentIndex = index
				this.$router.push({
					name: 'home'
				});
			},
			centerChange(index) {
				this.itemMenu = [{
					"buttons": ["add", "check", "update", "delete"],
					"menu": "update password",
					"tableName": "updatePassword"
				}, {
					"buttons": ["add", "check", "update", "delete"],
					"menu": "personal information",
					"tableName": "center"
				}];
				this.title = ""
				this.currentIndex = index
				this.$router.push({
					name: 'home'
				});
				
			}
		}
	};
</script>
<style lang="scss" scoped>
	a {
		text-decoration: none;
		color: #555;
	}

	a:hover {
		background: #00c292;
	}

	.nav-list {
		width: 100%;
		margin: 0 auto;
		text-align: left;
		margin-top: 20px;

		.nav-title {
			display: inline-block;
			font-size: 15px;
			color: #333;
			padding: 15px 25px;
			border: none;
		}

		.nav-title.active {
			color: #555;
			cursor: default;
			background-color: #fff;
		}
	}

	.nav-item {
		margin-top: 20px;
		background: #FFFFFF;
		padding: 15px 0;

		.menu {
			padding: 15px 25px;
		}
	}

	.el-main {
		padding: 0 24px;
		min-height: 100vh;
	}

	.router-view {
		padding: 10px;
		margin-top: 10px;
		background: #FFFFFF;
		box-sizing: border-box;
	}

	.bread-crumbs {
		width: 100%;
		margin-top: 10px;
		box-sizing: border-box;
	}
	
	.detail-form-content {
	    background: transparent;
	}
</style>
