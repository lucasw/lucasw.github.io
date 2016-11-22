---
title: Bullet Physics Soft Bodies
layout: post
---


The bullet source doesn't build SoftDemo currently (is it unstable?), needed these changes:

```
diff --git a/examples/ExampleBrowser/CMakeLists.txt b/examples/ExampleBrowser/CMakeLists.txt
index 32f4c18..11a72fa 100644
--- a/examples/ExampleBrowser/CMakeLists.txt
+++ b/examples/ExampleBrowser/CMakeLists.txt
@@ -196,6 +196,8 @@ SET(BulletExampleBrowser_SRCS
        ../Planar2D/Planar2D.h
        ../RollingFrictionDemo/RollingFrictionDemo.cpp
        ../RollingFrictionDemo/RollingFrictionDemo.h
+       ../SoftDemo/SoftDemo.cpp
+       ../SoftDemo/SoftDemo.h
        ../FractureDemo/FractureDemo.cpp
        ../FractureDemo/btFractureBody.cpp
        ../FractureDemo/btFractureDynamicsWorld.cpp
diff --git a/examples/ExampleBrowser/ExampleEntries.cpp b/examples/ExampleBrowser/ExampleEntries.cpp
index 0608f0b..2562b08 100644
--- a/examples/ExampleBrowser/ExampleEntries.cpp
+++ b/examples/ExampleBrowser/ExampleEntries.cpp
@@ -158,7 +158,8 @@ static ExampleEntry gDefaultExamples[]=
        //ExampleEntry(1, "Spheres & Plane C-API (Bullet3)", "Collision C-API using Bullet 3.x backend", CollisionTutorialBullet2CreateFunc,TUT_SPHERE_PLANE_RTB3),
 
 
-
+// TODO(lucasw) had to add this
+#define INCLUDE_CLOTH_DEMOS
 #ifdef INCLUDE_CLOTH_DEMOS
        ExampleEntry(0,"Soft Body"),
        ExampleEntry(1,"Cloth","Simulate a patch of cloth.", SoftDemoCreateFunc,0),
```


My soft body nodes float off the ground- how to fix that?


The demos show off volume and pressure preserving soft bodies- how do they work?

kVST, kAST, and many other paramters aren't used at all.
