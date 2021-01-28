## 事件句柄　(Event Handlers)

HTML 4.0 的新特性之一是能够使 HTML 事件触发浏览器中的行为，比如当用户点击某个 HTML 元素时启动一段  JavaScript。下面是一个属性列表，可将之插入 HTML 标签以定义事件的行为。

| 属性                                 | 此事件发生在何时...                  |
| ------------------------------------ | ------------------------------------ |
| [onabort](event_onabort.asp)         | 图像的加载被中断。                   |
| [onblur](event_onblur.asp)           | 元素失去焦点。                       |
| [onchange](event_onchange.asp)       | 域的内容被改变。                     |
| [onclick](event_onclick.asp)         | 当用户点击某个对象时调用的事件句柄。 |
| [ondblclick](event_ondblclick.asp)   | 当用户双击某个对象时调用的事件句柄。 |
| [onerror](event_onerror.asp)         | 在加载文档或图像时发生错误。         |
| [onfocus](event_onfocus.asp)         | 元素获得焦点。                       |
| [onkeydown](event_onkeydown.asp)     | 某个键盘按键被按下。                 |
| [onkeypress](event_onkeypress.asp)   | 某个键盘按键被按下并松开。           |
| [onkeyup](event_onkeyup.asp)         | 某个键盘按键被松开。                 |
| [onload](event_onload.asp)           | 一张页面或一幅图像完成加载。         |
| [onmousedown](event_onmousedown.asp) | 鼠标按钮被按下。                     |
| [onmousemove](event_onmousemove.asp) | 鼠标被移动。                         |
| [onmouseout](event_onmouseout.asp)   | 鼠标从某元素移开。                   |
| [onmouseover](event_onmouseover.asp) | 鼠标移到某元素之上。                 |
| [onmouseup](event_onmouseup.asp)     | 鼠标按键被松开。                     |
| [onreset](event_onreset.asp)         | 重置按钮被点击。                     |
| [onresize](event_onresize.asp)       | 窗口或框架被重新调整大小。           |
| [onselect](event_onselect.asp)       | 文本被选中。                         |
| [onsubmit](event_onsubmit.asp)       | 确认按钮被点击。                     |
| [onunload](event_onunload.asp)       | 用户退出页面。                       |

## 鼠标 / 键盘属性

| 属性                                     | 描述                                         |
| ---------------------------------------- | -------------------------------------------- |
| [altKey](event_altkey.asp)               | 返回当事件被触发时，"ALT" 是否被按下。       |
| [button](event_button.asp)               | 返回当事件被触发时，哪个鼠标按钮被点击。     |
| [clientX](event_clientx.asp)             | 返回当事件被触发时，鼠标指针的水平坐标。     |
| [clientY](event_clienty.asp)             | 返回当事件被触发时，鼠标指针的垂直坐标。     |
| [ctrlKey](event_ctrlkey.asp)             | 返回当事件被触发时，"CTRL" 键是否被按下。    |
| [metaKey](event_metakey.asp)             | 返回当事件被触发时，"meta" 键是否被按下。    |
| [relatedTarget](event_relatedtarget.asp) | 返回与事件的目标节点相关的节点。             |
| [screenX](event_screenx.asp)             | 返回当某个事件被触发时，鼠标指针的水平坐标。 |
| [screenY](event_screeny.asp)             | 返回当某个事件被触发时，鼠标指针的垂直坐标。 |
| [shiftKey](event_shiftkey.asp)           | 返回当事件被触发时，"SHIFT" 键是否被按下。   |

## IE 属性

除了上面的鼠标/事件属性，IE 浏览器还支持下面的属性：

| 属性            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| cancelBubble    | 如果事件句柄想阻止事件传播到包容对象，必须把该属性设为 true。 |
| fromElement     | 对于 mouseover 和 mouseout 事件，fromElement 引用移出鼠标的元素。 |
| keyCode         | 对于 keypress 事件，该属性声明了被敲击的键生成的 Unicode 字符码。对于 keydown 和 keyup  事件，它指定了被敲击的键的虚拟键盘码。虚拟键盘码可能和使用的键盘的布局相关。 |
| offsetX,offsetY | 发生事件的地点在事件源元素的坐标系统中的 x 坐标和 y 坐标。   |
| returnValue     | 如果设置了该属性，它的值比事件句柄的返回值优先级高。把这个属性设置为 fasle，可以取消发生事件的源元素的默认动作。 |
| srcElement      | 对于生成事件的 Window 对象、Document 对象或 Element 对象的引用。 |
| toElement       | 对于 mouseover 和 mouseout 事件，该属性引用移入鼠标的元素。  |
| x,y             | 事件发生的位置的 x 坐标和 y 坐标，它们相对于用CSS动态定位的最内层包容元素。 |

## 标准 Event 属性

下面列出了 2 级 DOM 事件标准定义的属性。

| 属性                                     | 描述                                           |
| ---------------------------------------- | ---------------------------------------------- |
| [bubbles](event_bubbles.asp)             | 返回布尔值，指示事件是否是起泡事件类型。       |
| [cancelable](event_cancelable.asp)       | 返回布尔值，指示事件是否可拥可取消的默认动作。 |
| [currentTarget](event_currenttarget.asp) | 返回其事件监听器触发该事件的元素。             |
| [eventPhase](event_eventphase.asp)       | 返回事件传播的当前阶段。                       |
| [target](event_target.asp)               | 返回触发此事件的元素（事件的目标节点）。       |
| [timeStamp](event_timestamp.asp)         | 返回事件生成的日期和时间。                     |
| [type](event_type.asp)                   | 返回当前 Event 对象表示的事件的名称。          |

## 标准 Event 方法

下面列出了 2 级 DOM 事件标准定义的方法。IE 的事件模型不支持这些方法：

| 方法                                           | 描述                                     |
| ---------------------------------------------- | ---------------------------------------- |
| [initEvent()](event_initevent.asp)             | 初始化新创建的 Event 对象的属性。        |
| [preventDefault()](event_preventdefault.asp)   | 通知浏览器不要执行与事件关联的默认动作。 |
| [stopPropagation()](event_stoppropagation.asp) | 不再派发事件。                           |