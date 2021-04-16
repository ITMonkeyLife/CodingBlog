---
title: iOS 奇淫技巧
tags: OC
category: 2021-04
renderNumberedHeading: true
grammar_cjkRuby: true
---

- 在携程首页存在很多其他的BU，这时候遇到一个莫名其妙的接口报错信息，显示一个接口报错弹窗。这种情况如何快速定位到问题？



- view的UIButton按钮点击无响应(按钮的位置在父视图之外的解决方法),传递响应链

这里有两个方法，每次有touch动作时，都会走这两个方法
```objc
- (UIView *)hitTest:(CGPoint)point withEvent:(UIEvent *)event；
- (BOOL)pointInside:(CGPoint)point withEvent:(UIEvent *)event；
```
重写方法```objc - (UIView *)hitTest:(CGPoint)point withEvent:(UIEvent *)event```

首先调用当前视图的pointInside:withEvent:方法判断触摸点是否在当前视图内；
若返回NO,则hitTest:withEvent:返回nil;
若返回YES,则向当前视图的所有子视图(subviews)发送hitTest:withEvent:消息，所有子视图的遍历顺序是从top到bottom，即从subviews数组的末尾向前遍历,直到有子视图返回非空对象或者全部子视图遍历完毕；
若第一次有子视图返回非空对象,则hitTest:withEvent:方法返回此对象，处理结束；
如所有子视图都返回非，则hitTest:withEvent:方法返回自身(self)。
最后，这个触摸事件交给主窗口的hitTest:withEvent:方法返回的视图对象去处理。




- iOS 自己定义的类，如何通知使用方移除掉代码？
 在终端中输入```grep -r UIWebView .```查找
 
API_DEPRECATED

iOS开发高级Debug技巧

