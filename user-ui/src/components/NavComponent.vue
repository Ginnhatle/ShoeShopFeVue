<template>
<!--  navbar navbar-expand-lg bg-white sticky-top navbar-light p-3 shadow-sm-->
<!--  navbar navbar-expand-lg  bg-secondary fixed-top-->
	<nav class="navbar navbar-expand-lg bg-white fixed-top navbar-light p-3 shadow-sm">
		<div class="container">
			<router-link to="/home" class="navbar-brand">Shoe Shop</router-link>
			<button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
			        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
				<span class="navbar-toggler-icon"></span>
			</button>
			<div class="collapse navbar-collapse " id="navbarNav">
				<ul class="navbar-nav me-auto ">
					<li class="nav-item">
						<router-link to="/home" class="nav-link">Trang chủ</router-link>
					</li>
					<li class="nav-item">
						<router-link to="/product" class="nav-link">Sản phẩm</router-link>
					</li>
					<li class="nav-item">
						<router-link to="/contact" class="nav-link">Liên hệ</router-link>
					</li>
				</ul>
				<ul class="navbar-nav">
					<li class="nav-item" v-show="!isLogin">
						<router-link to="/login" class="nav-link" title="Đăng nhập">Đăng nhập</router-link>
					</li>
					<li class="nav-item" v-show="!isLogin">
						<router-link to="/register" class="nav-link" title="Đăng ký">Đăng ký</router-link>
					</li>
					<li class="nav-item" v-show="isLogin === true" title="Giỏ hàng">
						<router-link to="/order" class="nav-link">
							<i class="bi bi-truck-front-fill"></i>
							Đơn hàng
						</router-link>
					</li>
					<li class="nav-item" v-show="isLogin === true" title="Giỏ hàng">
						<router-link to="/cart" class="nav-link">
							<i class="bi bi-cart-fill"></i>
							Giỏ hàng
						</router-link>
					</li>
					<li class="nav-item" v-show="isLogin === true">
						<div class="dropdown">
							<button class="btn btn-light dropdown-toggle" type="button" data-bs-toggle="dropdown"
							        aria-expanded="false">
								Xin chào : {{ user?.username }}
							</button>
							<ul class="dropdown-menu">
								<li>
									<router-link to="/profile" class="dropdown-item">Thông tin tài khoản</router-link>
								</li>
								<li>
									<router-link to="/order" class="dropdown-item">Lịch sử mua hàng</router-link>
								</li>
								<li>
									<router-link to="/voucher" class="dropdown-item">Voucher</router-link>
								</li>
								<li>
									<router-link to="/cart" class="dropdown-item">
										Giỏ hàng
									</router-link>

								</li>
								<li><a class="dropdown-item" @click.prevent="logout()">Đăng xuất</a></li>
							</ul>
						</div>
					</li>
				</ul>
			</div>
		</div>
	</nav>
  <div class="superNav border-bottom py-2 bg-light">
    <div class="container">
      <div class="row">
        <div class="col-lg-6 col-md-6 col-sm-12 col-xs-12 centerOnMobile">
          <select  class="me-3 border-0 bg-light">
            <option value="en-us">EN-US</option>
          </select>
          <span class="d-none d-lg-inline-block d-md-inline-block d-sm-inline-block d-xs-none me-3"><strong>info@somedomain.com</strong></span>
          <span class="me-3"><i class="fa-solid fa-phone me-1 text-warning"></i> <strong>1-800-123-1234</strong></span>
        </div>
        <div class="col-lg-6 col-md-6 col-sm-12 col-xs-12 d-none d-lg-block d-md-block-d-sm-block d-xs-none text-end">
          <span class="me-3"><i class="fa-solid fa-truck text-muted me-1"></i><a class="text-muted" href="#">Shipping</a></span>
          <span class="me-3"><i class="fa-solid fa-file  text-muted me-2"></i><a class="text-muted" href="#">Policy</a></span>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import {defineComponent} from "vue";
import {User} from '@/core/model/user.model';
import {toast} from 'vue3-toastify';

export default defineComponent({
	name: 'NavComponent',
	data() {
		return {
			user: {} as User,
			isLogin: false as boolean
		}
	}, methods: {
		logout() {
			localStorage.removeItem('access_token');
			localStorage.removeItem('user');
			this.$router.push('/login');
			toast.success('Đăng xuất thành công');
		}
	},
	created() {
		this.user = JSON.parse(localStorage.getItem('user') || '{}');
		this.isLogin = localStorage.getItem('access_token') ? true : false;
	}
});
</script>

<style scoped>
li {
	cursor: pointer;
}
</style>