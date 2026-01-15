<script setup>
	import Header from '@/components/Header.vue'
	import Aside from '@/components/Aside.vue'
	import Footer from '@/components/Footer.vue'
	import FlowDashboardChart from '@/components/FlowDashboardChart.vue'	
</script>

<template>
  <Header title="លំហូរឯកសារទីស្តីការគណៈរដ្ឋមន្ត្រី" />
  <section class="appppw">
  <Aside />
  <div class="sw">
    <div class="app_content">		
				<div class="ocm_cwr">					
					<h2 class="h wttt ocm_ptitle t-lspace">ផ្ទាំងគ្រប់គ្រប់លំហូរឯកសារសង្ខេប</h2>						
				</div>
							
				<div class="ocm_dashboard_splits">
					<div>
						<div class="ocm_bfw ocm_stat">
					<div class="ocm_caw noneh status_wait">
						<div class="ocm_card_body">
							<div class="ocm_icardw">
							<h5 class="ocm_card_value">១១</h5>
							<div class="ocm_icard">
								<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
							</div>			
							</div>
							<p class="ocm_card_title">លំហូរឯកសារមិនទាន់អនុម័ត</p>
						</div>
					</div>
					<div class="ocm_caw noneh status_accept">
						<div class="ocm_card_body">
						<div class="ocm_icardw">	
						<h5 class="ocm_card_value">៤</h5>
						<div class="ocm_icard">
							<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
						</div>			
						</div>
							<p class="ocm_card_title">លំហូរឯកសារអនុម័តរួច</p>
						</div>
					</div>
					<div class="ocm_caw noneh status_all">
						<div class="ocm_card_body">
							<div class="ocm_icardw">
							<h5 class="ocm_card_value">២៧</h5>
							<div class="ocm_icard">
								<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
							</div>			
							</div>
							<p class="ocm_card_title">លំហូរឯកសារទាំងអស់</p>
						</div>
					</div>
					<div class="ocm_caw noneh status_draft">
						<div class="ocm_card_body">
							<div class="ocm_icardw">
							<h5 class="ocm_card_value">១០</h5>
							<div class="ocm_icard">
								<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
							</div>			
							</div>
							<p class="ocm_card_title">លំហូរឯកសារព្រាង</p>
						</div>
					</div>
					<div class="ocm_caw noneh status_decline">
						<div class="ocm_card_body">
						<div class="ocm_icardw">
						<h5 class="ocm_card_value">២</h5>
							<div class="ocm_icard">
								<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
							</div>			
							</div>
							<p class="ocm_card_title">លំហូរឯកសារមិនយល់ព្រម</p>
						</div>
					</div>
						</div>

						<div class="ocmopt-col cols2 mb-30">
							<div class="ocm_card ocm_doc_fr ocm_dcnew">
								<div class="ocm_card_body">
									<h2 class="h card_tt t-lspace">លំហូរឯកសារថ្មី (២០)</h2>
									<span class="jl_tbl_w">
								<span class="ocm_docfw">
									<span class="ocm_docf d-flex flex-column align-items-center">
									<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
									PDF
									</span>
									3 MB
								</span>
								<span class="jl_tbl_c">
									<span class="tb_n1 bold ellip-2">អនុម័តយល់ព្រមលើកិច្ចព្រមព្រៀងបន្ថែមទៅលើសន្ធិសញ្ញាស្តីពីតំបន់អាស៊ី-អាគ្នេយ៍គ្មានអាវុធ នុយក្លេអ៊ែរ ដែលត្រូវបានអនុម័តដោយរដ្ឋភាគីនៃសន្ធិសញ្ញាស្តីពីតំបន់អាស៊ី-អាគ្នេយ៍គ្មានអាវុធនុយក្លេអ៊ែរ នៅទីក្រុងគូឡាឡាំពួនៃប្រទេសម៉ាឡេស៊ី នាថ្ងៃទី២៥ ខែឧសភា ឆ្នាំ២០២៥ ហើយដែលមានអត្ថបទ ទាំងស្រុងភ្ជាប់មកជាមួយនេះ។</span>
									<span class="tb_n1 fs-90">លិខិតលេខ: នស/រកម / ០០៣២</span>
								</span>
							</span>
							<span class="jl_tbl_w">
								<span class="ocm_docfw">
									<span class="ocm_docf d-flex flex-column align-items-center">
									<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
									PDF
									</span>
									4 MB
								</span>
								<span class="jl_tbl_c"><span class="tb_n1 ellip-2 bold">ផែនការសកម្មភាព ២០២៤-២០២៨ ដើម្បីអនុវត្ដវិធានការគន្លឹះក្នុងការកែទម្រង់រដ្ឋបាលសាធារណៈរបស់រាជរដ្ឋាភិបាលនីតិកាលទី៧ នៃរដ្ឋសភា</span>
								<span class="tb_n1 fs-90">លិខិតលេខ: ផសក្រ / ០០០០</span>
								</span>
							</span>
							<span class="jl_tbl_w">
								<span class="ocm_docfw">
									<span class="ocm_docf d-flex flex-column align-items-center">
									<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
									PDF
									</span>
									2 MB
								</span>
								<span class="jl_tbl_c"><span class="tb_n1 ellip-2 bold">ច្បាប់ស្តីពីការអនុម័តយល់ព្រមលើកិច្ចព្រមព្រៀងស្តីពីការអភិរក្ស និងការប្រើប្រាស់ជីវៈចម្រុះសមុទ្រប្រកបដោយចីរភាព នៅក្រៅដែនយុត្តាធិការជាតិក្រោមអនុសញ្ញា សហប្រជាជាតិស្តីពីច្បាប់សមុទ្រ</span>
								<span class="tb_n1 fs-90">លិខិតលេខ: នស/រកម / ០០៣១</span>											
								</span>
							</span>
							
								</div>
							</div>
							

							<div class="ocm_card ocm_doc_fr ocm_dcwait">
								<div class="ocm_card_body">
									<h2 class="h card_tt t-lspace">លំហូរឯកសារមិនទាន់អនុម័ត (១១)</h2>
									<span class="jl_tbl_w">
								<span class="ocm_docfw">
									<span class="ocm_docf d-flex flex-column align-items-center">
									<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
									PDF
									</span>
									3 MB
								</span>
								<span class="jl_tbl_c"><span class="tb_n1 ellip-2 bold">សេចក្តីសម្រេចស្ដីពីការចាត់តាំង លោកជំទាវ ទេស ផល្លីន អគ្គនាយិកា នៃអគ្គនាយកដ្ឋានរដ្ឋបាល និងហិរញ្ញវត្ថុ ក្រសួងព័ត៌មាន ជាសមាជិកាក្រុមការងាររាជរដ្ឋាភិបាលចុះមូលដ្ឋានខេត្តក្រចេះ។</span>
								<span class="tb_n1 fs-90">លិខិតលេខ: សសរ / ០១០៨</span>
								</span>
							</span>
							<span class="jl_tbl_w">
								<span class="ocm_docfw">
									<span class="ocm_docf d-flex flex-column align-items-center">
									<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
									PDF
									</span>
									3 MB
								</span>
								<span class="jl_tbl_c"><span class="tb_n1 ellip-2 bold">សេចក្តីសម្រេចស្ដីពីការបញ្ចប់ពីសមាជិកក្រុមការងារពិសេសរបស់នាយករដ្ឋមន្ត្រីលើកិច្ចការតាមដាន ត្រួតពិនិត្យ និងវាយតម្លៃការអនុវត្តសកម្មភាព និងវិធានការអាទិភាពក្នុងវិស័យឌីជីថល</span>
								<span class="tb_n1 fs-90">លិខិតលេខ: សសរ / ០១០៧</span>
								</span>
							</span>
							<span class="jl_tbl_w">
								<span class="ocm_docfw">
									<span class="ocm_docf d-flex flex-column align-items-center">
									<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="4 2 16 20"><g fill="none"><path d="M12 8V2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V10h-6a2 2 0 0 1-2-2zm-5 4.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm0 3a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm3-6a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zm0 3a.75.75 0 0 1 .75-.75h5.5a.75.75 0 0 1 0 1.5h-5.5a.75.75 0 0 1-.75-.75zM13.5 8V2.5l6 6H14a.5.5 0 0 1-.5-.5z" fill="currentColor"></path></g></svg>
									PDF
									</span>
									3 MB
								</span>
								<span class="jl_tbl_c"><span class="tb_n1 ellip-2 bold">សេចក្តីសម្រេចស្ដីពីការផ្ទេរនិងសមាហរណកម្មក្រុមការងារកម្ពុជាប្រឆាំងអំពើជួញដូរមនុស្ស នៅមហាអនុតំបន់មេគង្គ ទៅក្នុងក្រុមការងារសហប្រតិបត្តិការអន្តរជាតិ នៃគណៈកម្មាធិការជាតិប្រយុទ្ធប្រឆាំងអំពើជួញដូរមនុស្ស</span>
								<span class="tb_n1 fs-90">លិខិតលេខ: សសរ / ០១០៥</span>
								</span>
							</span>
							
								</div>
							</div>
				
																
						</div>
											
						
						
					</div>
					<div class="ocm_chart_card">
						<FlowDashboardChart />
					</div>
				</div>
			</div>
			<Footer />
		</div>  
</section>
</template>