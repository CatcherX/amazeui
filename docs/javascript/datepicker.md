# Datepicker
---

## 使用演示

### 基本形式

在 `<input>` 上增加 `.data-am-datepicker` 属性，调用日期插件。

`````html
<p><input type="text" class="am-form-field am-radius" placeholder="日历组件" data-am-datepicker readonly/></p>

`````
```html
<p><input type="text" class="am-form-field am-radius" placeholder="日历组件" data-am-datepicker readonly/></p>
```

### 结合组件使用

结合 `.am-input-group` 使用，父类添加 class `.am-datepicker-date` ，非 `<input>` 触发元素需增加 `.am-datepicker-add-on` class。

`````html
<div class="am-input-group am-datepicker-date" data-am-datepicker="{format: 'dd-mm-yyyy'}">
  <input type="text" class="am-form-field" placeholder="日历组件" readonly>
  <span class="am-input-group-btn am-datepicker-add-on">
    <button class="am-btn am-btn-default" type="button"><span class="am-icon-calendar"></span> </button>
  </span>
</div>
`````
```html
<div class="am-input-group am-datepicker-date" data-am-datepicker="{format: 'dd-mm-yyyy'}">
  <input type="text" class="am-form-field" placeholder="日历组件" readonly>
  <span class="am-input-group-btn am-datepicker-add-on">
    <button class="am-btn am-btn-default" type="button"><span class="am-icon-calendar"></span> </button>
  </span>
</div>
```

### 更改颜色

默认为蓝色，设置 `theme` 选项可改变颜色：

- `success`: 绿色
- `warning`: 橙色
- `danger`: 红色

`````html
<p><input type="text" class="am-form-field am-radius" placeholder="日历组件" data-am-datepicker="{theme: 'success'}" readonly/></p>

`````
```html
<p><input type="text" class="am-form-field am-radius" placeholder="日历组件" data-am-datepicker="{theme: 'success'}" readonly/></p>
```

### 视图模式

通过参数 `viewMode` 设置日历初始视图模式：

- `days`: 显示天（默认）
- `months`: 显示月
- `years`: 显示年

`````html
<div class="am-input-group am-datepicker-date" data-am-datepicker="{format: 'yyyy-mm-dd', viewMode: 'years'}">
  <input type="text" class="am-form-field" placeholder="日历组件" readonly>
  <span class="am-input-group-btn am-datepicker-add-on">
    <button class="am-btn am-btn-default" type="button"><span class="am-icon-calendar"></span> </button>
  </span>
</div>

`````
```html
<div class="am-input-group am-datepicker-date" data-am-datepicker="{format: 'yyyy-mm-dd', viewMode: 'years'}">
  <input type="text" class="am-form-field" placeholder="日历组件" readonly>
  <span class="am-input-group-btn am-datepicker-add-on">
    <button class="am-btn am-btn-default" type="button"><span class="am-icon-calendar"></span> </button>
  </span>
</div>
```

### 限制视图模式

设置参数 `minViewMode` 可以限制视图模式。下面的示例中限制了只能选择到月份：

`````html
<div class="am-input-group am-datepicker-date" data-am-datepicker="{format: 'yyyy-mm', viewMode: 'years', minViewMode: 'months'}">
  <input type="text" class="am-form-field" placeholder="日历组件" readonly>
  <span class="am-input-group-btn am-datepicker-add-on">
    <button class="am-btn am-btn-default" type="button"><span class="am-icon-calendar"></span> </button>
  </span>
</div>

`````
```html
<div class="am-input-group am-datepicker-date" data-am-datepicker="{format: 'yyyy-mm', viewMode: 'years', minViewMode: 'months'}">
  <input type="text" class="am-form-field" placeholder="日历组件" readonly>
  <span class="am-input-group-btn am-datepicker-add-on">
    <button class="am-btn am-btn-default" type="button"><span class="am-icon-calendar"></span> </button>
  </span>
</div>
```

### 自定义事件

通过监听自定义事件 `changeDate`，可以在回调函数中进行验证等操作。通过 `$().data('date')` 获取改变后的日期。

