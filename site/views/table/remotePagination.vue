<template>
  <div style=" width: 100%;height: 300px">
    <bk-table
      :columns="columns"
      :data="remoteData"
      :pagination="pagination"
      :height="300"
      border="horizontal"
      remote-pagination
      @page-value-change="handlePageValueChange"
      @page-limit-change="handlePageLimitChange"
      @column-sort="handleColumnSort"
    />
  </div>
</template>

<script>
  import { defineComponent } from 'vue';

  import { DATA_COLUMNS } from './options';
  const DATA_ROWS = new Array(Math.ceil(Math.random() * 9000) + 1000).fill('')
    .map((_, index) => ({
      ip: `${index}--192.168.0.x`,
      source: `${index}_QQ`,
      status: '创建中',
      create_time: `2018-05-25 15:02:24.${index}`,
    }));

  export default defineComponent({
    components: {},
    data() {
      return {
        tableData: DATA_ROWS,
        columns: [...DATA_COLUMNS],
        pagination: { count: 0, limit: 20, current: 1 },
      };
    },
    computed: {
      remoteData() {
        const { limit, current } = this.pagination;
        const startIndex = (current - 1) * limit;
        const endIndex = current * limit;
        return this.tableData.slice(startIndex, endIndex);
      },
    },
    mounted() {
      setTimeout(() => {
        this.pagination.count = 100;
      }, 300);
    },
    methods: {
      handlePageValueChange(value) {
        this.pagination.current = value;
      },
      handlePageLimitChange(limit) {
        this.pagination.limit = limit;
      },
      handleColumnSort(...args) {
        console.log('sort', args);
      },
    },
  });
</script>
