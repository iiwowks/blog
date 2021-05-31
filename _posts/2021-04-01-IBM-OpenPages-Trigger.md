---
layout: post
title: "IBM OpenPages Trigger"
date: 2021-03-20
category: Java
author: iiwowks
published: true
photoswipe: true
syntaxhighlight: true
---

# IBM OpenPages Trigger

The first project work in ctc for the mufg user

- [Trigger Develope Guide](https://public.dhe.ibm.com/software/data/cognos/documentation/openpages/en/8.2.0/Trigger_Developer_Guide.pdf)
- [Openpages API javadoc](https://public.dhe.ibm.com/software/data/cognos/documentation/openpages/en/8.2.0.2/javadoc/index.html)

## 简介：

IBM OpenPages GRC Trigger 框架提供一些构架实现来帮助定制自定义业务逻辑和规则。使用 Java 创建，可以实现现有的业务逻辑基于现有的 Openpages GRC API。当一个用户实行一个 action 时，被调用，这些业务逻辑可以自动化实现。

熟悉 openpages GRC API

![图片 3](https://i.imgur.com/rtwnKMz.png)

## 定义：

一个 trigger 可以在执行一个操作的前面或者后面执行。

通常包含两个部分：

1. 一个规则：在需要执行的操作和参数的一个规则

a) 被执行的操作

b) Object 的类型

c) 在上下文中 object 属性的条件

2. 一个或者多个事件处理器，如果当前操作满足在 trigger 中的定义规则，它将会被执行。可以实现任何业务逻辑：

a) 丢出一个异常

b) 创建一个新的 object

c) 删除一个 object

d) 重置或修改 object 的属性

e) 执行 report 或者 program

f) Kick off 一个工作流

高级特性：

trigger 有以下一些特性：

1. 只针对特定的平台操作

2. 必须使用 java 编写

## GRC Trigger FrameWork

这个框架负责处理 custom code 加载 class 文件，当 OpenPages 启动的时候，有关 triggers 的定义是使用 xml 配置的，在系统启动的时候也会被加载。xml 配置文件会提供需要调用的全称类路径和必要的属性和参数。

在 xml 配置文件中需要确定 custom classes 类全称路径，将类文件添加到类路径的方法：

**位置：**

在一个操作的前后，PRE 和 POST 两个阶段，triggers 将会注册到并监听其中的一个阶段。

**事务**

任何 trigger 中的错误，会导致业务回滚

## 流图：

trigger manager 是一个 GRC Trigger 框架创建的组件，将 API 操作转换为事件，检测注册了的 trigger，调用其中的方法。其中调用的结果将作为平台的自动业务逻辑结果。

## 配置 trigger：

可以通过 xml 配置 trigger， xml 文件作为一个资源对象存储在 OpenPages 仓库中作为一个系统文件。

其中一个叫 `_trigger_config.xml` 的配置文件

在 xxxxx 路径下存储 trigger 配置文件。

添加一个文件到 trigger 配置仓库 ：

加载一个 xml 配置文件，需要将文件名添加到 registry setting 中，步骤：

配置文件将会被顺序加载，在系统启动的时候。

可通过 Trigger Configuration Refresh Utility 重新加载 xml 配置文件。

对 jar 包的更新和配置更新，需要服务器重启才可以生效

定义一个新的规则， 添加`<grcTrigger>`标签 `<rule> `多个`<eventHandler>`, `<attribute>`

xml 配置文件的基本格式：

定义了 rule 和 event handler。

通过`<grcTrigger>`标签和`<rule>`，`<eventHandler>`标签

`<attribute>`标签是用来，在 rule 和 event handler 处理类之中 传配置参数的

## GRCTrigger 属性：

`<grcTrigger>`标签属性 需要定义 trigger 并且包含的 rule 和 event handler

## rule 属性

`<rule>`标签配置将会使用哪个类

attribute 用来配置 rule 的行为

rule Attribute

使用键值对配置这些属性

**事件处理属性**

## 支持的事件：

以下的一些操作是支持的，针对每个事件的方法 可以参照 api 文档

1. Create Object

2. Update Object

3. Associate Objects

4. Disassociate Object

5. Delete Objects

6. Copy Object

7. Search Objects

## 配置事件处理器去顺序执行

避免多个 trigger 并行更新，

使用一个 mechanism configuration 来强制 trigger 顺序化执行。 步骤：

1. 在 OpenPages 仓库中找到*trigger_config*.xml 文件

2. 定位到需要顺序执行的 trigger 定义的位置

3. 定位到`<eventHandler>`标签

## 实现一个 Rule

每一个注册了的 trigger 必须有一个定义了的 rule，每一个 rule 是一个 java class 文件，都继承自 DefaultRule。这个 rule 确定这个事件是否应用到 trigger 的业务逻辑中。如果不匹配，这个事件将传递给下一个 trigger，如果 rule 还不匹配，将会交付给系统处理。

实现一个 rule, 必须继承 com.ibm.openpages.api.trigger.ext.DefaultRule

针对所有的 event type，默认的 rule 返回 false。

重写 关联到这个 trigger rule 的事件的特定的方法 isApplicable()

## 实现一个 Event Handler

一旦一个 rule 对一个事件返回一个 positive 值，其他定义在同一个 trigger 中的其他 event handler 将会处理这些事件。

event handler 必须继承 com.ibm.openpages.api.trigger.ext.DefaultEventHandler

# Out-of-the-Box Rules

Content Type Match Rule

**Syntax:** com.ibm.openpages.api.trigger.oob.ContentTypeMatchRule

**Description:** This rule checks if the object type of the operating object matches the specific value.

**Usage:** This rule can be used in the following events:

create.object

