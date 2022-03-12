> Thinking

```
ActivityManager

RunningAppProcessInfo
MemoryInfo
ProcessErrorStateInfo
RunningTaskInfo
RunningServiceInfo
RecentTaskInfo
```

> Memory

```
Context.ACTIVITY_SERVICE

ActivityManager
	getRunningAppProcesses
	clearApplicationUserData
	getMemoryInfo
    getProcessesInErrorState
    getRunningTasks # 获得系统里正在运行的所有进程
    getRunningServices
    getRecentTasks(20, 1) # RECENT_WITH_EXCLUDED=1,RECENT_IGNORE_UNAVAILABLE=2
    getProcessMemoryInfo(new int[]{Process.myPid()});
ActivityManager.RunningAppProcessInfo
	processName pid uid
    lastTrimLevel lru pkgList
    importance importanceReasonCode importanceReasonPid importanceReasonComponent
    IMPORTANCE_FOREGROUND
ActivityManager.MemoryInfo
	availMem # 可用内存
    lowMemory # 最低内存
    threshold # 临界值，达到这个值，进程就要被杀死
    totalMem # 总内存
ActivityManager.ProcessErrorStateInfo
	condition # 进程进入的条件
    crashData # crash数据
    longMsg # 对条件condition的描述
    processName
    pid
    shortMsg
    stackTrace # 堆栈追踪到的信息
    tag # activity名是否与错误有关联
    uid
    describeContents # 数据包裹的描述
ActivityManager.RunningTaskInfo
    baseActivity # 任务主activity名
    description # 任务的描述
    taskInfo.id # 任务的id号
    numActivities # 该任务的activity的数量
    numRunning # 当前活动的activity数量
    thumbnail
    topActivity # 当前活动activity中处于最顶端的activity
    describeContents # 描述文本
ActivityManager.RunningServiceInfo
	service # 服务组件名
    clientPackage
    process
    activeSince # 开始时间
    clientCount # 连接到服务的客户数量
    clientLabel # 标识特殊服务
    crashCount # 运行过程中奔溃的次数
    flags
    lastActivityTime # 最后服务结束的时间
    restarting # 如果非0,代表服务没启动,计划启动
    foreground # 是否处于处于最前面的服务状态
    started # 服务以后已经开启
    pid
    uid
ActivityManager.RecentTaskInfo
	baseIntent # 触发该任务的Intent
    description # 描述性文字
    id # 如果是运行中的TASK，唯一标识该任务，如果不是，为-1
    origActivity # 触发任务的第一个activity
    persistentId # 当前任务的唯一标识
```

