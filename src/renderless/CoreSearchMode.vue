<script>
import Modes from '../modes';

export default {
    name: 'CoreSearchMode',

    inheritAttrs: false,

    props: {
        modelValue: {
            type: String,
            default: 'full',
            validator: v => Modes.includes(v),
        },
        modes: {
            type: Array,
            default: () => Modes,
            validator: v => v.every(mode => Modes.includes(mode)),
        },
        query: {
            type: String,
            required: true,
        },
    },

    emits: ['change', 'update:modelValue'],

    methods: {
        update(event) {
            this.$emit('update:modelValue', this.modes[this.next()]);
            this.$emit('change');
            event.stopPropagation();
        },
        next() {
            const current = this.modes.findIndex(mode => mode === this.modelValue);

            return current === this.modes.length - 1 ? 0 : current + 1;
        },
    },

    render() {
        return this.$slots.default({
            clickEvents: {
                click: this.update,
            },
            query: this.query,
            modelValue: this.modelValue,
        });
    },
};
</script>
