<template>
  <div class="side-bar__panel side-bar__panel--menu">
    <menu-entry @click.native="exportMarkdown">
      <icon-download slot="icon"></icon-download>
      <div>Export as Markdown</div>
      <span>Save plain text file.</span>
    </menu-entry>
    <menu-entry @click.native="exportHtml">
      <icon-download slot="icon"></icon-download>
      <div>Export as HTML</div>
      <span>Generate an HTML page from a template.</span>
    </menu-entry>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import MenuEntry from './common/MenuEntry';
import exportSvc from '../../services/exportSvc';
import store from '../../store';

export default {
  components: {
    MenuEntry,
  },
  computed: mapGetters(['isSponsor']),
  methods: {
    exportMarkdown() {
      const currentFile = store.getters['file/current'];
      return exportSvc.exportToDisk(currentFile.id, 'md')
        .catch(() => { /* Cancel */ });
    },
    exportHtml() {
      return store.dispatch('modal/open', 'htmlExport')
        .catch(() => { /* Cancel */ });
    },
    exportPdf() {
      return store.dispatch('modal/open', 'pdfExport')
        .catch(() => { /* Cancel */ });
    },
    exportPandoc() {
      return store.dispatch('modal/open', 'pandocExport')
        .catch(() => { /* Cancel */ });
    },
  },
};
</script>
