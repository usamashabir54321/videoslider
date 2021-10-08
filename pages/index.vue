<template>
	<div>
		<section class="showcase" :class="[ sideBar ? 'active' : '' ]">
			<header>
				<h2 class="logo">Travel</h2>
				<div :class="[ sideBar ? 'active' : '' ]" class="toggle" @click="sideBar = !sideBar"></div>
			</header>
			<div v-for="(vd , index) in vids" :key="index">
				<video v-show="index == selectVid" muted loop autoplay><source :src="`https://attakus.masoodapp.com//video/${vd.src}.mp4`" type="video/mp4"></video>
			</div>
			<div class="overlay"></div>
			<div class="text">
				<h2>Never Stop To </h2> 
				<h3>Exploring The World</h3>
				<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
				<a>Explore {{ selectVid+1 }}</a>
			</div>
			<ul class="social">
				<li><span @click="selectVid -= 1">&#8592;</span></li>
				<li v-for="(vd , index) in vids" :key="index"><span :class="[ index == selectVid ? 'active' : '' ]" @click="selectVid = index"></span></li>
				<li><span @click="selectVid += 1">&#8594;</span></li>
			</ul>
		</section>
		<div class="menu">
			<ul>
				<li><a href="#">Home</a></li>
				<li><a href="#">News</a></li>
				<li><a href="#">Destination</a></li>
				<li><a href="#">Blog</a></li>
				<li><a href="#">Contact</a></li>
			</ul>
		</div>
	</div>
</template>

<script>
	export default {
		data () {
			return {
				sideBar: false,
				vids: [],
				selectVid: 0,
			}
		},
		watch: {
			selectVid (val) {
				if (val > this.vids.length-1) { this.selectVid = 0 }
				else if (val < 0) { this.selectVid = 0 }
			},
		},
		async fetch() {
			await this.myImgArrs();
		},
		fetchDelay: 1000,
		methods: {
			async myImgArrs() {
				const data = [{src:'1'},{src:'2'},{src:'3'},{src:'4'},{src:'5'},{src:'6'},{src:'7'},{src:'8'},{src:'9'},{src:'10'}];
				const result = await data;
				result.forEach((vid) => {
					this.vids.push(vid)
				})
			},
		},
	}
</script>