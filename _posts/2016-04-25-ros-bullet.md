
catkin_make
./devel/lib/bullet_server/bullet_server 
Segmentation fault (core dumped)

export PKG_CONFIG_PATH=/home/lucasw/other2/install/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH
g++ bullet_server.cpp `pkg-config bullet --cflags` `pkg-config bullet --libs`
bullet_server.cpp: In constructor ‘BulletServer::BulletServer()’:
bullet_server.cpp:53:53: error: cannot allocate an object of abstract type ‘btSequentialImpulseConstraintSolver’
   solver_ = new btSequentialImpulseConstraintSolver();
                                                     ^
In file included from /usr/include/bullet/btBulletDynamicsCommon.h:37:0,
                 from bullet_server.cpp:21:
/usr/include/bullet/BulletDynamics/ConstraintSolver/btSequentialImpulseConstraintSolver.h:32:28: note:   because the following virtual functions are pure within ‘btSequentialImpulseConstraintSolver’:
 ATTRIBUTE_ALIGNED16(class) btSequentialImpulseConstraintSolver : public btConstraintSolver
...

Try exact copy of hello world http://www.bulletphysics.org/mediawiki-1.5.8/index.php/Hello_World

g++ hello_world.cpp `pkg-config bullet --cflags` `pkg-config bullet --libs`

That works with the system libs, but no the 2.82 other2 libs (that one segfaults)

So copying hello world into bullet_server.cpp does not SIGSEGV, so work from there into a real bullet server that works.

