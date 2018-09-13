应急模块 controller 入口（1）
> 涉及应急专题查询 应急群组 应急指令 应急审核 功能
> 

类名称：EmgcManagerController

      // 获取专题应急列表 
      // EmgcManagerController/findTcEmcTheme
      var themeList = portal.callRemote("EmgcManagerController/findTcEmcTheme.json",{});