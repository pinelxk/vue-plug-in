<template>
  <div class="dragTable">

    <td-draggable element="el-table" :list="tableData" :data="tableData" :options="dragOptions" dragSelector="tbody" @end='endDrag'>

      <el-table-column  type="index" label="序号" width="70">
        <template slot-scope="scope">
          {{1+scope.$index}}
        </template>
      </el-table-column>
      <template v-for="column in columns">
        <el-table-column v-if="column.formatter" :fixed="column.fixed" resizable show-overflow-tooltip :prop="column.prop" :key="column.prop" :label="column.label" :formatter="column.formatter" >
        </el-table-column>
        <el-table-column  v-else-if="column.operations" :fixed="column.fixed" :prop="column.prop" :label="column.label" :key="column.prop" >
          <template slot-scope="scope">
            <el-button v-for="(operate, index) in column.operations" :key="index" type="text" @click.native.prevent="operate.func(scope.$index, scope.row)">{{operate.label}}</el-button>
          </template>
        </el-table-column>

        <el-table-column v-else resizable show-overflow-tooltip :fixed="column.fixed" :prop="column.prop"   :label="column.label" :key="column.prop" >
        </el-table-column>
      </template>
    </td-draggable>
  </div>
</template>

<script>
export default {
  name: 'elementDraggableTable',
  data () {
    return {
      dragOptions: {
        draggable: '.el-table__row'
      },
      tableData: [
        {'no': 122, 'type': '222'},
        {'no': 233, 'type': '112'},
        {'no': 3444, 'type': 'aaa'},
        {'no': 5555, 'type': 'bb'},
        {'no': 666, 'type': 'cc'},
        {'no': 777, 'type': 'dd'},
        {'no': 888, 'type': 'ee'},
        {'no': 999, 'type': 'rr'},
        {'no': 100, 'type': 'tt'},
        {'no': 'aaa', 'type': 'qq'}
      ],
      columns: [{
        prop: 'no',
        label: '盘点单号'
      }, {
        prop: 'type',
        label: '盘点类型',
        formatter: function (item) {
          return 'cc'
        }
      }]
    }
  },
  components: {
  },
  methods: {
    endDrag (data) {
      console.log('data: ', data)
      console.log(this.tableData)
    }
  }
}
</script>
