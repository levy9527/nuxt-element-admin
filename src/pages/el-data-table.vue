<template>
  <el-data-table v-bind="$data" />
</template>

<script>
export default {
  data() {
    return {
      // url: '/deepexi-tenant/modules',
      // url: 'http://localhost:8088/mock/11/getmodules',
      url: 'http://yapi.demo.qunar.com/mock/68321/modules',
      hasEdit: false,
      columns: [
        {
          type: 'selection',
          selectable: (row, index) => index >= 0
        },
        {
          prop: 'name',
          label: '组件名称',
          width: '150px'
        },
        {
          prop: 'type',
          label: '分类',
          width: '150px'
        },
        {
          prop: 'version',
          label: '版本',
          width: '150px'
        },
        {
          prop: 'language',
          label: '开发语言',
          width: '150px'
        },
        {
          prop: 'lastTime',
          label: '最后更新时间',
          width: '150px'
        },
        {
          prop: 'mode',
          label: '状态',
          width: '150px',
          formatter: row =>
            row.mode === '0' ? <div class="shelf">上架</div> : <div>下架</div>
        }
      ],
      searchForm: [
        {
          $type: 'input',
          $id: 'name',
          label: '组件名称',
          $el: {
            placeholder: '请输入'
          }
        },
        {
          $type: 'select',
          $id: 'type',
          label: '分类',
          $options: ['前端组件'].map(f => ({label: f, value: f})),
          $el: {
            placeholder: '请选择'
          }
        },
        {
          $type: 'select',
          $id: 'mode',
          label: '状态',
          $options: ['上架', '未上架'].map(f => ({label: f, value: f})),
          $el: {
            placeholder: '请选择'
          }
        }
      ],
      form: [
        {
          $type: 'input',
          $id: 'name',
          label: '组件名称',
          rules: [
            {
              required: true,
              message: '请输入组件名称',
              trigger: 'blur',
              transform: v => v && v.trim()
            }
          ],
          $el: {
            placeholder: '请输入'
          }
        },
        {
          $type: 'select',
          $id: 'language',
          label: '开发语言',
          rules: [
            {
              required: true,
              message: '请选择开发语言',
              trigger: 'blur'
            }
          ],
          $options: ['javascript', 'java', 'c#'].map(f => ({
            label: f,
            value: f
          })),
          $el: {
            placeholder: '请选择'
          }
        }
      ],
      extraButtons: [
        {
          type: 'primary',
          text: '查看',
          atClick: row => {
            alert(row.name)
            return Promise.resolve()
          }
        },
        {
          text: '编辑',
          atClick: row => {
            alert('编辑' + row.name)
            return Promise.resolve()
          }
        },
        {
          text: '下架',
          atClick: row => {
            alert('下架' + row.name)
            return Promise.resolve()
          }
        }
      ]
    }
  },

  methods: {
    onNew(data, row) {
      // this.$axios.$post(url)
    },
    onEdit(data, row) {
      // this.$axios.$put(url)
    },
    onDelete(row) {
      // this.$axios.$delete(url)
    }
  }
}
</script>

<style lang="less" scoped>
.shelf {
  color: green;
}
</style>
