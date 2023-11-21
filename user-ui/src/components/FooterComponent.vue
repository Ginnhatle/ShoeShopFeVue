<template>
	<!-- Remove the container if you want to extend the Footer to full width. -->
	<div class="my-5">
<!--		<footer class=" text-center text-lg-start" style="background-color: #262626;">-->
<!--			<div class="container d-flex justify-content-center py-4">-->
<!--				<button type="button" class="btn btn-primary btn-sm btn-floating mx-2"-->
<!--				        style="background-color: #54456b;">-->
<!--					<i class="bi bi-facebook"></i>-->
<!--				</button>-->
<!--				<button type="button" class="btn btn-primary btn-sm btn-floating mx-2"-->
<!--				        style="background-color: #54456b;">-->
<!--					<i class="bi bi-youtube"></i>-->
<!--				</button>-->
<!--				<button type="button" class="btn btn-primary btn-sm btn-floating mx-2"-->
<!--				        style="background-color: #54456b;">-->
<!--					<i class="bi bi-instagram"></i>-->
<!--				</button>-->
<!--				<button type="button" class="btn btn-primary btn-sm btn-floating mx-2"-->
<!--				        style="background-color: #54456b;">-->
<!--					<i class="bi bi-twitter"></i>-->
<!--				</button>-->
<!--			</div>-->

<!--			&lt;!&ndash; Copyright &ndash;&gt;-->
<!--			<div class="text-center text-white p-3" style="background-color: rgba(0, 0, 0, 0.2);">-->
<!--				© 2023 Copyright:-->
<!--				<a class="text-white" href="#">Shoe Shop</a>-->
<!--			</div>-->
<!--			&lt;!&ndash; Copyright &ndash;&gt;-->
<!--		</footer>-->
    <footer class="text-center text-lg-start bg-white text-muted">
      <!-- Section: Social media -->
      <section style="background-color: #E8ECF0" class="d-flex justify-content-center justify-content-lg-between p-4 border-bottom">
        <!-- Left -->
        <div class="me-5 d-none d-lg-block" >
          <span>Kết nối với chúng tôi qua các trang mạng xã hội:</span>
        </div>
        <!-- Left -->

        <!-- Right -->
        <div>
          <a href="" class="me-4 link-secondary">
            <i class="bi bi-facebook"></i>
          </a>
          <a href="" class="me-4 link-secondary">
            <i class="bi bi-twitter"></i>
          </a>
          <a href="" class="me-4 link-secondary">
            <i class="bi bi-google"></i>
          </a>
          <a href="" class="me-4 link-secondary">
            <i class="bi bi-instagram"></i>
          </a>
          <a href="" class="me-4 link-secondary">
            <i class="bi bi-linkedin"></i>
          </a>
          <a href="" class="me-4 link-secondary">
            <i class="bi bi-github"></i>
          </a>
        </div>
        <!-- Right -->
      </section>
      <!-- Section: Social media -->

      <!-- Section: Links  -->
      <section class="">
        <div class="container text-center text-md-start mt-5">
          <!-- Grid row -->
          <div class="row mt-3">
            <!-- Grid column -->
            <div class="col-md-3 col-lg-4 col-xl-3 mx-auto mb-4">
              <!-- Content -->
              <h6 class="text-uppercase fw-bold mb-4">
                <i class="bi bi-gem me-3 text-secondary"></i>Công ty: Shoe Shop
              </h6>
              <p>
                Giày rẻ, đẹp, chất lượng. Hãy đến với shop của chúng tôi để nhận những ưu đãi mới nhất.
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-md-2 col-lg-2 col-xl-2 mx-auto mb-4">
              <!-- Links -->
              <h6 class="text-uppercase fw-bold mb-4">
                Sản Phẩm
              </h6>
              <p>
                <a href="#!" class="text-reset">Angular</a>
              </p>
              <p>
                <a href="#!" class="text-reset">React</a>
              </p>
              <p>
                <a href="#!" class="text-reset">Vue</a>
              </p>
              <p>
                <a href="#!" class="text-reset">Laravel</a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-md-3 col-lg-2 col-xl-2 mx-auto mb-4">
              <!-- Links -->
              <h6 class="text-uppercase fw-bold mb-4">
                Liên kết hữu ích
              </h6>
              <p>
                <a href="#!" class="text-reset">Pricing</a>
              </p>
              <p>
                <a href="#!" class="text-reset">Settings</a>
              </p>
              <p>
                <a href="#!" class="text-reset">Orders</a>
              </p>
              <p>
                <a href="#!" class="text-reset">Help</a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-md-4 col-lg-3 col-xl-3 mx-auto mb-md-0 mb-4">
              <!-- Links -->
              <h6 class="text-uppercase fw-bold mb-4">Liên Hệ</h6>
              <p><i class="fas fa-home me-3 text-secondary"></i> New York, NY 10012, US</p>
              <p>
                <i class="fas fa-envelope me-3 text-secondary"></i>
                info@example.com
              </p>
              <p><i class="fas fa-phone me-3 text-secondary"></i> + 01 234 567 88</p>
              <p><i class="fas fa-print me-3 text-secondary"></i> + 01 234 567 89</p>
            </div>
            <!-- Grid column -->
          </div>
          <!-- Grid row -->
        </div>
      </section>
      <!-- Section: Links  -->

      <!-- Copyright -->
      <div class="text-center p-4" style="background-color: #ccc;">
        © 2021 Copyright:
        <a class="text-reset fw-bold" href="http://localhost:8081/">Shoe Shop</a>
      </div>
      <!-- Copyright -->
    </footer>
    <!-- Footer -->
	</div>
</template>

<script lang="ts">

export default {
	name: 'FooterComponent',
	methods: {}
}
</script>