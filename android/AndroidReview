##性能优化
###内存优化
####tips :
1. #### 使用 Memory Profiler 查看 Java 堆和内存分配
1. ####节制的使用service
 在启动一个Service后,系统将不会轻易的杀死这个进程,这是Android系统的保留机制,这样会耗费很多性能,在切换应用程序的时候,还有机率导致OOM,让一个Service一直在后台运行,然而不做任何事是一件非常浪费性能的做法.官方推荐的最佳解决方案是使用IntentService,在后台的异步任务结束后这个Service也会停止,释放内存,这样可以极大程度的避免Service的内存泄漏.
 2. #### 当页面不可见或者低内存时释放内存
```java
 /**
     * Release memory when the UI becomes hidden or when system resources   
     * become low.
     * @param level the memory-related event that was raised.
     */
    public void onTrimMemory(int level) {

        // Determine which lifecycle or system event was raised.
        switch (level) {

            case ComponentCallbacks2.TRIM_MEMORY_UI_HIDDEN:

                /*
                   Release any UI objects that currently hold memory.

                   The user interface has moved to the background.
                */

                break;

            case ComponentCallbacks2.TRIM_MEMORY_RUNNING_MODERATE:
            case ComponentCallbacks2.TRIM_MEMORY_RUNNING_LOW:
            case ComponentCallbacks2.TRIM_MEMORY_RUNNING_CRITICAL:

                /*
                   Release any memory that your app doesn't need to run.

                   The device is running low on memory while the app is running.
                   The event raised indicates the severity of the memory-related event.
                   If the event is TRIM_MEMORY_RUNNING_CRITICAL, then the system will
                   begin killing background processes.
                */

                break;

            case ComponentCallbacks2.TRIM_MEMORY_BACKGROUND:
            case ComponentCallbacks2.TRIM_MEMORY_MODERATE:
            case ComponentCallbacks2.TRIM_MEMORY_COMPLETE:

                /*
                   Release as much memory as the process can.

                   The app is on the LRU list and the system is running low on memory.
                   The event raised indicates where the app sits within the LRU list.
                   If the event is TRIM_MEMORY_COMPLETE, the process will be one of
                   the first to be terminated.
                */

                break;

            default:
                /*
                  Release any non-critical data structures.

                  The app received an unrecognized memory level value
                  from the system. Treat this as a generic low-memory message.
                */
                break;
       		}
 	}
```
3. ####尽量使用SparseArray替代HashMap
4. ####使用protobufs进行序列化
5. ####避免频繁创建对象占用堆内存,比如在ondraw方法中new 对象,这是很浪费内存的,应该将创建对象移动到外面去,比如构造方法中.
6. ####在不影响应用程序功能和用户体验的情况下尽可能的缩小APK的体积
7. ####使用Dagger来实现项目的依赖注入,Dagger非常适合安卓平台,并不是在运行时通过反射实现,反射这种机制尽量避免在Android平台上使用.会浪费很多内存.
8. ####谨慎的使用第三方框架,第三方框架一般来说功能非常丰富,代码也相应的很多,所以我们必须要考虑对性能的影响,有条件的可以查看对应的源码进行性能调研,如果是只用其中的一小部分功能,建议裁剪或或者自行实现,不必全部引入,增大应用的体积,也会耗费更多内存,降低应用性能
 
 