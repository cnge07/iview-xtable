<template>
  <div class="demo">
    <p>stripe:
      <i-switch v-model="xTableOptions.stripe"></i-switch>
    </p>
    <p>border:
      <i-switch v-model="xTableOptions.border"></i-switch>
    </p>
    <p>showHeader:
      <i-switch v-model="xTableOptions.showHeader"></i-switch>
    </p>
    <p>loading:
      <i-switch v-model="xTableOptions.loading"></i-switch>
    </p>
    <p>disabledHover:
      <i-switch v-model="xTableOptions.disabledHover"></i-switch>
    </p>
    <p>highlightRow:
      <i-switch v-model="xTableOptions.highlightRow"></i-switch>
    </p>
    <p>
      <RadioGroup v-model="xTableOptions.size" type="button">
        <Radio label="small"></Radio>
        <Radio label="default"></Radio>
        <Radio label="large"></Radio>
      </RadioGroup>
    </p>
    <x-table :data="tabledata" v-bind="xTableOptions" @on-row-click="onRowClick">
      <x-table-column type="expand" :width="60" align="center">
        <template slot-scope="scope">
          展开
        </template>
      </x-table-column>
      <x-table-column type="selection" :width="60" align="center"></x-table-column>


      <x-table-column title="Age" prop="age" :filters="[{
                                label: 'Greater than 25',
                                value: 1
                            }]"
                            :filterMethod="()=>(true) "
                            ></x-table-column>
      <x-table-column title="Address" prop="address"></x-table-column>
      <x-table-column title="Date" prop="date"></x-table-column>
      <x-table-column title="Action">
        <template slot-scope="scope">
            <Button type="primary" @click="$Modal.info({
                  title: '提示',
                  content: `查看 ${scope.name} 的信息`
              })">查看</Button>
            <Button type="warning" @click="$Modal.warning({
                  title: '提示',
                  content: `点击编辑 ${scope.name} 的信息`
              })">编辑</Button>
            <Button type="error" @click="$Modal.error({
                  title: '警告',
                  content: `确定要删除用户： ${scope.name} ？`
              })">删除</Button>
        </template>
      </x-table-column>
    </x-table>
  </div>
</template>

<script>
  import xTable from "@/components/xTable/xTable";
  import xTableColumn from "@/components/xTable/xTableColumn";
  export default {
    components: {
      xTable,
      xTableColumn
    },
    data() {
      return {
        xTableOptions: {
          stripe: false,
          border: false,
          showHeader: true,
          loading: false,
          disabledHover: false,
          highlightRow: false,
          size: "default",
          noDataText: "暂无数据",
          noFilteredDataText: "暂无筛选结果"
        },
        tabledata: [{
            name: "John Brown",
            age: 18,
            address: "New York No. 1 Lake Park",
            date: "2016-10-03"
          },
          {
            name: "Jim Green",
            age: 24,
            address: "London No. 1 Lake Park",
            date: "2016-10-01"
          },
          {
            name: "Joe Black",
            age: 30,
            address: "Sydney No. 1 Lake Park",
            date: "2016-10-02"
          },
          {
            name: "Jon Snow",
            age: 26,
            address: "Ottawa No. 2 Lake Park",
            date: "2016-10-04"
          }
        ]
      };
    },
    methods: {
      onRowClick(args) {
        console.log(args);
      }
    }
  };
</script>

<style>
  .demo {
    padding: 20px;

  }
  .demo > p {
      margin-bottom: 10px;
    }
</style>