`````html
<div class="am-alert am-alert-danger" id="my-alert" style="display: none">
  <p>开始日期应小于结束日期！</p>
</div>
<div class="am-g">
  <div class="am-u-sm-6">
    <button type="button" class="am-btn am-btn-default am-margin-right" id="my-start">开始日期</button><span id="my-startDate">2014-12-20</span>
  </div>
  <div class="am-u-sm-6">
    <button type="button" class="am-btn am-btn-default am-margin-right" id="my-end">结束日期</button><span id="my-endDate">2014-12-25</span>
  </div>
</div>
<script>
  $(function() {
    var startDate = new Date(2014, 11, 20);
    var endDate = new Date(2014, 11, 25);
    var $alert = $('#my-alert');
    $('#my-start').datepicker().
      on('changeDate.datepicker.amui', function(event) {
        if (event.date.valueOf() > endDate.valueOf()) {
          $alert.find('p').text('开始日期应小于结束日期！').end().show();
        } else {
          $alert.hide();
          startDate = new Date(event.date);
          $('#my-startDate').text($('#my-start').data('date'));
        }
        $(this).datepicker('close');
      });

    $('#my-end').datepicker().
      on('changeDate.datepicker.amui', function(event) {
        if (event.date.valueOf() < startDate.valueOf()) {
          $alert.find('p').text('结束日期应大于开始日期！').end().show();
        } else {
          $alert.hide();
          endDate = new Date(event.date);
          $('#my-endDate').text($('#my-end').data('date'));
        }
        $(this).datepicker('close');
      });
  });
</script>
`````

```html
<div class="am-alert am-alert-danger" id="my-alert" style="display: none">
  <p>开始日期应小于结束日期！</p>
</div>
<div class="am-g">
  <div class="am-u-sm-6">
    <button type="button" class="am-btn am-btn-default am-margin-right" id="my-start">开始日期</button><span id="my-startDate">2014-12-20</span>
  </div>
  <div class="am-u-sm-6">
    <button type="button" class="am-btn am-btn-default am-margin-right" id="my-end">结束日期</button><span id="my-endDate">2014-12-25</span>
  </div>
</div>
<script>
  $(function() {
    var startDate = new Date(2014, 11, 20);
    var endDate = new Date(2014, 11, 25);
    var $alert = $('#my-alert');
    $('#my-start').datepicker().
      on('changeDate.datepicker.amui', function(event) {
        if (event.date.valueOf() > endDate.valueOf()) {
          $alert.find('p').text('开始日期应小于结束日期！').end().show();
        } else {
          $alert.hide();
          startDate = new Date(event.date);
          $('#my-startDate').text($('#my-start').data('date'));
        }
        $(this).datepicker('close');
      });

    $('#my-end').datepicker().
      on('changeDate.datepicker.amui', function(event) {
        if (event.date.valueOf() < startDate.valueOf()) {
          $alert.find('p').text('结束日期应大于开始日期！').end().show();
        } else {
          $alert.hide();
          endDate = new Date(event.date);
          $('#my-endDate').text($('#my-end').data('date'));
        }
        $(this).datepicker('close');
      });
  });
</script>
```

### 设置禁止选择日期

初始化的时候通过 `onRender` 选项设置禁用日期。

`````html
<div class="am-g">
  <div class="am-u-sm-6">
    设置禁用日期<br/>
    <p><input type="text" class="am-form-field am-radius" placeholder="今天之前的日期被禁用" id="my-start-2"/></p>
  </div>
  <div class="am-u-sm-6">
    禁用日期<br/>
    <p><input type="text" class="am-form-field am-radius" id="my-end-2" /></p>
  </div>
</div>
<script>
  $(function() {
    var nowTemp = new Date();
    var now = new Date(nowTemp.getFullYear(), nowTemp.getMonth(), nowTemp.getDate(), 0, 0, 0, 0);
    var $myStart2 = $('#my-start-2');

    var checkin = $myStart2.datepicker({
      onRender: function(date) {
        return date.valueOf() < now.valueOf() ? 'am-disabled' : '';
      }
    }).on('changeDate.datepicker.amui', function(ev) {
        if (ev.date.valueOf() > checkout.date.valueOf()) {
          var newDate = new Date(ev.date)
          newDate.setDate(newDate.getDate() + 1);
          checkout.setValue(newDate);
        }
        checkin.close();
        $('#my-end-2')[0].focus();
    }).data('amui.datepicker');

    var checkout = $('#my-end-2').datepicker({
      onRender: function(date) {
        return date.valueOf() <= checkin.date.valueOf() ? 'am-disabled' : '';
      }
    }).on('changeDate.datepicker.amui', function(ev) {
      checkout.close();
    }).data('amui.datepicker');

  })
</script>
`````

