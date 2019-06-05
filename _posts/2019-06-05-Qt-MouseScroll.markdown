---
title: "Qt Mouse Scroll"
layout: post
date: 2019-06-05 12:34
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Qt
- MouseEvent
category: blog
author: zuewang
description: 
---

# Qt deal with Mouse Scroll Event

{% highlight cpp %}
bool QDialog::eventFilter(QObject *target, QEvent *event)
{
    if (target == *SomeQGraphicsScene*)
    {
       if (event->type() == QEvent::GraphicsSceneWheel)
       {
           const QGraphicsSceneWheelEvent * const me = static_cast<const QGraphicsSceneWheelEvent*>(event);
           /* deal with me->delta() */
           return true;
        }
    }
    return false;
}
{% endhighlight %}
