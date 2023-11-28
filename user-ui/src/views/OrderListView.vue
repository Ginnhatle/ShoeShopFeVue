<template>
	<div class="container table-responsive mt-lg-5">
		<table v-if="orderPage?.content?.length > 0" class="table table-striped table-hover table-bordered">
			<thead>
			<tr>
				<th>STT</th>
				<th>Mã đơn hàng</th>
				<th>Địa chỉ</th>
				<th>SĐT</th>
				<th>Họ tên</th>
				<th>Email</th>
				<th>Ngày tạo</th>
				<th>Hình thức thanh toán</th>
				<th>Trạng thái</th>
				<th>Hành động</th>
				<th>Xem đơn hàng</th>
				<th>In hóa đơn</th>
			</tr>
			</thead>
			<tbody>
			<tr v-for="item in orderPage.content">
				<td>{{ item.id }}</td>
				<td>{{ item.code }}</td>
				<td>{{ item.address }}</td>
				<td>{{ item.phoneNumber }}</td>
				<td>{{ item.name }}</td>
				<td>{{ item.email }}</td>
				<td>{{ dateTimeFormat(item.created) }}</td>
				<td>{{ item.paymentMethod }}</td>
				<td>
					<span class="badge"
					      :class="[{'bg-warning': item.status === Order.PENDING},{'bg-success': item.status === Order.CONFIRMED || item.status === Order.DELIVERED || item.status === Order.DELIVERING || item.status === Order.RECEIVED || item.status === Order.AT_STORE},{'bg-danger': item.status === Order.CANCELLED},
					      {'bg-danger' : item.status === Order.RETURNED }]">
						{{ Order.getStatusLabel(item.status) }}
					</span>
				</td>
				<td>
					<button v-if="item.status === Order.CONFIRMED" title="Yêu cầu hoàn hàng" class="btn btn-warning"
					        data-bs-toggle="modal" data-bs-target="#exampleModal" @click.prevent="idCurrent  = item.id | 0">
						<i class="bi bi-arrow-counterclockwise"></i>
					</button>
					<button v-if="item.status === Order.PENDING" title="Hủy đơn hàng" class="btn btn-warning"
					        @click.prevent="cancel(item.id | 0)">
						<i class="bi bi-archive-fill"></i>
					</button>
					<button v-if="item.status === Order.DELIVERING" title="Đã nhận được hàng" class="btn btn-warning"
					        @click.prevent="receivedOrder(item.id | 0)">
						<i class="bi bi-bag-check"></i>
					</button>
				</td>
				<td>
					<button class="btn btn-primary" @click.prevent="$router.push('/order/' + item.id)">
						<i class="bi bi-eye-fill"></i>
					</button>
				</td>
				<td>
					<button class="btn btn-primary" @click.prevent="createPDF(item)" title="In hóa đơn">
						<i class="bi bi-printer-fill"></i>
					</button>
				</td>
			</tr>
			</tbody>
			<tr>
			</tr>
		</table>
	</div>
	<div class="container mt-lg-5">
		<div class="row">
			<div class="col-md-12">
				<div class="d-flex justify-content-between">
					<select @change.prevent="findAll()" v-model="size">
						<option value="10">10</option>
						<option value="20">20</option>
						<option value="50">50</option>
					</select>
					<div class="d-flex">
						<button class="btn btn-primary" @click.prevent="prePage()">
							<i class="bi bi-arrow-left"></i>
						</button>
						<div v-for=" item in orderPage.totalPages">
							<button class="btn btn-primary" @click.prevent="changePage(item - 1)">
								{{ item }}
							</button>
						</div>
						<button class="btn btn-primary" @click.prevent="nextPage()">
							<i class="bi bi-arrow-right"></i>
						</button>
					</div>
				</div>
			</div>
		</div>
	</div>
	<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h1 class="modal-title fs-5" id="exampleModalLabel">Lý do trả hàng</h1>
					<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
				</div>
				<div class="modal-body">
					<textarea class="w-100" placeholder="Lý do trả hàng" v-model="note">
					</textarea>
				</div>
				<div class="modal-footer">
					<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
					<button class="btn btn-primary" @click.prevent="returnOrder(idCurrent)">Xác nhận</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import {Pageable} from "@/core/model/core.base";
import {Order} from "@/core/model/order.model";
import {OrderService} from "@/core/service/order.service";
import html2pdf from 'html2pdf.js';

