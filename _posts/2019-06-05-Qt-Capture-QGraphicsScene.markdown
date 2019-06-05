---
title: "Qt QGraphicsScene Magnifier"
layout: post
date: 2019-06-05 12:34
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Qt
- grab
category: blog
author: zuewang
description: 
---

# 0. some variables

{% highlight cpp %}
QGraphicsView *view;
QGraphicsScene *scene;
// current mouse position in the scene
QPointF mouse_pos;
// diameter of the magnifier
double magnifier_size = 100.0;
// scale factor inside magnifier
double magnify_factor;
view->setScene(scene);
{% endhighlight %}


# 1. grab QGraphicsView

{% highlight cpp %}
// after adding all contents to scene, fit in view to ensure entire scene is displayed
view->fitInView(view->sceneRect(), Qt::KeepAspectRatio);
// grab whole view
QPixmap pix = view->grab();
{% endhighlight %}

# 2. setup magnifier

{% highlight cpp %}
// set pix as the texture of brush 
QBrush brush(pix);
// set position of magnifier as a circle with current mouse position as its center
QGraphicsEllipseItem * magnifier = new QGraphicsEllipseItem(mouse_pos.x()-magnifier_size/2, mouse_pos.y()-magnifier_size/2, magnifier_size, magnifier_size);
// get mouse position in view
QPoint mouse_pos_view = view->mapFromScene(mouse_pos);
// get position of scene origin in view
QPoint origin_view = view->mapFromScene(0, 0);
// calculate the ratio: distance_in_scene / distance_in_view
double view_scale_ratio = (mouse_pos.x() - 0) / (mouse_pos_view.x() - origin_view.x());
/* the transformation matrix should work like this
   T mul mouse_pos_view = mouse_pos
   T mul origin_view = (0, 0)
   scale should be magnify_factor * view_scale_ratio,
   then calculate the translations tx and ty
*/
double scale = magnify_factor * view_scale_ratio;
QTransfrom transform(scale,     0.0,    0.0,
                     0.0,       scale,  0.0,
                     tx,        ty,     1.0);
brush.setTransform(transform);
magnifier.setBrush(brush);
// if already added to scene, do removeItem and then addItem
scene->addItem(magnifier);


{% endhighlight %}
