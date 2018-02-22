<template>
  <div class="container">
    <h1>{{$t('default.shotgun')}}</h1>
    <my-table v-if="!error" v-bind:rows="rows"></my-table>
    <div v-if="error">{{$t('default.failedToLoad')}}</div>
  </div>
</template>

<script>
import MyTable from "~/components/my-table.vue";
import { getUrl, updateUrl } from "~/helpers";

export default {
  head() {
    const link = [];
    const url = `https://ammobin.ca/${
      this.$i18n.locale !== "en" ? this.$i18n.locale + "/" : ""
    }shotgun`;
    if (this.page > 1) {
      link.push({
        rel: "prev",
        href: getUrl(url, this.page - 1, this.calibre)
      });
    }

    if (this.pages > this.page) {
      link.push({
        rel: "next",
        href: getUrl(url, this.page + 1, this.calibre)
      });
    }

    return {
      title: this.calibre + " Shotgun Prices", //TODO: en francais
      meta: [
        {
          hid: "description",
          name: "description",
          content: `The place to view the best ${
            this.calibre
          } shotgun shell prices across Canada.` //TODO: en francais
        }
      ],
      link
    };
  },
  components: {
    MyTable
  },
  data() {
    return {
      error: null,
      rows: [],
      calibre: "",
      page: 1,
      pages: 1
    };
  },
  async asyncData({ error, query, app }) {
    try {
      const page = parseInt(query.page || "1");
      const calibre = query.calibre || "";
      const pageSize = parseInt(query.pageSize || "25", 10);

      let res = await app.$axios.get(
        BASE_API_URL +
          `shotgun?calibre=${encodeURIComponent(calibre)}&page=${page}`
      );
      const rows = res.data;
      return { rows, calibre, page, pages: Math.ceil(rows.length / pageSize) };
    } catch (e) {
      console.error(e);
      return { statusCode: 500, message: "Failed to load prices", error: true };
    }
  }
};
</script>
