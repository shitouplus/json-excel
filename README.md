# json-excel
> 用SheetJS js-xlsx库，使json & excel 互相转换

### excel 转 json
```html
// html
<button>
  <label for="upload">上传</label>
</button>
<input id="upload" hidden type="file" onchange="excelToJson(event)">
```
```js
// js
function excelToJson (e) {
    var reader = new FileReader();
    var file = e.target.files[0];

    reader.onload = function(loadEvent) {
      var data = new Uint8Array(loadEvent.target.result);
      var workbook = XLSX.read(data, {type: 'array'});
      var json = XLSX.utils.sheet_to_json(workbook.Sheets[workbook.SheetNames[0]])

      console.log(json)
    }
    reader.readAsArrayBuffer(file)
  }
```

### json 转 excel
```html
// html
<button onclick="jsonToExcel()">下载excel</button>
```
```js
// js
function jsonToExcel () {
    var filename = "write.xlsx";
    var ws_name = "SheetJS";
    var json = [
      { name: 'a', link: 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa' },
      { name: 'b', link: 'bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb' }
    ];
    var wb = XLSX.utils.book_new();
    var ws = XLSX.utils.json_to_sheet(json);
    XLSX.utils.book_append_sheet(wb, ws, ws_name);
    XLSX.writeFile(wb, filename);
  }
```
