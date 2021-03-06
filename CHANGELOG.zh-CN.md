## 更新日志

### 2.0.0-rc.1
*2017-10-25*

#### 新特性
- Form
  - 新增 `clearValidate` 方法，用于清空所有表单项的验证信息，#7623
- MessageBox
  - 新增 `inputType` 属性，用户指定内部输入框的类型，#7651
- Table
  - 新增 `size` 属性，用于控制表格尺寸
  - 新增 `toggleRowExpansion` 方法，用于手动展开或关闭行
  - 新增 `cell-class-name` 属性，用于指定单元格的类名
  - 新增 `cell-style` 属性，用于指定单元格的样式
  - 新增 `header-row-class-name` 属性，用于指定表头行的类名
  - 新增 `header-row-style` 属性，用于指定表头行的样式
  - 新增 `header-cell-class-name` 属性，用于指定表头单元格的类名
  - 新增 `header-cell-style` 属性，用于指定表头单元格的样式
  - TableColumn 的 `prop` 属性支持 `object[key]` 格式
  - TableColumn 新增 `index` 属性，用于自定义索引值

#### 修复
- Table
  - 修复 `max-height` 变更后无法恢复的问题
  - 修复一些样式上的计算错误

#### 非兼容性更新
- Autocomplete
  - 移除 `props` 属性，现在使用 `value-key` 属性指定输入建议对象中用于显示的键名
- Table
  - 将 `append` slot 移至 `tbody` 元素以外，以保证其只被渲染一次
  - `expand` 事件更名为 `expand-change`，以保证 API 的命名一致性
  - `row-class-name` 和 `row-style` 的函数参数改为对象，以保证 API 的一致性

### 2.0.0-beta.1
*2017-10-20*

#### 新特性
- 综合
  - 新增 TypeScript 类型声明
  - 重绘了全部图标，并新增了部分图标
  - 为部分非兼容性更新增加控制台警告，方便迁移项目。当你在项目中使用了被移除或更名了的属性或事件时，控制台会出现一条警告，例如：
  ```
  [Element Migrating][ElSwitch][Attribute]: on-color is renamed to active-color.
  ```
  - 新增了一系列基于断点的工具类，用于当视口尺寸满足一定条件时隐藏元素
- Layout
  - 新增断点 `xl`，适用于宽度大于 1920px 的视口
- Table
  - 新增 `span-method` 属性，用于合并行或列
  - 新增 `clearSort` 方法，用于清空排序状态
  - 新增 `clearFilter` 方法，用于清空过滤状态
  - 对于可展开行，当该行展开时会获得一个 `.expanded` 类名，方便自定义样式
- DatePicker
  - 新增 `unlink-panels` 属性，用于在选择日期范围时取消两个日期面板之间的联动
- Select
  - 新增 `reserve-keyword` 属性，用于在选择某个选项后保留当前的搜索关键词

#### 修复
- Table
  - 修复 TableColumn 的 `header-align` 属性失效的问题
  - 修复 Table 在父元素从 `display: none` 变成其他状态时会隐藏的问题
  - 修复 Table 在父元素为 `display: flex` 时可能出现的宽度逐渐变大的问题
  - 修复 `append` 具名 slot 和固定列并存时，动态获取表格数据会导致固定列消失的问题
  - 修复 `expand-row-keys` 属性初始化无效的问题
  - 修复 `data` 改变时过滤条件失效的问题
  - 修复多级表头时固定列隐藏情况计算错误的问题

#### 非兼容性更新
- Switch
  - 由于 `on-*` 属性在 JSX 中会被识别为事件，导致 Switch 所有 `on-*` 属性在 JSX 中无法正常工作，所以 `on-*` 属性更名为 `active-*`，对应地，`off-*` 属性更名为 `inactive-*`。受到影响的属性有：`on-icon-class`、`off-icon-class`、`on-text`、`off-text`、`on-color`、`off-color`、`on-value`、`off-value`
- Table
  - `sort-method` 现在和 `Array.sort` 保持一致的逻辑，要求返回一个数字。

### 2.0.0-alpha.3
*2017-10-16*

#### 新特性
- 综合
  - 新增全局配置组件尺寸的功能：在引入 Element 时，配置 `size` 字段可以改变所有组件的默认尺寸。当完整引入 Element 时：
  ```JS
  import Vue from 'vue'
  import Element from 'element-ui'
  Vue.use(Element, { size: 'small' })
  ```
  当按需引入 Element 时：
  ```JS
  import Vue from 'vue'
  import { Button } from 'element-ui'
  Vue.prototype.$ELEMENT = { size: 'small' }
  Vue.use(Button)
  ```
  按照以上设置，项目中所有拥有 `size` 属性的组件的默认尺寸均为 'small'。
