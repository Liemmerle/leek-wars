<template>
	<v-menu :close-on-content-click="false" :width="280" offset-overflow :nudge-top="bottom ? 0 : 6" :open-delay="_open_delay" :close-delay="_close_delay" :top="!bottom" transition="none" :bottom="bottom" :open-on-hover="!locked" offset-y @input="$emit('input', $event)">
		<template v-slot:activator="{ on }">
			<slot :on="on"></slot>
		</template>
		<div class="card">
			<chip-preview ref="preview" :chip="chip" @input="locked = $event" />
		</div>
	</v-menu>
</template>

<script lang="ts">
	import ChipPreview from '@/component/market/chip-preview.vue'
	import { ChipTemplate } from '@/model/chip'
	import { Component, Prop, Vue, Watch } from 'vue-property-decorator'

	@Component({ components: { ChipPreview } })
	export default class RichTooltipChip extends Vue {
		@Prop({required: true}) chip!: ChipTemplate
		@Prop() bottom!: boolean
		@Prop() instant!: boolean
		locked: boolean = false

		get _open_delay() {
			return this.instant ? 0 : 200
		}
		get _close_delay() {
			return this.instant ? 0 : 200
		}
	}
</script>

<style lang="scss" scoped>
	.card {
		width: 280px;
		background: #eee;
	}
</style>