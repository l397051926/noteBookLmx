1. 入口 SpringApplication.run(SampleWebUiApplication.class, args);
    开始构建 SpringApplication 对象
    执行run的动作
        开启一个整体的观察着 如果中间出现问题 则关闭整体功能
        构建 bootstrapContext 上下文 里面包含实体类的map 映射 
        可配置的应用程序上下文 重要对象   ConfigurableApplicationContext context 
        构造一个 application listeners  SpringApplicationRunListeners listeners
        正式开始处理所有数据 try{} catch
            应用的参数信息  ApplicationArguments applicationArguments = new DefaultApplicationArguments(args)
            构建 整体环境 重要步骤 ConfigurableEnvironment environment = prepareEnvironment(listeners, bootstrapContext, applicationArguments);
            