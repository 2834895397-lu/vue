# 弹框

###### 有时候我们在弹框中获取的是id, 而我们又需要显示的是名称, 这个名称又在其他表里面

> 这时候我们可以在配置报表的时候进行联表查询操作, 通过条件把弹框所需要用到的信息查询出来:
>
> ![image-20201109165434881](img/image-20201109165434881.png)



> ###### 选择弹框之后, 表单要显示的是名称, 而要存的是id, 却显示的是id
>
> 可以通过配置一个下拉框组件或者其他组件来关联表显示其名称:
>
> ![image-20201109170030872](img/image-20201109170030872.png)



---



# 字典的翻译



## input页面下拉框使用[#](https://www.cnblogs.com/wjw1014/p/12242203.html#input页面下拉框使用)

**效果展示**
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219154432619.png)](https://img-blog.csdnimg.cn/20191219154432619.png)
**实现**

1. 定义数据字典
   [![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219154524311.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)](https://img-blog.csdnimg.cn/20191219154524311.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)
2. 引用并调用JDictSelectTag组件

```javascript
import JDictSelectTag from '@/components/dict/JDictSelectTag.vue'
export default {
 	....
     components: {
       JDate,
       CustomerModal,
       JDictSelectTag
     },
     ...
}
<j-dict-select-tag :triggerChange="true" v-model="queryParam.type1Id" placeholder="请选择类型" dictCode="customer_type"/>
```

dictCode为数据字典中定义的code。

## list页面显示 数据字典[#](https://www.cnblogs.com/wjw1014/p/12242203.html#list页面显示-数据字典)

**效果展示**
处理前
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219154729217.png)](https://img-blog.csdnimg.cn/20191219154729217.png)
处理后
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219154748123.png)](https://img-blog.csdnimg.cn/20191219154748123.png)
**实现**

1. 实体类添加注解

```java
@Dict(dicCode = "customer_type")
private String type1Id;
```

dicCode为数据字典中定义的code。
\2. 修改table column定义

```javascript
{
  title:'类型',
   align:"center",
   dataIndex: 'type1Id_dictText',
 },
```

dataIndex值为字段名+"_dictText"
修改后也可以在vue中查看数据源。
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219154956775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)](https://img-blog.csdnimg.cn/20191219154956775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)

## list页面显示 表关联[#](https://www.cnblogs.com/wjw1014/p/12242203.html#list页面显示-表关联)

**效果展示**
处理前
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219155038727.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)](https://img-blog.csdnimg.cn/20191219155038727.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)
处理后
[![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121915505565.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)](https://img-blog.csdnimg.cn/2019121915505565.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc3NjExMQ==,size_16,color_FFFFFF,t_70)
**实现**

1. 实体类添加注解

```java
@Dict(dicCode = "id",dictTable = "sys_user",dicText = "realname")
private String managerId;
dicCode为关联表的组件
dictTable为关联表
dicText 为需要显示的内容
```

1. 修改table column定义

```javascript
{
  title:'负责人',
   align:"center",
   dataIndex: 'managerId_dictText'
 },
```

dataIndex值为字段名+"_dictText",和数据字典的一致。

---