- Loading
  - 配置对象新增 `spinner` 和 `background` 字段，支持自定义加载图标和背景色，#7390
- Autocomplete
  - 新增 `debounce` 属性，#7413
- Upload
  - 新增 `limit` 和 `on-exceed` 属性，支持对上传文件的个数进行限制，#7405
- Menu
  - 新增 `open` 和 `close` 方法，支持手动打开和关闭 SubMenu，#7412
- DatePicker
  - 新增 `value-format` 属性，支持对绑定值的格式进行自定义，#7367
- TimePicker
  - 新增 `arrow-control` 属性，提供另一种交互形式，#7438
- DateTimePicker
  - 新增 `time-arrow-control` 属性，用于开启时间选择器的 `arrow-control`，#7438
- Form
  - Form 和 Form-item 新增 `size` 属性，用于控制表单内组件的尺寸，#7428
  - `validate` 方法在不传入 callback 的情况下返回 promise，#7405

#### 修复
  - 修复部分组件的 `Injection "elFormItem" not found` 报错

#### 非兼容性更新
  - DatePicker 的 `change` 事件参数现在为组件的绑定值，格式由 `value-format` 控制
  - Input 组件的 `change` 事件现在仅在输入框失去焦点或用户按下回车时触发，与原生 input 元素一致。如果需要实时响应用户的输入，可以使用 `input` 事件
  - 最低兼容 Vue 2.5.2 版本

### 2.0.0-alpha.2
*2017-10-05*

- 修正 `theme-chalk` 的主色，#7351
- 修复使用 Dropdown 时控制台报错的问题，#7322
- 修复使用 Menu 时控制台报错的问题，#7321
- ColorPicker 新增 `popper-class` 属性，#7351
- 修复 Button 的 `disabled` 属性无效的问题，#7352

### 2.0.0-alpha.1
*2017-09-30*

#### 新特性
- 综合
  - 新增 `theme-chalk` 主题
  - 增强以下组件的可访问性：Alert、AutoComplete、Breadcrumb、Button、Checkbox、Collapse、Input、InputNumber、Menu、Progress、Radio、Rate、Slider、Switch 和 Upload
  - 新增布局组件 Container、Header、Aside、Main 和 Footer
- Button
  - 新增 `round` 属性，用于圆角按钮 #6643
- TimeSelect
  - 可以用 `Up`、`Down` 导航，用 `Enter` 选中时间 #6023
- TimePicker
  - 可以用方向键导航，用 `Enter` 选中时间 #6050
  - 新增 `start-placeholder` 和 `end-placeholder`，用于设置范围选择时两个输入框的占位符 #7169
- Tree
  - 子节点在首次被展开之前不进行渲染 #6257
  - 新增 `check-descendants` 属性，设置 `lazy` 模式下勾选节点时，是否完全展开整个子树 #6235
- Tag
  - 新增 `size` 属性 #7203
- Datepicker
  - type 为 `datetimerange` 时可以使用 `timeFormat` 格式化时间选择器 #6052
  - 新增 `start-placeholder` 和 `end-placeholder`，用于设置范围选择时两个输入框的占位符 #7169
- MessageBox
  - 新增 `closeOnHashChange` 属性 #6043
  - 新增 `center` 属性，提供居中布局 #7029
  - 新增 `roundButton` 属性，使得内部按钮为圆角按钮 #7029
  - 新增 `dangerouslyUseHTMLString` 属性，使得 `message` 支持传入 HTML 字符串<sup>*</sup> #6043
- Dialog
  - 新增 `width`、`fullscreen`、`append-to-body` 属性，支持嵌套使用
  - 新增 `center` 属性，提供居中布局 #7042
  - 新增 `focus-after-closed`、`focus-after-open`属性，支持无障碍访问 #6511
- ColorPicker
  - 增加手动输入色值的支持 #6167
  - 新增 `size` 属性，用于控制组件的大小 #7026
  - 新增 `disabled` 属性，用于禁用组件 #7026
- Message
  - 图标部分使用 icon 代替图片，从而支持通过 CSS 修改图标背景色 #6207
  - 新增 `dangerouslyUseHTMLString` 属性，使得 `message` 属性支持传入 HTML 字符串<sup>*</sup> #6207
  - 新增 `center` 属性，提供居中布局 #6875
