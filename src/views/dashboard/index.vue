<template>
	<div class="dashboard-container">
		<!-- <Moveable
			class="moveable"
			v-bind="moveable"
			@drag="handleDrag"
			@resize="handleResize"
			@scale="handleScale"
			@rotate="handleRotate"
			@warp="handleWarp"
			@pinch="handlePinch"
		>
			<span>Vue Moveable</span>
		</Moveable> -->

		<el-upload
			class="upload-demo"
			drag
			:on-preview="handlePreview"
			:on-remove="handleRemove"
			:file-list="fileList"
			multiple
			action=""
		>
			<i class="el-icon-upload"></i>
			<div class="el-upload__text">
				Drop file here or <em>click to upload</em>
			</div>
			<div class="el-upload__tip" slot="tip">
				jpg/png files with a size less than 500kb
			</div>
		</el-upload>
	</div>
</template>

<script>
import { mapGetters } from 'vuex';
import Moveable from 'vue-moveable';
export default {
	data() {
		return {
			moveable: {
				draggable: true,
				throttleDrag: 1,
				resizable: false,
				throttleResize: 1,
				keepRatio: false,
				scalable: true,
				throttleScale: 0,
				rotatable: false,
				throttleRotate: 0,
				pinchable: false, // ["draggable", "resizable", "scalable", "rotatable"]
				origin: false,
			},
			fileList: [],
		};
	},
	name: 'Dashboard',
	components: {
		Moveable,
	},
	computed: {
		...mapGetters(['name']),
	},
	methods: {
		handleUpload() {},
		handlePreview() {},
		handleRemove() {},
		handleDrag({ target, transform }) {
			console.log('onDrag left, top', transform);
			target.style.transform = transform;
		},
		handleResize({ target, width, height, delta }) {
			console.log('onResize', width, height);
			delta[0] && (target.style.width = `${width}px`);
			delta[1] && (target.style.height = `${height}px`);
		},
		handleScale({ target, transform, scale }) {
			console.log('onScale scale', scale);
			target.style.transform = transform;
		},
		handleRotate({ target, dist, transform }) {
			console.log('onRotate', dist);
			target.style.transform = transform;
		},
		handleWarp({ target, transform }) {
			console.log('onWarp', transform);
			target.style.transform = transform;
		},
		handlePinch({ target }) {
			console.log('onPinch', target);
		},
	},
};
</script>

<style lang="scss" scoped>
.dashboard-container {
	display: flex;
	align-items: center;
	justify-content: center;
}
.dashboard {
	&-container {
		margin: 30px;
	}
	&-text {
		font-size: 30px;
		line-height: 46px;
	}
}
.moveable {
	font-family: 'Roboto', sans-serif;
	position: relative;
	width: 300px;
	height: 200px;
	text-align: center;
	font-size: 40px;
	margin: 0 auto;
	font-weight: 100;
	letter-spacing: 1px;
	display: flex;
	align-items: center;
	justify-content: center;
}
</style>