```html
<div class="am-g">
  <div class="am-u-sm-6">
    设置禁用日期<br/>
    <p><input type="text" class="am-form-field am-radius" placeholder="今天之前的日期被禁用" id="my-start-2"/></p>
  </div>
  <div class="am-u-sm-6">
    禁用日期<br/>
    <p><input type="text" class="am-form-field am-radius" id="my-end-2" /></p>
  </div>
</div>
<script>
  $(function() {
    var nowTemp = new Date();
    var now = new Date(nowTemp.getFullYear(), nowTemp.getMonth(), nowTemp.getDate(), 0, 0, 0, 0);
    var $myStart2 = $('#my-start-2');

    var checkin = $myStart2.datepicker({
      onRender: function(date) {
        return date.valueOf() < now.valueOf() ? 'am-disabled' : '';
      }
    }).on('changeDate.datepicker.amui', function(ev) {
        if (ev.date.valueOf() > checkout.date.valueOf()) {
          var newDate = new Date(ev.date)
          newDate.setDate(newDate.getDate() + 1);
          checkout.setValue(newDate);
        }
        checkin.close();
        $('#my-end-2')[0].focus();
    }).data('amui.datepicker');

    var checkout = $('#my-end-2').datepicker({
      onRender: function(date) {
        return date.valueOf() <= checkin.date.valueOf() ? 'am-disabled' : '';
      }
    }).on('changeDate.datepicker.amui', function(ev) {
      checkout.close();
    }).data('amui.datepicker');

  })
</script>
```

## 调用方式

### 通过 Data API

添加 `data-am-datepicker` 属性，并设置相关选项。

```html
<input class="" data-am-datepicker="{format: 'yyyy-mm'}"/>
```

#### JS 调用

通过 `$().datepicker(options)` 调用。

```javascript
$('#my-datepicker').datepicker({format: 'yyyy-mm'});
```

#### 方法说明

<table class="am-table am-table-bd am-table-striped">
  <thead>
  <tr>
    <th>方法名称</th>
    <th>描述</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td><code>.datepicker('open')</code></td>
    <td>显示日历</td>
  </tr>
  <tr>
    <td><code>.datepicker('close')</code></td>
    <td>隐藏日历</td>
  </tr>
  <tr>
    <td><code>.datepicker('place')</code></td>
    <td>更新调用<code>datepicker</code>的相对位置</td>
  </tr>
  <tr>
    <td><code>.datepicker('setValue', value)</code></td>
    <td>设置<code>Datepicker</code>新值</td>
  </tr>
  </tbody>
</table>

#### 选项说明

- `format`: 日期格式，默认为 `yyyy-mm-dd`，可以选择 `yy/mm/dd` 、`mm/dd` 或者英文日期格式 `dd/mm/yyyy`、`dd/mm/yy`、`dd/mm`等，中间分隔符可以使用 `/`、`-`、` `。
- `viewMode`: type `string`|`integer` 默认为 0 ，设置开始查看模式，传递 `days`、`months`、`years`或者分别对应的 `0`、`1`、`2`。
- `minViewMode`: type `string`|`integer` 默认为 `0`，设置视图模式的限制，传递 `days`、`months`、`years`或者对应的 `0`、`1`、`2`。
- onRender: 渲染日历时调用的函数，比如 `.am-disabled` 设置禁用日期。
- theme: 设置日期颜色主题，接受 `success`、`danger`、`warning` 值，对应为绿色、红色、橙色，默认为蓝色。

设置 `viewMode` 和 `minViewMode` 需要注意日期格式 `format` 的设置。

#### 事件说明

选择日期时，通过查看控制台选择的日期。

`````html
<p><input type="text" class="am-form-field am-radius" placeholder="日历组件" id="doc-datepicker"/></p>
<script>
$(function() {
  $('#doc-datepicker').datepicker().
    on('changeDate.datepicker.amui', function(event) {
      console.log(event.date);
    });
});
</script>
`````

```javascript
$(function() {
  $('#doc-datepicker').datepicker().
    on('changeDate.datepicker.amui', function(event) {
      console.log(event.date);
    });
});
```

<table class="am-table am-table-bd am-table-striped">
  <thead>
  <tr>
    <th>事件名称</th>
    <th>描述</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td><code>changeDate.datepicker.amui</code></td>
    <td>日期改变时触发</td>
  </tr>
  </tbody>
</table>

### 语言扩展

内置英语和简体中文支持，默认为中文，要支持更多语言可以通过 `Datepicker.locales` 添加。
