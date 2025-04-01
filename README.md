# Sieyuan可视化CBB规范-统一元数据模型(CBB-Meta)

## 概述
> 通过建立统一元数据模型CBB-Meta和跨端模块库CBB-Core将常用业务功能的封装,达到模块共用和资源共享的目的。结合配置工具链CBB-Chain,实现"数据建模-模块库开发-跨端应用"一体化

> <font color="red">***Todo:***</font>
相关模块需各专业负责人进一步完善

## 根标签定义

```xml
<?xml version="1.0" encoding="utf-8" ?>
```

## Application
> 应用标签是对应用程序的描述

```xml
<Application
    version="1.0"
    locale="zh-CN"
    title="VF-3串谐试验装置"
    description="D03-01-智慧变频电源试验系统"
    icon="vf3.ico"
    theme="light"
>
    <Metadata></Metadata>
    <Containers></Containers>
    <Components></Components>
    <Styles></Styles>
    <Behaviors></Behaviors>
</Application>
```

***属性定义***
|序号|属性|说明|示例|
|:-:|:-|:-|:-|
|1|version|版本||
|2|locale|语言||
|3|title|标题||
|4|description|描述||
|5|icon|图标||
|6|theme|主题||

***子标签定义***
|序号|标签|说明|示例|
|:-:|:-|:-|:-|
|1|Metadata|元数据||
|2|Containers|布局容器||
|3|Components|组件||
|4|Styles|主题样式||
|5|Behaviors|交互行为||


### Metadata
> 元数据定义是对结构体、常量、变量、信号与槽的描述

```xml
<Class name="DataProcessor">
    <Signals>
        <Signal name="processing" version="1.2" deprecated="true"/>
        <Signal name="update">
            <Param type="struct" name="data">
                <Param type="string" name="name">
                <Param type="number" name="type">
            </Param>
            <Param type="number" name="timestamp"/>
        </Signal>
    </Signals>
    <Slots>
        <Slot name="processing">
            <Param type="string" name="path"/>
        </Slot>
        <Slot name="save" returnType="bool">
            <Param type="struct" name="data"/>
        </Slot>
    </Slots>
</Class>
```


### <font color="yellow">Containers</font>
> 布局容器是对页面布局的描述，支持嵌套

```xml
<Containers>
    <ColumnContainer>
    </ColumnContainer>
    <RowContainer>
    </RowContainer>
    <GridContainer>
    </GridContainer>
</Containers>
```

#### <font color="yellow">Container</font>

***属性定义***
|序号|属性|说明|示例|
|:-:|:-|:-|:-|
|1|width|宽度|1280px 50%|
|2|height|高度|720px 50%|
|3|minWidth|最小宽度||
|4|minHeight|最小高度||
|5|maxWidth|最大宽度||
|6|maxHeight|最大高度||
|7|margin|四周边距|10px|
|8|marginLeft|左边距|10px|
|9|marginTop|上边距|10px|
|10|marginRight|右边距|10px|
|11|marginBottom|底边距|10px|
|12|alignHorizontal|水平对齐|left center right|
|13|alignVertical|垂直对齐|top middle bottom|


#### <font color="yellow">ColumnContainer : Container</font>

***属性定义***
|序号|属性|说明|示例|
|:-:|:-|:-|:-|
|1|spacing|间距|5px|
|2|direction|子项排列方向|默认positive上下,reverse下上|

#### <font color="yellow">RowContainer : Container</font>

***属性定义***
|序号|属性|说明|示例|
|:-:|:-|:-|:-|
|1|spacing|间距|5px|
|2|direction|子项排列方向|默认positive左右,reverse右左|

#### <font color="yellow">GridContainer : Container</font>

***属性定义***
|序号|属性|说明|示例|
|:-:|:-|:-|:-|
|1|rows|最大行数||
|2|columns|最大列数||
|3|flow|换行策略|horizontal水平填充后换行,vertical垂直填充后换行|
|4|rowSpacing|行间距|5px|
|5|columnSpacing|列间距|5px|


### <font color="yellow">Components</font>
> 组件定义是对组件的描述，支持基础组件和自定义组件

```xml
<Components>
    <Breadcrumb name="面包屑" />
    <Label name="标签" />
    <Spring name="弹簧" />
    <Table name="表格" />
    <Tabs name="标签页" />
</Components>
<Components namespace="layout">
    <Header name="头" path="Components/layout/Header_v1.0"/>
    <Navigation name="导航" type="horizontal"/>
    <Footer name="脚" path="Components/layout/Footer_v1.0"/>
</Components>
<Components namespace="about">
    <Footer name="脚" custom="true">
        <RowContainer alignHorizontal="center" margin="20px">
            <Image src="images/logo/sieyuan.svg"/>
            <Label>思源电气</Label>
        </RowContainer>
    </Footer>
</Components>
<Components namespace="chart">
    <PRPS path="Components/chart/PRPS_GL_v1.0"/>
</Components>
```
> <font color="red">***Todo:***</font>
列出每种组件的属性，同名组件通过命名空间区分


### <font color="yellow">Styles</font>
> 样式定义是对主题Theme的描述，原子样式AtomicStyles可以被复用

```xml
<Styles>
    <Theme name="light">
        <ColorPalette primary="#2C3E50" secondary="#3498DB"/>
        <Typography baseSize="16px" ratio="1.333"/>
    </Theme>
    <AtomicStyles>
        <SpacingClass name="m-1" value="8px"/>
        <ShadowClass name="elevation-2" value="0 2px 4px #336699"/>
    </AtomicStyles>
</Styles>
```
> <font color="red">***Todo:***</font>
列出主题Theme的和原子样式AtomicStyles的子标签及属性

### <font color="yellow">Behaviors</font>
> 交互行为定义是对信号与槽的连接关系的描述

```xml
<Class name="DataProcessor">

</Class>
```



