流程引擎activiti

将流程的配置和定义和业务数据进行分离，对比以状态为驱动开发的业务流程，有点在于**流程变动成本低**，只需更新业务流程图就可以完成

Activiti7 已经以启动器的形式自动集成了所有依赖，实现springboot的集成最简化，只需要通过简单的添加几行配置到springboot配置文件，即可使用

**因为activiti7自动集成了springboot-security,启动时需要添加相应配置**

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/activiti?useUnicode=true&characterEncoding=utf8&serverTimezone=UTC
    username: root
    password: allen

  activiti:
    #检查数据库是否存在默认表结构，没有则自动创建
    database-schema-update: true
    db-history-used: true
    #历史数据保留等级 full表示最高级
    #保存历史数据的最高级别，除了会保存audit级别的数据外，还会保存其他全部流程相关的细节数据，包括一些流程参数等。
    history-level: full
    #校验流程文件，默认校验resources下的processes文件夹里的流程文件
    check-process-definitions: true
```



### **表的命名规则和作用**

 **ACT_RE** ：'RE'表示 repository。 这个前缀的表包含了流程定义和流程静态资源 （图片，规则，等等）。

 **ACT_RU**：'RU'表示 runtime。 这些运行时的表，包含流程实例，任务，变量，异步任务，等运行中的数据。 Activiti 只在流程实例执行过程中保存这些数据， 在流程结束时就会删除这些记录。 这样运行时表可以一直很小速度很快。

 **ACT_HI**：'HI'表示 history。 这些表包含历史数据，比如历史流程实例， 变量，任务等等。

 **ACT_GE** ： GE 表示 general。 通用数据， 用于不同场景下

![img](https://pic2.zhimg.com/80/v2-222f12f36d890a4d26ffce66c83dd459_1440w.jpg)

## **类关系图**



![img](https://pic4.zhimg.com/80/v2-c33ee3444141b1a2c3b45ef88db771df_1440w.jpg)

在新版本中，我们通过实验可以发现IdentityService，FormService两个Serivce都已经删除了。

所以后面我们对于这两个Service也不讲解了，但老版本中还是有这两个Service，同学们需要了解一下

```java
//运行时数据服务类
@Autowired
private RuntimeService runtimeService;

  //使用运行时数据服务类 根据流程定义key查询 相关流程
  ProcessInstanceQuery myLeave = runtimeService.createProcessInstanceQuery()
                  .processDefinitionKey("myLeave");
  List<ProcessInstance> list = myLeave.list();
  for (ProcessInstance instance : list) {
    System.out.println("流程实例ID：" + instance.getProcessInstanceId());
    System.out.println("所属流程定义ID：" + instance.getProcessDefinitionId());
    System.out.println("是否执行完成：" + instance.isEnded());
    System.out.println("是否暂停：" + instance.isSuspended());
    System.out.println("当前活动标识：" + instance.getActivityId());
    System.out.println("业务关键字：" + instance.getBusinessKey());
    System.out.println("--------------------");
  }

//任务服务类
@Autowired
private TaskService taskService;

  // 任务负责人
  String assignee = "financer";
  // 根据流程id，任务负责人查询待办任务
  TaskQuery myLeave = taskService.createTaskQuery()
    .processDefinitionKey("myLeave")
    .taskAssignee(assignee);
   List<Task> list = myLeave.list();
          for (Task task : list) {
              System.out.println("流程实例ID：目前看来是启动流程实例时在act_ru_execution表生成的第一条id" + task.getProcessInstanceId());
              System.out.println("任务ID" + task.getId());
              System.out.println("任务负责人" + task.getAssignee());
              System.out.println("任务名称" + task.getName());
              System.out.println("--------------------");
              taskService.complete(task.getId());
          }

//仓库服务类（存储部署流程）
@Autowired
private RepositoryService repositoryService;

	//根据id删除流程部署
  repositoryService.deleteDeployment("d630c5d7-ba07-11eb-8dc1-62f262d6f7c2");

//历史服务类
@Autowired
private HistoryService historyService;
```

