<template>
	<div class="container-fluid">
		<div class="row flex-nowrap">
			<div class="col-auto col-md-3 col-xl-2 px-sm-2 px-0 bg-dark">
				<div class="d-flex flex-column align-items-center align-items-sm-start px-3 pt-2 text-white min-vh-100">
					<a href="/"
					   class="d-flex align-items-center pb-3 mb-md-0 me-md-auto text-white text-decoration-none">
						<span class="fs-5 d-none d-sm-inline text-uppercase">Quản lý dữ liệu</span>
					</a>
					<ul class="nav nav-pills flex-column mb-sm-auto mb-0 align-items-center align-items-sm-start"
					    id="menu">
						<li class="nav-item">
							<a href="#" class="nav-link align-middle px-0" @click.prevent="this.$router.push('/chart')">
								<i class="bi bi-bar-chart-line-fill"></i> <span class="ms-1 d-none d-sm-inline">Thống kê</span>
							</a>
						</li>
						<li>
							<a href="#submenu1" data-bs-toggle="collapse" class="nav-link px-0 align-middle">
								<i class="bi bi-database-fill"></i> <span class="ms-1 d-none d-sm-inline">Quản lý dữ liệu bảng</span>
							</a>
							<ul class="collapse show nav flex-column ms-1" id="submenu1" data-bs-parent="#menu">
								<li class="w-100" v-for="item in component">
									<a class="nav-link px-0 d-flex m-3" @click.prevent="this.$router.push(item.routerLink)"
									   role="button">
										<span class="d-none d-sm-inline" :title="item.label">{{ item.label }}</span>
									</a>
								</li>
							</ul>
						</li>
					</ul>
					<hr>
					<div class="dropdown pb-4">
						<a href="#" class="d-flex align-items-center text-white text-decoration-none dropdown-toggle"
						   id="dropdownUser1" data-bs-toggle="dropdown" aria-expanded="false">
							<img src="https://github.com/mdo.png" alt="hugenerd" width="30" height="30"
							     class="rounded-circle">
							<span class="d-none d-sm-inline mx-1">Admin</span>
						</a>
						<ul class="dropdown-menu dropdown-menu-dark text-small shadow" aria-labelledby="dropdownUser1">
							<li><a class="dropdown-item" @click.prevent="logout()">Đăng xuất</a></li>
						</ul>
					</div>
				</div>
			</div>
			<div class="col py-3">
				<router-view></router-view>
			</div>
		</div>
	</div>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import CategoryComponent from "@/views/category/CategoryComponent.vue";
import AttributeComponent from "@/views/attribute/AttributeComponent.vue";
import PublisherComponent from "@/views/brand/BrandComponent.vue";
import ProductComponent from "@/views/product/ProductComponent.vue";

export default defineComponent({
	name: "ProductView",
	components: {
		CategoryComponent,
		AttributeComponent,
		PublisherComponent,
		ProductComponent
	},
	data() {
		return {
			component: [
				{name: 'user', show: false, label: 'Quản lý người dùng', routerLink: '/admin/user'},
				{name: 'category', show: false, label: 'Quản lý danh mục', routerLink: '/admin/category'},
				{name: 'brand', show: false, label: 'Quản lý hãng', routerLink: '/admin/brand'},
				{name: 'product', show: false, label: 'Quản lý sản phẩm', routerLink: '/admin/product'},
				{name: 'cart', show: false, label: 'Quản lý đơn hàng', routerLink: '/admin/order'},
				{name:'voucher', show: false, label: 'Quản lý voucher', routerLink: '/admin/voucher'},
				{name: 'attribute', show: false, label: 'Quản lý thuộc tính', routerLink: '/admin/attribute'},
			],
			userCurrent: {
			}
		}
	},
	created() {
		this.init();
	},
	methods: {
		init() {

		},
		logout() {
			this.$router.push('/login');
			localStorage.removeItem('access_token');
		}
	}

})
</script>

<style scoped>

a {
	color: #fff;
}
</style>