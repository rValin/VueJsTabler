<template>
  <div>
    <button :disabled="currentStart <= 0" @click="currentStart--">Prev</button>
    <button :disabled="currentStart >= cols.cols.length - nb_visible_cols" @click="currentStart++">Next</button>
    <table class="table table-bordered">
      <thead>
      <tr v-for="(row, index) in cols.thead">
        <th v-for="col in row" :colspan="colspan(col.col)" :rowspan="rowspan(col, index)" :class="{'hidden-cell': !col.col.visible}" @click="toggle(col.col)">
          <slot :name="'col-head-' + col.col.key" :col="col.col">
            {{ col.col.label }}
          </slot>
        </th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="line in values">
        <td v-for="col in cols.cols" :class="{'hidden-cell': !col.visible}">
          <slot :name="'col-value-' + col.key" :line="line">
            {{ getValue(col, line) }}
          </slot>
        </td>
      </tr>
      </tbody>
    </table>
  </div>

</template>

<script>
  import Vue from 'vue';
  import _ from 'lodash';

export default {
  name: 'Tabler',
  props: {
    config: Object,
    values: Array,
    start: {
      type: Number,
      default: 0,
    },
    nb_visible_cols: {
      type: Number,
      default: 5
    }
  },
  data() {
    return {
      currentStart: this.start,
    }
  },
  computed: {
    cols() {
      let data = {
        thead: [],
        cols: [],
      };

      this.config.cols.forEach(col => {
        this.loadCol(data, col, 0);
      });

      data.thead.forEach(row => {
        let rowPosition = 0;
        row.forEach(col => {
          if (col.col.visible === undefined) {
            Vue.set(col.col, 'visible', false);
          }
          col.col.visible = (rowPosition >= this.currentStart || (rowPosition + (col.colspan -1)) >= this.currentStart) && rowPosition < this.currentStart + this.nb_visible_cols;

          if (col.col.label === 'Détails') {
            console.log(
                    col,
                    rowPosition,
                    this.currentStart,
                    (rowPosition >= this.currentStart || (rowPosition + (col.colspan -1)) >= this.currentStart),
                    rowPosition < this.currentStart + this.nb_visible_cols
            )
          }
          rowPosition += col.colspan;

          // if (rowPosition < this.currentStart && col.col.visible) {
          //   col.colspan -= (this.currentStart - rowPosition)
          // }
          //
          // if (rowPosition + col.colspan > this.currentStart + this.nb_visible_cols) {
          //   col.colspan = this.currentStart + this.nb_visible_cols - rowPosition;
          // }

        })
      });

      data.cols.forEach((col, index) => {
        if (col.visible === undefined) {
          Vue.set(col.visible, 'visible', false);
        }
        col.visible = index >= this.currentStart && index < this.currentStart + this.nb_visible_cols;
      });

      return data;
    }
  },
  methods: {
    rowspan(col, index) {
      return col.last ? this.cols.thead.length - index : 1;
    },
    colspan(col) {
      if (!col.visible) {
        return 0;
      }

      let colspan = 0;
      if (col.subCols !== undefined && col.subCols.length > 0) {
        col.subCols.forEach(subCol => {
          colspan += this.colspan(subCol);
        });
      }

      return colspan === 0 ? 1 : colspan;
    },

    loadCol(data, col, level, parent) {
      if (col.expanded === undefined) {
        Vue.set(col, 'expanded', false);
      }

      if(!data.thead[level]) {
        data.thead[level] = [];
      }

      if (!col.expanded || !col.subCols || col.subCols.length === 0) {
        data.cols.push(col);
        data.thead[level].push({
          col: col,
          colspan: 1,
          last: true
        });

        return 1;
      }

      let colspan = 0;
      col.subCols.forEach(subCol => {
        colspan += this.loadCol(data, subCol, level + 1)
      });

      data.thead[level].push({
        col: col,
        colspan: colspan,
        last: false
      });

      return colspan;
    },


    getValue(col, line) {
      if (typeof col.value === 'string') {
        return _.get(line, col.value);
      } else if (typeof col.value === 'function') {
        return col.value(line);
      }
    },

    toggle(col, value) {
      col.expanded = value !== undefined ? value : !col.expanded;

      if (!col.expanded && col.subCols && col.subCols.length > 0) {
        col.subCols.forEach(this.hide)
      }
    },
    hide(col) {
      col.visible = false;
      if (col.subCols && col.subCols.length > 0) {
        col.subCols.forEach(this.hide)
      }
    }
  }
}
</script>

<style scoped>
  table {
    table-layout: fixed;
  }

  .hidden-cell {
    /*width: 0;*/
    display: none;
  }
</style>