export default defineComponent({
	name: "OrderListView",
	data() {
		return {
			orderPage: new Pageable<Order>(),
			orderService: new OrderService(),
			userId: Number(localStorage.getItem("userId")) || 0,
			idCurrent: 0,
			page: 0,
			size: 10,
			Order : Order,
			note : "" as string
		}
	},
	methods: {
		findAll() {
			if (this.userId != 0) {
				this.orderService.getOrderByUserId(this.userId, this.page, this.size).then(async res => {
					this.orderPage = await res;
				});
			}
		},
		dateTimeFormat(date: Date) {
			return new Date(date).toLocaleString();
		},
		prePage() {
			if (this.page > 0) {
				this.page--;
				this.findAll();
			}
		},
		nextPage() {
			if(this.orderPage.totalPages){
				if (this.page < this.orderPage.totalPages - 1) {
					this.page++;
					this.findAll();
				}
			}
		},
		changePage(page: number) {
			this.page = page;
			this.findAll();
		},
		cancel(id: number) {
			if(confirm("Bạn có chắc chắn muốn hủy đơn hàng này?")){
				this.orderService.cancelOrder(id).then(res => {
					if (res) {
						this.findAll();
					}
				});
			}
		},
		returnOrder(id: number) {
			if(confirm("Bạn có chắc chắn muốn trả lại đơn hàng này?")){
				this.orderService.returnOrder(id,this.note).then(res => {
					if (res) {
						this.findAll();
					}
				});
			}
		},
		receivedOrder(id: number) {
			if(confirm("Bạn có chắc chắn muốn xác nhận đã nhận hàng?")){
				this.orderService.receiveOrder(id).then(res => {
					if (res) {
						this.findAll();
					}
				});
			}
		},
		createPDF(order: any) {
			const getText = (val : string) => {
				return val && val !== '' ? val : 'Không có';
			}
			let i = 1,html ='',totalPrice = 0;
			html += "<h1 style='text-align: center'>Hóa đơn</h1>";
			html += "<h3 style='text-align: left'>Mã đơn hàng : <b>" + order?.code + "</b></h3>";
			html += "<h4 style='text-align: left'>Ngày tạo : <b>" + this.dateTimeFormat(order?.created) + "</b></h4>";
			html += "<h4 style='text-align: left'>Hình thức thanh toán : <b>" + order?.paymentMethod + "</b></h4>";
			html += "<h4 style='text-align: left'>Trạng thái : " + Order.getStatusLabel(order?.status) + "</h4>";
			html += "<h4 style='text-align: left'>Địa chỉ : " + getText(order?.address) + "</h4>";
			html += "<h4 style='text-align: left'>Số điện thoại : " + getText(order?.phoneNumber) + "</h4>";
			html += "<h4 style='text-align: left'>Họ tên : " + getText(order?.name) + "</h4>";
			html += "<h4 style='text-align: left'>Email : " + getText(order?.email) + "</h4>";
			html += "<h4 style='text-align: left'>Ghi chú : " + getText(order?.note) + "</h4>";
			html += "<hr class='my-4'/>"
			html += "<table class='table table-responsive table-bordered table-striped'><tr><th>STT</th><th>Tên sản phẩm</th><th>Số lượng</th><th>Giá</th><th>Thành tiền</th></tr>";
			order?.orderDetails.forEach((detail: any) => {
				let total = detail.quantity * detail?.price;
				totalPrice += total;
				// Add a row to the HTML table
				html += `<tr><td>${i}</td><td>${detail?.productDetail?.product?.name}</td><td><b>${detail.quantity}</b></td><td><b>${this.formatMoney(detail?.price)}</b></td><td><b>${this.formatMoney(total)}</b></td></tr>`;
				i++;
			});
			// tạo cột tổng tiền colSpan = 4
			html += `<tr><td colspan="4"><b>Tổng tiền</b></td><td><b>${this.formatMoney(totalPrice)}</b></td></tr>`;
			// Close the HTML table
			html += '</table>';
			html2pdf(html, {
				filename: `${order?.phoneNumber}_${Number(new Date())}.pdf`,
			});
		},
		formatMoney(number : number) {
			return new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(number);
		}

	},
	created() {
		this.findAll();
	}
});
</script>

<style scoped>

</style>