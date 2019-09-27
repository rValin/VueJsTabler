<template>
    <div>
        <button :disabled="currentStart <= 0" @click="currentStart--">Prev</button>
        <button :disabled="false && currentStart >= cols.cols.length - nb_visible_cols" @click="currentStart++">Next</button>
        <table class="table table-bordered">
            <thead>
            <tr v-for="row in cols.thead">
                <th v-for="col in row" :colspan="col.colspan" :rowspan="col.rowspan" @click="toggle(col.col)">
                    <slot :name="'col-head-' + col.col.key" :col="col.col">
                        {{ col.col.label }}
                    </slot>
                </th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="line in values">
                <td v-for="col in cols.cols">
                    <slot :name="'col-value-' + col.col.key" :line="line" :col="col.col" :values="values">
                        {{ getValue(col.col, line, values) }}
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

                this.keyToCols(this.config.root).forEach(col => {
                    this.loadCol(data, col, undefined);
                });

                let visibleCols = data.cols.slice(this.currentStart, this.currentStart + this.nb_visible_cols);

                let height = 1;
                visibleCols.forEach(col => {
                    let maxHeight = 1;
                    while(col.parent !== undefined) {
                        maxHeight++;
                        col = col.parent;
                    }

                    height = Math.max(maxHeight, height);
                });


                let thead = [];
                visibleCols.forEach(col => {
                    let parents = [];

                    let colParent = col;
                    while(colParent.parent !== undefined) {
                        parents.push(colParent.parent);
                        colParent.parent.rowspan = 1;
                        colParent = colParent.parent;
                    }

                    parents.reverse().forEach((parent, key) => {
                        if (thead[key] === undefined) {
                            thead[key] = [];
                        }
                        thead[key].push(parent);
                    });
                    let nbParents = parents.length;
                    if (thead[nbParents] === undefined) {
                        thead[nbParents] = [];
                    }

                    col.rowspan = height - nbParents;
                    thead[nbParents].push(col);
                });

                thead.forEach(row => {
                    let previous = null;
                    let removedElements = [];

                    row.forEach(col => {
                        if (previous && col.col === previous.col) {
                            previous.colspan++;
                            removedElements.push(col);
                        } else {
                            col.colspan = 1;
                            previous = col;
                        }
                    });

                    removedElements.forEach(col => {
                        row.splice(row.indexOf(col), 1);
                    });
                });

                return {
                    thead: thead,
                    cols: visibleCols,
                };
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
                    this.keyToCols(col.subCols).forEach(subCol => {
                        colspan += this.colspan(subCol);
                    });
                }

                return colspan === 0 ? 1 : colspan;
            },

            loadCol(data, col, parent) {
                if (col.expanded === undefined) {
                    Vue.set(col, 'expanded', false);
                }

                if (!col.expanded || !col.subCols || col.subCols.length === 0) {
                    data.cols.push({
                        parent: parent,
                        col: col,
                        colspan: 1,
                        last: true
                    });

                    return;
                }

                this.keyToCols(col.subCols).forEach(subCol => {
                    this.loadCol(data, subCol, {
                        parent: parent,
                        col
                    })
                });
            },


            getValue(col, line, values) {
                if (typeof col.value === 'string') {
                    return _.get(line, col.value);
                } else if (typeof col.value === 'function') {
                    return col.value(line, values);
                }
            },
            keyToCols(keys) {
                return keys.map(key => {
                    let col = this.config.cols[key];
                    col.key = key;

                    return col;
                }).filter(col => {
                    return this.config.visibility === undefined || this.config.visibility[col.key] !== false
                })
            },

            toggle(col, value) {
                col.expanded = value !== undefined ? value : !col.expanded;

                if (!col.expanded && col.subCols && col.subCols.length > 0) {
                    this.keyToCols(col.subCols).forEach(this.hide)
                }
            },
            hide(col) {
                col.visible = false;
                if (col.subCols && col.subCols.length > 0) {
                    this.keyToCols(col.subCols).forEach(this.hide)
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