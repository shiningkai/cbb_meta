# Sieyuan可视化CBB规范-统一元数据模型(CBB-Meta)

## 概述
> 通过建立统一元数据模型CBB-Meta和跨端模块库CBB-Core将常用业务功能的封装,达到模块共用和资源共享的目的。结合配置工具链CBB-Chain,实现"数据建模-模块库开发-跨端应用"一体化

> <font color="red">***Todo:***</font>
相关模块需各专业负责人进一步完善

## 标签定义
### 根标签定义

```xml
<?xml version="1.0" encoding="utf-8" ?>
```

### Application
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


### Metadata
> 元数据定义是对常量、变量、结构体的描述
```xml
<Metadata>
    <!-- 常量 -->
    <Const type="string" name="NoLogin">未登录</Const>
    <!-- 变量 -->
    <Var type="string" name="userName">未知用户</Var>
    <!-- 结构体 -->
    <Struct name="CommonRow">
        <Var type="integer" name="id" />
        <Var type="string" name="guid" />
        <Var type="string" name="name" />
    </Struct>
    <!-- 枚举 -->
    <Enum name="LOCAL">
        <Const type="integer" value="0">zh-CN</Const>
        <Const type="integer" value="1">en-US</Const>
    </Enum>
</Metadata>
```


***数据类型***
|No|Meta|C++|TypeScript|
|:-:|:-|:-|:-|
|1|Integer|Integer|Number|
|2|Float|Float|Number|
|3|String|String|String|
|4|Boolean|Boolean|Boolean|
|5|Vector|Vector|T[]|
|6|Tuple|Tuple|[T1, T2]|
|7|Struct|Struct|Interface|
|8|Enum|Enum|Enum|



### <font color="yellow">Containers</font>
> 布局容器是对页面布局的描述，支持嵌套

```xml
<Containers>
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
|3|dividerDraggable|分隔线是否可拖动|false|

#### <font color="yellow">RowContainer : Container</font>

***属性定义***
|序号|属性|说明|示例|
|:-:|:-|:-|:-|
|1|spacing|间距|5px|
|2|direction|子项排列方向|默认positive左右,reverse右左|
|3|dividerDraggable|分隔线是否可拖动|false|

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
> 组件定义是对组件的描述，支持基础组件和自定义组件。每个组件的信号Signal与槽Slot定义在组件内，对外需提供说明。

```xml
<Components>
    <!-- 原子组件，这里只是示范，不需要定义 -->
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
    <!-- 主题 -->
    <Theme name="light">
        <ColorPalette primary="#2C3E50" secondary="#3498DB"/>
    </Theme>
    <!-- 原子样式 -->
    <AtomicStyles>
        <BorderClass name="border" color="primary"/>
    </AtomicStyles>
</Styles>
```
> <font color="red">***Todo:***</font>
列出主题Theme的和原子样式AtomicStyles的子标签及属性

### <font color="yellow">Behaviors</font>
> 交互行为定义是对信号与槽的连接关系的描述

```xml
<Behaviors>
</Behaviors>
```

## 完整示例

### 智慧变频电源试验系统

```xml
<?xml version="1.0" encoding="utf-8" xmlns:MNT="app.monitor" xmlns:HIS="app.history"?>

<Metadata>
    <Const type="string" name="title">VF-3串谐试验装置</Const>
    <Const type="string" name="description">D03-01-智慧变频电源试验系统</Const>
    <Var type="integer" name="ratio">1</Var>
    <Struct name="Station">
        <Var type="integer" name="id" />
        <Var type="string" name="guid" />
        <Var type="string" name="name" />
    </Struct>
    <Enum name="LOCAL">
        <Const type="integer" value="0">zh-CN</Const>
        <Const type="integer" value="1">en-US</Const>
    </Enum>
    <Vector type="Station" name="stations"></Vector>
</Metadata>

<Application
    version="1.0"
    locale="zh-CN"
    title="VF-3串谐试验装置"
    description="D03-01-智慧变频电源试验系统"
    icon="vf3.ico"
    theme="light"
>
    <RowContainer>
        <Header />
        <Navigation type="horizontal"/>
        <Breadcrumb />
        <Views />
        <SieyuanFooter />
    </RowContainer>
</Application>

<View route="app/monitor">
    <ColumnContainer id="cc" margin="10px">
        <MNT:PRPS dataBinding=""/>
    </ColumnContainer>
</View>

<Components>
    <!-- 可视化类 -->
    <Header path="Components/layout/Header_v1.0"/>
    <Footer path="Components/layout/Footer_v1.0"/>
    <MNT:PRPS path="Components/chart/PRPS_GL_v1.0"/>
    <HIS:PRPS path="Components/chart/PRPS_GL_v1.2"/>
    <SieyuanFooter>
        <Container:RowContainer alignHorizontal="center" height="80px" margin="20px">
            <Image src="images/logo/sieyuan.svg"/>
            <Label>思源电气</Label>
        </RowContainer>
    </SieyuanFooter>
    <RatioDialog id="dlg1" title="设置励磁变比" icon="dlg1.ico" width="640px" height="480px">
        <ColumnContainer>
            <Container>
                <Label>请输入励磁变比</Label>
                <IntegerBox id="ratio1" meta="ratio" min="1" max="9"><IntegerBox>
            </Container>
            <Container>
                <Confirm id="confirm1" yesText="确定" noText="取消"/>
            </Container>
        </ColumnContainer>
    </RatioDialog>
    <!-- 数据类 -->
</Components>

<Behaviors>
    <Connection sender="cc" signal="init" receive="dlg1" slot="show" />
</Behaviors>
```
