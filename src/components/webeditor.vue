<template>
	<div id="gjs">
		<slot />
	</div>
	<div id="blocks"></div>
</template>

<script>
	import grapesjs from 'grapesjs'

	export default {
		name: 'WebBuilder',
		mixins: [],

		data() {
			return {
				editor: null
			}
		},
		methods: {
			pushBlock(id, block) {
				this.editor.BlockManager.add(id, block);
			},
			pushCss(selector, rule) {
				this.editor.Css.setRule(selector, rule)
			}
		},
		mounted() {
			this.editor = grapesjs.init({
				container: '#gjs',
				fromElement: true,
				panels: {
					defaults: []
				},
				height: "300px",
				width: "auto",
				blockManager: {
					appendTo: '#blocks'
				},
				storageManager: false
			});

			// Push blocks
			this.pushBlock("1-column", {
				category: "layout",
				label: "1-column",
				content: `<div class="row" data-gjs-droppable=".row-cell" data-gjs-custom-name="Row">
							<div class="row-cell" data-gjs-draggable=".row"></div>
						</div>`
			});

			this.pushBlock("for", {
				category: "special",
				label: 'capitalized_for',
				content: '<div class="label label-for">For</div><div class="data-field"></div>',
			});

			// Push css
			this.pushCss(".row", {
				"display": "flex",
				"justify-content": "flex-start",
				"align-items": "stretch",
				"flex-wrap": "nowrap",
				"padding": "10px",
				"min-height": "75px"
			});

			this.pushCss(".row .row-cell", {
				"flex-grow": "1",
				"flex-basis": "100%",
				"padding": "5px"
			});

			this.pushCss(".label", {
				"color": "grey",
				"padding": "5px"
			});

			this.pushCss(".label-for", {});

			this.pushCss(".data-field", {
				"background-color": "#777",
				"border-radius": "10px",
				"width": "200px",
				"height": "2rem"
			});
		}
	}
</script>
<style src="grapesjs/dist/css/grapes.min.css" />