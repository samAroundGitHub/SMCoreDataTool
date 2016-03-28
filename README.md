# SMCoreDataTool

轻量级处理CoreData工具

简单易用实现 增 删 改 查

内部单例模式, 增加数据方法使用运行时机制, 提供Model自动捕获赋值

//////////////////////////////////////////////////////////////////////////

// 查看项目内所有entity
    NSArray *entities = [SMCoreDataTool shareSMTool].sm_entitys;
    for (NSEntityDescription *desc in entities) {
        NSLog(@"entityNames: -%@", desc.name);
    }

//////////////////////////////////////////////////////////////////////////

// 添加操作
// 方法1

    [SMCoreDataTool sm_toolAddDataWithEntity:ExampleEntity attributeNames:@[@"name", @"title", @"age"] attributeValues:@[@"jack", @"jack is ugly", @"22"]];
    
    // 方法2
    // 运行时机制, 传入model即可
    // model 不含有age属性, 所以age属性不会进入到coredata
    SMModel *model = [[SMModel alloc] init];
    model.name = @"tom";
    model.title = @"tom is handsome";
    [SMCoreDataTool sm_toolAddDataWithEntity:ExampleEntity attributeModel:model];

// 查询操作

    NSArray *arr = [SMCoreDataTool sm_toolSearchDataWithEntity:ExampleEntity andPredicate:nil];
    for (Example *example in arr) {
        NSLog(@"arr1 : %@ - %@ - %@", example.name, example.age, example.title);
    }
    
// 删除操作

    [SMCoreDataTool sm_toolDeleteDataWithEntity:ExampleEntity andPredicate:@"name = 'jack'"];
    
// 更新操作

    [SMCoreDataTool sm_toolUpdateDataWithEntity:ExampleEntity attributeName:@"title" predicate:@"name = 'tom'" andUpdateValue:@"tom is ugly too"];

//////////////////////////////////////////////////////////////////////////

// 清除所有结果

    [SMCoreDataTool sm_toolClearCoraDataWithEntiy:ExampleEntity];

//////////////////////////////////////////////////////////////////////////
