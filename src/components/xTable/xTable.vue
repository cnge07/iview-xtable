<template>
  <div>
    <Table
      ref="table"
      :columns="columns"
      v-bind="$props"
      >
    </Table>
    <div style="display:none"> <slot></slot> </div>
  </div>
</template>
<script>
export default {
  props: {
    data: Array,
    stripe: Boolean,
    border: Boolean,
    showHeader: {
      type: Boolean,
      default: true
    },
    width: [Number, String],
    height: [Number, String],
    loading: Boolean,
    disabledHover: Boolean,
    highlightRow: Boolean,
    rowClassName: Function,
    size: String,
    noDataText: String,
    noFilteredDataText: String
  },
  data() {
    return {
      columns: []
    };
  },
  methods: {
    getColumn() {
      if (this.$slots.default) {
        const slots = Array.isArray(this.$slots.default)
          ? this.$slots.default
          : [this.$slots.default];
        Array.from(slots)
          .filter(component => component.componentInstance)
          .forEach(column => {
            const instance = column.componentInstance;
            const o = instance.$options.propsData;
            o.key = o.prop
            if (instance.$scopedSlots.default) {
              o.render = (h, props) => {
                return h("div", instance.$scopedSlots.default(props.row));
              };
            }
            this.columns.push(o);
          });
      }
    }
  },
  mounted() {
    this.getColumn();
    [
      "on-current-change",
      "on-select",
      "on-select-cancel",
      "on-select-all",
      "on-selection-change",
      "on-sort-change",
      "on-filter-change",
      "on-row-click",
      "on-row-dblclick",
      "on-expand"
    ].forEach(evtName => {
      this.$refs.table.$on(evtName, (...args) => {
        this.$emit.call(this, evtName, ...args);
      });
    });

    ["exportCsv", "clearCurrentRow"].forEach(methodName => {
      this[methodName] = this.$refs.table[methodName];
    });
  }
};
</script>

