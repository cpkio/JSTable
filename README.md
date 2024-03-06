# JSTable²

This is a mod of [JSTable](https://github.com/jstable/JSTable) with row-
and colspanned cells sorting support.

![2024-03-05_09-01-43](https://github.com/cpkio/JSTable/assets/1917113/66c4dbbe-a16b-4943-b94a-ba29d7535588)

Previously sorting such tables broke the table rendering. Now the script
parses the table into separate cells and renders it back to row- and
colspanned table when sorted.

I didn't want pagination, but the original script has no way of disabling it,
so I had to comment it out.

Install with instructions from [JSTable](https://github.com/jstable/JSTable)
repo.

## Antora integration

This has been integrated into Antora-UI as table sorting and filtering solution:

### Build and install

* run `gulp sass` and `gulp uglify` in JSTable folder to get `.js` and `.css`
  files in `dist` folder
* copy `jstable.es5.min.js` to `antora-ui\src\js\vendor\jstable.es5.min.js`
* copy `jstable.css` to `antora-ui\src\css\vendor\jstable.css`

### Load script

`src/partials/head-scripts.hbs`
```
<script src="{{{uiRootPath}}}/js/vendor/jstable.es5.js"></script>
```

### Call script on any standalone table

`src/partials/footer-scripts.hbs`
```
<script>
for ( tbl of document.querySelectorAll('table.tableblock') ) {
  new JSTable(tbl, {
    sortable: true,
    searchable: true,
    addQueryParams: false,
    layout: { top: '{search}', bottom: '{info}' },
    labels: {
      placeholder: 'Поиск…',
      noRows: 'Ничего не найдено',
      info: 'Всего {rows}',
      loading: 'Загрузка…',
      infoFiltered: 'Показано {rows} из {rowsTotal}'
    },
  });
}
</script>
```

JSTable² will not work for inner tables (tables inside tables), as original
JSTable did not. Tables with no header rows are skipped on load.