- Notification
  - 新增 `position` 属性，用于配置 Notification 出现的位置 #6231
  - 新增 `dangerouslyUseHTMLString` 属性，使得 `message` 属性支持传入 HTML 字符串<sup>*</sup> #6231
  - 新增 `showClose` 属性，用于隐藏关闭按钮 #6402
- Rate
  - 新增 `show-score` 属性，控制是否在右侧显示当前分数 #6295
- Tabs
  - 新增 `tab-position` 属性，控制选项面板内容显示的上、下、左、右四个方向 #6096
- Radio
  - 增加 `border` 属性和 `size` 属性 #6690
- Checkbox
  - 增加 `border` 属性和 `size` 属性 #6690
- Alert
  - 新增 `center` 属性，提供居中布局 #6876
- Menu
  - 新增 `background-color`、`text-color` 和 `active-text-color` 属性，分别用于设置菜单的背景色、菜单的文字颜色和当前激活菜单的文字颜色 #7064
- Form
  - 新增 `inline-message` 属性，设置后校验信息会以行内样式显示 #7032
  - 新增 `status-icon` 属性，用于在输入框中显示校验结果反馈图标 #7032
- Input
  - 新增 `suffix`、`prefix` 的 slot，以及 `suffixIcon`、`prefixIcon` 属性，用于给输入框内部增加前置和后置内容 #7032
- Breadcrumb
  - 新增 `separator-class` 属性，可使用图标作为分隔符 #7203
- Steps
  - 新增 `simple` 属性，用于开启简洁风格的步骤条 #7274
- Pagination
  - 新增 `prev-text` 和 `next-text` 属性，用于自定义上一页和下一页的文本 #7005

#### 修复
- DatePicker
  - 选择周数时，`v-model` 结果返回该周第二天的问题 #6038
  - 在 `daterange` 类型中，第一次的输入会被清空的问题 #6021
- DateTimePicker
  - 和 TimePicker 相互影响的问题 #6090
  - 选择时间小时和秒可超出限制的问题 #6076
- TimePicker
  - 失去焦点时无法正确改变 `v-model` 值的问题 #6023
- Dialog
  - 当含有下拉框时，下拉框的打开和关闭会造成文字虚晃的问题 #6088
- Select
  - 提升性能，修复组件销毁时可能导致 Vue dev-tool 卡死的问题 #6151

#### 非兼容性更新
- 综合
  - 移除 `theme-default`
  - 表单组件的 `change` 事件和 Pagination 的 `current-change` 事件现在仅响应用户交互
  - Button 和表单组件的 `size` 属性不再接受 `large` 值，可接受 `medium`、`small` 和 `mini`
  - 为了方便使用第三方图标，Button 的 `icon` 属性、Input 的 `prefix-icon` 和 `suffix-icon` 属性、Steps 的 `icon` 属性现在需要传入完整的图标类名
- Dialog
  - 移除 `size` 属性。现在 Dialog 的尺寸由 `width` 和 `fullscreen` 控制
  - 移除通过 `v-model` 控制 Dialog 显示和隐藏的功能
- Rate
  - `text-template` 属性更名为 `score-template`
- Dropdown
  - `menu-align` 属性变更为 `placement`，增加更多方位属性
- Transfer
  - `footer-format` 属性更名为 `format`
- Switch
  - `on-text` 和 `off-text` 属性不再有默认值
- Tag
  - `type` 属性现在支持 `success`、`info`、`warning` 和 `danger` 四个值
  - `close-transition` 属性更名为 `disable-transitions`
- Menu
  - 移除 `theme` 属性。现在通过 `background-color`、`text-color` 和 `active-text-color` 属性进行颜色的自定义
- Input
  - 移除 `icon` 属性。现在通过 `suffix-icon` 属性或者 `suffix` 具名 slot 来加入尾部图标
  - 移除 `on-icon-click` 属性和 `click` 事件。现在如果需要为输入框中的图标添加点击事件，请以具名 slot 的方式添加图标
- Autocomplete
  - 移除 `icon` 和 `on-icon-click` 属性。现在通过 `prefix` 和 `suffix` 具名 slot 来加入图标
  - 移除 `custom-item` 属性。现在通过 `scoped slot` 自定义输入建议列表项的内容
- Table
  - 移除通过 `inline-template` 自定义列模板的功能
- Steps
  - 移除 `center` 属性
  - 现在步骤条将默认充满父容器

##
<i><sup>*</sup> 在网站上动态渲染任意 HTML 是非常危险的，因为容易导致 [XSS 攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。因此请在 `dangerouslyUseHTMLString` 打开的情况下，确保 `message` 的内容是可信的，**永远不要**将用户提交的内容赋值给 `message` 属性。</i>