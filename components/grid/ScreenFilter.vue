<template>
  <el-row type="flex"
          justify="space-between"
          class="screen-filter-wrap"
          ref="searchForm">
    <el-col class="search-part1">
      <el-form :inline="true" size="small">
        <slot name="slot_one"></slot>
        <el-form-item>
            <el-button plain @click="resetSearch" size="small">重置</el-button>
            <el-button @click="searchBtn" type="primary" size="small">查询</el-button>
        </el-form-item>
      </el-form>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: "screenFilter",
  props: ['searchParams'],
  data () {
    return {
      popVisible: false,
      isMounted: false,
      defaultValue: {}
    };
  },
  computed: {
    popHeight () {
      let top = 145
      if (this.isMounted) {
        top = this.$el.getBoundingClientRect().top
      }
      let popHeight = this.$store.state.screenHeight - top - 75
      if (popHeight < 100) {
        popHeight = 100
      }
      return popHeight + "px"
    }
  },
  mounted: function () {
    this.defaultValue = JSON.parse(JSON.stringify(this.searchParams))
    this.isMounted = true
  },
  methods: {
    resetSearch: function () {
      var _this = this
      for (var item in this.searchParams) {
        _this.searchParams[item] = _this.defaultValue[item];
      }
      _this.getLoadData();
    },
    searchBtn: function () {
      // this.screenOut=false;
      this.getLoadData(); // 根据搜索参数加载
    },
    getLoadData: function () {
      var _this = this
      _this.$parent.$children.forEach(item => {
        if (item.$refs.hasOwnProperty('ListTable')) {
          item.loadData(_this.searchParams) // 重新加载数据
        }
      })
    }
  },
  beforeDestroy: function () {
    $(".screenFilter").off("scroll");
  }
}
</script>

<style lang="less" scoped>
/*.screenFilter {*/
/*    overflow-y: auto;*/
/*}*/

/*.screen-filter-wrap {*/
/*  margin: 18px 0 0 0;*/
/*}*/

.advance_search,
.advance_search:focus,
.advance_search:hover {
  background: @bgGray;
  border: 1px solid rgba(0, 0, 0, 0.15);
  color: @textColor2;
  width: 120px;
}

/*.advance_search /deep/ .el-icon-d-arrow-right {*/
/*    transform: rotate(90deg);*/
/*}*/

/*.open-tooltip /deep/ .el-icon-d-arrow-right {*/
/*    transform: rotate(-90deg);*/
/*}*/
/*.search-part1 {*/
/*    flex: 1;*/
/*}*/

/*.search-part2 {*/
/*    text-align: right;*/
/*    width: 350px;*/
/*}*/

/*.search-part2 /deep/ .search-name {*/
/*    width: 210px;*/
/*    margin-right: 10px;*/
/*}*/

/*.screenFilter /deep/ .date-picker-155.el-date-editor.el-input, .screenFilter /deep/ .date-picker-155.el-date-editor.el-input__inner {*/
/*    width: 162px;*/
/*}*/

/*.screenFilter /deep/ .range {*/
/*    display: inline-block;*/
/*    width: 44px;*/
/*    text-align: center;*/
/*}*/

/*.screenFilter /deep/ .el-date-editor.el-input, .screenFilter /deep/ .el-select {*/
/*    width: 100%;*/
/*}*/
</style>
