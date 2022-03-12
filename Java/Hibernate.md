> Thinking

```
Configuration
AnnotationConfiguration
SessionFactory
Session
Transaction
SessionStatistics


// xml 元注解初始化
Configuration configuration = new Configuration().configure(); // 加载hibernate的配置文件
SessionFactory sessionFactory = configuration.buildSessionFactory();
Session session = sessionFactory.openSession(); // 打开session
Transaction transaction = session.beginTransaction(); // 开启事务

// insert id 不能相同
TableRecord tableRecord = new TableRecord();
Serializable serializable = session.save(tableRecord); // 把对象放入到了一级缓存中
System.out.println(serializable);
session.persist(tableRecord); // 取代save

// update
TableRecord tableRecord = session.get(TableRecord.class, 0L); // 查询 会把对象放入session缓存
System.out.println(tableRecord);
tableRecord.setName("tab0");

TableRecord tableRecord = new TableRecord();
tableRecord.setId(1);
session.update(tableRecord); // id存在，执行update语句 id不存在，报错 会把对象放入session缓存

// query
TableRecord tableRecord = session.get(TableRecord.class, 1L); //没有发出sql语句,说明数据来自于缓存
System.out.println(tableRecord);

Query query = session.createQuery("from TableRecord"); // 创建查询 org.hibernate.Query
List<TableRecord> tableRecords = query.list(); // 查询所有记录
for (TableRecord tableRecord : tableRecords) {
    System.out.println(tableRecord);
}

// delete
TableRecord tableRecord = session.get(TableRecord.class, 0L);
session.delete(tableRecord); // 删除

// refresh
TableRecord tableRecord = new TableRecord();
tableRecord.setId(1);
tableRecord.setName("tabName");
System.out.println(tableRecord);
session.refresh(tableRecord); // 把数据库中的数据同步到缓存中 发出sql语句了
System.out.println(tableRecord);

TableRecord tableRecord = session.get(TableRecord.class, 1L); //没有发出sql语句,说明数据来自于缓存
SessionStatistics sessionStatistics = session.getStatistics(); //SessionStatistics hibernate为一级缓存提供了一个统计机制
int entityCount = sessionStatistics.getEntityCount(); // session缓存中的实体个数
System.out.println(entityCount);
// session.clear(); // 清空session缓存中所有对象
session.evict(tableRecord); // 清除session缓存中单个对象
System.out.println(sessionStatistics.getEntityCount());


TableRecord tableRecord = new TableRecord();
TableRecord2 tableRecord2 = new TableRecord2(); // student是一个持久化状态的对象 要想让班级维护关系必须 inverse="false"
tableRecord2.setId(1);
Set<TableRecord2> tableRecord2Set = new HashSet<>();
tableRecord2Set.add(tableRecord2);
tableRecord.setTableRecord2Set(tableRecord2Set);
session.update(tableRecord);

/*
classes是一个持久化状态的对象,不需要对classes进行update显示操作
<set name="students" cascade="save-update"> 删除该班级的学生
 */
TableRecord tableRecord = session.get(TableRecord.class, 0L);
tableRecord.setTableRecord2Set(null); // 解除关联
for (TableRecord2 tableRecord2 : tableRecord.getTableRecord2Set()) {
    session.delete(tableRecord2);
}

/*
<set name="students" cascade="delete"> 在删除班级的同时删除学生
 */
TableRecord tableRecord = session.get(TableRecord.class, 0L);
session.delete(tableRecord);

```

> Memory

```
Configuration configuration = new Configuration().configure(); // 加载hibernate的配置文件
SessionFactory sessionFactory = configuration.buildSessionFactory();
Session session = sessionFactory.openSession(); // 打开session

Transaction transaction = session.beginTransaction(); // 开启事务

// TODO: 22-1-3

/*
刷新session一级缓存中持久化对象到数据库中
    如果一个对象由ID值，则会去检查该对象的副本，如果和副本一致，则什么都不做，如果和副本不一致，则发出update语句
    如果一个对象没有ID值，则会发出insert语句
    在执行session.flush之前，所有的对持久化对象的属性的改变都在一级缓存中，和数据库没有关系
    在执行session.flush的时候，数据还停留在缓存中
 */
session.flush();
transaction.commit(); // 提交事务
session.close(); // 关闭session session生命周期结束，一级缓存生命周期也结束





Configuration configuration = new Configuration().configure(); // 加载hibernate的配置文件 org.hibernate.cfg.AnnotationConfiguration;
SessionFactory sessionFactory = configuration.buildSessionFactory();
Session session = sessionFactory.openSession(); // 打开session
// sessionFactory.getCurrentSession();

Transaction transaction = session.beginTransaction(); // 开启事务

// TODO: 22-1-3

/*
刷新session一级缓存中持久化对象到数据库中
    如果一个对象由ID值，则会去检查该对象的副本，如果和副本一致，则什么都不做，如果和副本不一致，则发出update语句
    如果一个对象没有ID值，则会发出insert语句
    在执行session.flush之前，所有的对持久化对象的属性的改变都在一级缓存中，和数据库没有关系
    在执行session.flush的时候，数据还停留在缓存中
 */
session.flush();
transaction.commit(); // 提交事务
session.close(); // 关闭session session生命周期结束，一级缓存生命周期也结束
```

