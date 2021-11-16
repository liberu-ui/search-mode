<script>
import Modes from '../modes';

export default {
    name: 'CoreSearchMode',

    props: {
        value: {
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

    methods: {
        update(event) {
            this.$emit('input', this.modes[this.next()]);
            this.$emit('change');
            event.stopPropagation();
        },
        next() {
            const current = this.modes.findIndex(mode => mode === this.value);

            return current === this.modes.length - 1 ? 0 : current + 1;
        },
    },

    render() {
        return this.$slots.default({
            clickEvents: {
                click: this.update,
            },
            query: this.query,
            value: this.value,
        });
    },
};
</script>
