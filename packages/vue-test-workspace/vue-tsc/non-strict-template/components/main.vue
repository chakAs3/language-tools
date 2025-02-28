<script lang="ts">
import { exactType } from '../../shared';
import { defineComponent, PropType, ref } from 'vue';
import ScriptSetup from './script-setup.vue';
import ScriptSetupExpose from './script-setup-expose.vue';
import ScriptSetupTypeOnly from './script-setup-type-only.vue';
import ScriptSetupDefaultProps from './script-setup-default-props.vue';
import ScriptSetupGeneric from './script-setup-generic.vue';

// https://vuejs.org/api/sfc-script-setup.html#defineprops-defineemits
const ScriptSetupExact = defineComponent({
	props: {
		foo: String,
	},
	emits: ['change', 'delete'],
	setup() {
		return {};
	},
});
// https://vuejs.org/api/sfc-script-setup.html#defineexpose
const ScriptSetupExposeExact = defineComponent({
	setup() {
		const a = 1
		const b = ref(2)
		return {
			a,
			b
		};
	},
});
// https://vuejs.org/api/sfc-script-setup.html#typescript-only-features
const ScriptSetupTypeOnlyExact = defineComponent({
	props: {
		foo: {
			type: String,
			required: true
		},
		bar: Number
	},
	emits: {
		change(_id: number) { },
		update(_value: string) { },
	},
	setup() {
		return {};
	},
});
// https://vuejs.org/api/sfc-script-setup.html#default-props-values-when-using-type-declaration
const ScriptSetupDefaultPropsExact = defineComponent({
	props: {
		msg: {
			type: String,
			default: 'hello'
		},
		labels: {
			type: Array as PropType<string[]>,
			default: () => ['one', 'two']
		},
	},
	setup() {
		return {};
	},
});
// vue 3.3 generic
declare const ScriptSetupGenericExact: <T, >(
	_props: NonNullable<Awaited<typeof _setup>>['props'] & import('vue').VNodeProps & import('vue').AllowedComponentProps & import('vue').ComponentCustomProps,
	_ctx?: Pick<NonNullable<Awaited<typeof _setup>>, 'attrs' | 'emit' | 'slots'>,
	_expose?: NonNullable<Awaited<typeof _setup>>['expose'],
	_setup?: Promise<{
		props: { foo: T } & { [K in keyof JSX.ElementChildrenAttribute]?: { default?(data: T): any } },
		attrs: any,
		slots: { default?(data: T): any },
		emit: { (e: 'bar', data: T): void },
		expose(_exposed: { baz: T }): void,
	}>
) => import('vue').VNode & { __ctx?: Awaited<typeof _setup> };

exactType(ScriptSetup, ScriptSetupExact);
exactType(ScriptSetupExpose, ScriptSetupExposeExact);
exactType(ScriptSetupTypeOnly, ScriptSetupTypeOnlyExact);
exactType(ScriptSetupDefaultProps, ScriptSetupDefaultPropsExact);
exactType(ScriptSetupGeneric, ScriptSetupGenericExact);
</script>
