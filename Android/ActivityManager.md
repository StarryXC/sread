> Thinking

```
ActivityManager


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
ActivityManager activityManager = (ActivityManager) getSystemService(Context.ACTIVITY_SERVICE);

ActivityManager.MemoryInfo memoryInfo = new ActivityManager.MemoryInfo();
activityManager.getMemoryInfo(memoryInfo);
memoryInfo.totalMem; // 总内存
memoryInfo.availMem; // 可用内存
memoryInfo.threshold; // 临界值，达到这个值，进程就要被杀死
memoryInfo.lowMemory; // 最低内存

List<ActivityManager.RunningAppProcessInfo> runningAppProcesses = activityManager.getRunningAppProcesses();
runningAppProcesses.get(0).pid;
runningAppProcesses.get(0).uid;
runningAppProcesses.get(0).lru;
runningAppProcesses.get(0).processName;
runningAppProcesses.get(0).importance;
runningAppProcesses.get(0).importanceReasonCode;

// RECENT_WITH_EXCLUDED=1,RECENT_IGNORE_UNAVAILABLE=2
List<ActivityManager.RecentTaskInfo> recentTasks = activityManager.getRecentTasks(5, 1);
recentTasks.get(0).baseIntent; // 触发该任务的Intent
recentTasks.get(0).description; // 描述性文字
recentTasks.get(0).id; // 如果是运行中的TASK，唯一标识该任务，如果不是，为-1
recentTasks.get(0).origActivity; // 触发任务的第一个 activity
recentTasks.get(0).persistentId; // 当前任务的唯一标识

List<ActivityManager.RunningServiceInfo> runningServices = activityManager.getRunningServices(5);
runningServices.get(0).service; // 服务组件名
runningServices.get(0).clientPackage;
runningServices.get(0).process;
runningServices.get(0).activeSince; // 开始时间
runningServices.get(0).clientCount; // 连接到服务的客户数量
runningServices.get(0).clientLabel; // 标识特殊服务
runningServices.get(0).crashCount; // 运行过程中奔溃的次数
runningServices.get(0).flags;
runningServices.get(0).lastActivityTime; // 最后服务结束的时间
runningServices.get(0).restarting; // 如果非0,代表服务没启动,计划启动
runningServices.get(0).foreground; // 是否处于处于最前面的服务状态
runningServices.get(0).started; // 服务以后已经开启
runningServices.get(0).pid;
runningServices.get(0).uid;

// 获得系统里正在运行的所有进程
List<ActivityManager.RunningTaskInfo> runningTasks = activityManager.getRunningTasks(5);
runningTasks.get(0).baseActivity; // 任务主activity名
runningTasks.get(0).description; // 任务的描述
runningTasks.get(0).id; // 任务的id号
runningTasks.get(0).numActivities; // 该任务的activity的数量
runningTasks.get(0).numRunning; // 当前活动的activity数量
runningTasks.get(0).thumbnail;
runningTasks.get(0).topActivity; // 当前活动activity中处于最顶端的activity
runningTasks.get(0).describeContents(); // 描述文本

List<ActivityManager.ProcessErrorStateInfo> processesInErrorState = activityManager.getProcessesInErrorState();
processesInErrorState.get(0).condition; // 进程进入的条件
processesInErrorState.get(0).crashData; // crash数据
processesInErrorState.get(0).longMsg; // 对条件condition的描述
processesInErrorState.get(0).processName;
processesInErrorState.get(0).pid;
processesInErrorState.get(0).shortMsg;
processesInErrorState.get(0).stackTrace; // 堆栈追踪到的信息
processesInErrorState.get(0).tag; // activity名是否与错误有关联
processesInErrorState.get(0).uid;
processesInErrorState.get(0).describeContents(); // 数据包裹的描述

activityManager.clearApplicationUserData();
Debug.MemoryInfo[] processMemoryInfo = activityManager.getProcessMemoryInfo(new int[]{Process.myPid()});

```

