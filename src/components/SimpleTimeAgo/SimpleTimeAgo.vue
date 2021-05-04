<template>
	<div>
		{{ formattedDate }}
		<!-- <slot></slot> -->
	</div>
</template>

<script>
export default {
	name: "SimpleTimeAgo",
	props: {
		date: { // Required date to calculate timeago
			type: [String, Number],
			required: true,
		},
		initialUpper: { // Set initial letter to uppercase
			type: Boolean,
			default: true
		}
	},
	data() {
		return {
			dateUnits: {
				day: 86400,
				hour: 3600,
				minute: 60,
				second: 1,
			},
			formattedDate: this.date,
		};
	},
	methods: {
		getSecondsDiff(timestamp) {
			return (Date.now() - timestamp) / 1000;
		},
		getUnitAndValueDate(secondsElapsed) {
			for (const [unit, secondsInUnit] of Object.entries(this.dateUnits)) {
				if (secondsElapsed >= secondsInUnit || unit === "second") {
					const value = Math.floor(secondsElapsed / secondsInUnit) * -1;
					return { value, unit };
				}
			}
		},
		getTimeAgo() {
			const givenDate = typeof this.date === "string" ? Date.parse(this.date) : this.date
			const rtf = new Intl.RelativeTimeFormat();
			const secondsElapsed = this.getSecondsDiff(givenDate);
			const { value, unit } = this.getUnitAndValueDate(secondsElapsed);
			this.formattedDate = rtf.format(value, unit);
		},
	},
	created() {
		this.getTimeAgo();
	},
};
</script>
