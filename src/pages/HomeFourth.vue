<template>
  <div class="container">
    <Search :placeholder="placeholder" />
    <el-table
      :data="
        filterData.slice((currentPage - 1) * pageSize, currentPage * pageSize)
      "
      :stripe="true"
      :fit="true"
      :border="true"
      :row-key="getRowkey"
    >
      <TableColumn
        :columnsprops="columnsprops"
        :editRow="editRow"
        :pay="ispay"
      />
    </el-table>
    <TablePagination
      :pageSize="pageSize"
      :currentPage="currentPage"
      :tableDatalength="tableData.length"
      :handleCurrentChange="handleCurrentChange"
    />
  </div>
</template>
<script>
import TableColumn from "@/components/TableColumn.vue";
// import TableEdit from "@/components/TableEdit.vue";
import TablePagination from "@/components/TablePagination.vue";
import Search from "@/components/SearchInput.vue";
import { mapGetters } from "vuex";
import { nanoid } from "nanoid";
export default {
  components: {
    TableColumn,
    // TableEdit,
    TablePagination,
    Search,
  },

  data() {
    return {
      placeholder: "输入进入时间 / 离开时间 / 车牌号",
      ispay: true,
      searchVal: "",
      isSave: true,
      isDelete: true,
      pageSize: 10,
      currentPage: 1,
      editRow: null,
      columnsprops: [
        { prop: "id", label: "车牌号" },
        { prop: "orderid", label: "订单编号" },
        { prop: "phone", label: "手机号" },
        { prop: "start", label: "起始时间" },
        { prop: "leave", label: "离开时间" },
        { prop: "state", label: "状态" },
        { prop: "pay", label: "支付金额" },
        { prop: "delaybton", label: "延时按钮" },
        { prop: "cancelbton", label: "取消按钮" },
      ],
      tableData: [
        {
          orderid: nanoid(),
          phone: 123456,
          id: "湘J374E4",
          start: "2022-04-19 15:23:28",
          leave: "2022-04-19 18:13:48",
          state: "进行中",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "鄂P11515",
          start: "2022-04-19 13:23:28",
          leave: "2022-04-20 18:13:48",
          state: "已完成",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "湘J374E4",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "新CQ9B90",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "等待中",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "新RQ42V7",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "辽J98D3M",
          start: "2022-04-19 13:23:28",
          leave: "2022-04-20 18:13:48",
          state: "进行中",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "黑FM048A",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "云Q7D2D8",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "等待中",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "蒙K4Y9A8",
          start: "2022-04-19 13:23:28",
          leave: "2022-04-20 18:13:48",
          state: "已完成",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "粤ST0U24",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "赣B859Q1",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "等待中",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "川RU62S1",
          start: "2022-04-19 13:23:28",
          leave: "2022-04-20 18:13:48",
          state: "进行中",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "吉F0S673",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "豫K0QE65",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "等待中",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "浙DW67I0",
          start: "2022-04-19 13:23:28",
          leave: "2022-04-20 18:13:48",
          state: "进行中",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "皖AH7284",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "京H720S5",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "等待中",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "青EUP667",
          start: "2022-04-19 13:23:28",
          leave: "2022-04-20 18:13:48",
          state: "进行中",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "黑JJ1S22",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "冀J9H2I1",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "等待中",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "苏H52A27",
          start: "2022-04-19 13:23:28",
          leave: "2022-04-20 18:13:48",
          state: "已完成",
          cancelbton: 0,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "川ZE148I",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "未支付",
          cancelbton: 1,
          pay: "40",
        },
        {
          orderid: nanoid(),
          phone: 123456,
          id: "桂M72185",
          start: "2022-04-19 12:21:28",
          leave: "2022-04-21 18:13:48",
          state: "等待中",
          cancelbton: 1,
          pay: "40",
        },
      ],
    };
  },
  mounted() {
    this.$bus.$on("getSearchVal", this.getSearchVal);
  },
  beforeDestroy() {
    this.$bus.$off("getSearchVal");
  },
  methods: {
    //当前页改变时触发 跳转其他页
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      this.currentPage = val;
    },
    getSearchVal(Val) {
      this.searchVal = Val;
    },
    getRowkey(row) {
      return row.id;
    },
  },
  computed: {
    ...mapGetters(["getloginAd"]),
    filterData() {
      return this.tableData.filter((p) => {
        return (
          p.id.indexOf(this.searchVal) !== -1 ||
          p.leave.indexOf(this.searchVal) !== -1 ||
          p.start.indexOf(this.searchVal) !== -1
        );
      });
    },
  },
};
</script>
<style scoped>
.container {
  background-color: white;
  padding: 20px 20px 20px 20px;
  margin-top: 20px;
  margin-right: 20px;
  box-shadow: 0.2px 0.3px 0.5px rgba(0, 0, 0, 0.024),
    0.6px 0.8px 1.3px rgba(0, 0, 0, 0.035), 1.5px 1.8px 3px rgba(0, 0, 0, 0.046),
    5px 6px 10px rgba(0, 0, 0, 0.07);
  border-radius: 8px;
}
</style>
