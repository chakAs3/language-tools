<script lang="ts">
import { exactType } from 'vue-tsc/shared';
import { defineComponent, PropType } from 'vue';
import ScriptSetup from './script-setup.vue';
import ScriptSetupGeneric from './script-setup-generic.vue';

const ScriptSetupExact = defineComponent({
	props: {} as {
		a: PropType<string>;
		b: { type: PropType<string>, required: true };
		c: { type: PropType<number>, required: true };
		d: PropType<number>;
		e: PropType<string>;
		f: { type: PropType<string>, required: true };
		g: PropType<string>;
	},
	setup() {
		return {};
	},
});
declare const ScriptSetupGenericExact: <T, >(
	_props: NonNullable<Awaited<typeof _setup>>['props'] & import('vue').VNodeProps & import('vue').AllowedComponentProps & import('vue').ComponentCustomProps,
	_ctx?: Pick<NonNullable<Awaited<typeof _setup>>, 'attrs' | 'emit' | 'slots'>,
	_expose?: NonNullable<Awaited<typeof _setup>>['expose'],
	_setup?: Promise<{
		props: {
			a?: T | undefined;
			b?: T | undefined;
			c?: T | undefined;
			d: T;
		},
		attrs: any,
		slots: {},
		emit: any,
		expose(_exposed: {}): void,
	}>
) => import('vue').VNode & { __ctx?: Awaited<typeof _setup> };

exactType(ScriptSetup, ScriptSetupExact);
exactType(ScriptSetupGeneric, ScriptSetupGenericExact);
</script>
