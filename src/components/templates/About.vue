<template>
  <div class="ui grid stackable container">

    <div class="row">
      <div class="ui sixteen wide column">

        <h3 class="header">
          關於本站
        </h3>
        <p>
          No bullshit.
        </p>

        <h3 class="header">目的是什麼</h3>
        <p>速度快，直覺的時刻表查詢方式。</p>

        <h3 class="header">使用方法</h3>
        <p>
          格式：<b>起站 迄站 [時間] [車種]</b> <i>(空白分隔)</i>
        </p>
        <p>
          「中壢 臺北」「高雄 台南」「民雄 嘉義」「斗六 員林」
          <br> 「臺北 桃園 明天」「民雄 嘉義 星期六」「斗六 員林 12/8」「汐止 基隆 12月8日」
          <br> 「108 102」「115 板橋 11/26」「桃園 108 明天」
          <br> 「桃園 板橋 自強」「高雄 嘉義 明天 莒光號」「新竹 彰化 對號車」
          <br> 「taitng tapei」「鳳山 新左」「鳳 高」
        </p>
        <p>
          時間支援：「星期六」「週六」「12/8」「12-8」「12月8日」「今天」「明天」「大後天」
          <br> 車站查詢：請用全名或車站代碼，亦可進行模糊搜尋(「高 鳳」「新左 tapei」)，但是沒有簡稱 (北車、高火)
          <br> 車種支援：「莒光號」「自強號」「區間車」「傾斜式」「對號」「站票」.....
        </p>
        <h3 class="header">
          資料來源
        </h3>
        <p>
          交通部開放資料平台 + 自行整理
        </p>
        <h3 class="header">
          關於本專案
        </h3>
        <p>
          Author: <a href="http://benyi.tw" target="_blank">Benyi</a>
          <br> Github: <a href="https://github.com/banqhsia/tra-info" target="_blank">https://github.com/banqhsia/tra-info</a>
          <br> Email: banqhsia _AT_ msn.com
          <br> 如果有任何問題，歡迎來信詢問
          <br> 本站資料僅供參考，詳細以臺鐵公告及現場狀況為準
        </p>
        <h3 class="header">
          更新狀態
        </h3>
        <p v-if="status">
          最近更新日期：{{ moment(status.committer.date).format('YYYY年MM月DD日 HH:mm') }} ( {{ moment(status.committer.date).fromNow() }} )
          <br> 更新訊息：{{ status.message }}
        </p>
        <p v-else>
          取得更新資訊中...
        </p>

      </div>
    </div>
  </div>
</template>


<script>
  export default {

    data() {
      return {
        status: false,
      }
    },
    methods: {
      /**
       * Get Repository status from Github API
       */
      getStatus: function () {

        axios.get(
            'https://api.github.com/repos/banqhsia/tra-info/commits/master'
          )
          .then(
            (response) => {
              this.status = response.data.commit;
            }
          );
      }
    },
    mounted() {
      this.getStatus();
    }

  }

</script>