update.object

delete.objects

associate.objects

disassociate.objects

copy.object

copy.objects

这个 rule 用来在 PRE 和 POST 两个位置执行，只有在 delete.object 事件前面必须执行

Detect Property Change Rule

Fields Match Rule

This rule checks if values of the operating object match specific values.

# Out-of-the-box Handlers

Date Validation Handler

Send Email Event Handler

Set Current Date Handler

Set Enum Field Handler

**Trigger Events**

事件对象代表一个操作的所有信息，将会被 rules 检查适不适合，以及使用 event handler 来处理特定的业务逻辑。每一个事件类型是 com.ibm.openpages.api.trigger.events 包下的，继承自 com.ibm.openpages.api.trigger.events.AbstractEvent

TriggerEventType 枚举定义了所有可能的 event

一个事件类必须提供 TriggerEventType TriggerPositionType 和 Context

## 失效 Triggers

## Error Handling

允许自定义错误信息

在事件处理器中加上：

throwException(“com.openpages.xxx.trigger.missing.unique.property”,

params,

null,

event.getContext());

## 配置 triggers 的生命周期

一个生命周期 trigger 定义 objects 的工作 生命周期

Lifecycle trigger 的结构：

针对一个 lifecycle trigger 是没有必要确定 event handler 和 position，有默认的 rule 和 event handler

• event=”create.object” position=”pre”

• event=”create.object” position=”post”

• event=”update.object” position=”pre”

• event=”update.object” position=”post”

event=”create.objcet” position=”pre” 控制事件以及位置组合

Lifecycle trigger Properties

Lifecycle trigger Email Properties

Lifecycle trigger transition element and Properties

## Lifecycle trigger 条件元素和属性

使用条件元素检查每个变更。只能有一个条件元素添加到所有变更和默认配置中，

使用标签`<condition> </condition>`包裹

## 样例工程

GRC API 包含一些 demo 代码用于验证 trigger rules 和 event handlers, 编译 sample，打包。

样例 trigger 代码包括：

1. ContentTypeMathTrigger: 校验 GRC Object 的类型定义。

2. FolderMatchTrigger: 校验 GRC Object 路径

3. FieldsMatchTrigger: 继承自 FolderMatchTrigger，可以校验一个或多个 filed 值

4. DetectPropertyChangeTrigger: 校验一个 field 值改动

5. DateValidationAction: 事件处理器，检验日期格式

6. SetCurrentDateAction: 设置一个 Date Filed 子啊

7. SetEnumFieldAction:

## Legacy Out-of-the-Box Rules

Abstract Resoure Trigger

实现调用资源对象操作，

Folder Match Trigger

检测是否对象注册在特定的文件夹下

Detect Property Change Trigger

检测一些 fileds 定义在配置之中的是否改变

Content Type Match Trigger

检测是否是特定的类型

## Lagacy Out-of-the-Box Actions

- Abstract Resource Trigger Action
- Abstract Change Control Trigger Action
- Change Control Flag Trigger Action
- Abstract Exchange Rate As Of Date Trigger Action
- Abstract Picklist Dependency Trigger Action
- Picklist Value Mapping trigger action
- Abstract Resource Based Send Email Action
- Defalut Sent Email To User In Field Action
- Send Email To User In Field Action
- Set Field Value From Another Field Action
- Set Field Value From Parent Action
- Abstract Resource Copy Trigger Action

最佳实践：

1. Trigger 只是作为 openpages 的一部分运行，确定使用 trigger 可以实现的目标

2. 在执行方法前使用 trigger(PRE)

3. 在执行方法之后使用 Trigger(POST)

# 示例工程：

ContentTypeMatchRule

```
FieldsMatchRule
```

Bulk Update

Approve

Reject

```
Id startProcessesInBulk(StartProcessesOptions wfOptions)
```

## 开发

看源码发现了突破口：

```java
    public void processTransition(Id processId, String transitionName, IWFTransitionOptions options) throws Exception {
        // transition的上下文context是新创建的
        WFTransitionContext context = new WFTransitionContext(this.token, this, this.getProcess(processId), transitionName, options, false);
        // 通过上下文获取process
        IWFProcess proc = context.getProcess();
        // 通过上下文获得process 的定义
        IWFProcessDefinition procDef = context.getProcessDefinition();
        // 通过上下文获得activity实体
        IWFActivityInstance activityInstance = context.getActivityInstance();
        // 通过实体的id获得定义中的activity
        IWFActivity activity = procDef.getActivity(activityInstance.getActivityId());

        IWFTransition transition = null;
        // process的状态不能在executing
        if (proc.getState() == WFProcessState.executing) {
            throw new WFServiceException(-8539, Arrays.asList(processId.toString(), transitionName, activity.getName()), (Throwable)null);
        }
        // process 的状态必须在open
        else if (proc.getState() != WFProcessState.open) {
            throw new WFServiceException(-8538, Arrays.asList(processId.toString(), transitionName, activity.getName()), (Throwable)null);
        }
        //
        else {
            // 在定义中的activity之中通过transition名字获取transition对象
            transition = activity.getTransition(transitionName);
            // 判断transition对象是否可以处理
            if (!activityInstance.getCanProcessTransition()) {
                throw new WFServiceException(-8549, Arrays.asList(this.token.getName(), transitionName), (Throwable)null);
            }
            else {
                // 重要： 这里设置了process的状态
                this.setProcessState(processId, WFProcessState.executing);
                // 如果在定义中设置了在后台执行：
                if (transition.isBackground()) {
                    this.launchTransitionProcess(transitionName, context, procDef);
                }
                // 不在后台执行
                else {
                    this.processTransition(context);
                }

            }
        }
    }
```
