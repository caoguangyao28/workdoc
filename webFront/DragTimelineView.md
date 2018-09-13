# 基于fish的可拖拽播放时间轴
  宁波决策系统(http://10.45.7.208/svnzqzhjt/sts_dev/Product/Transport/tdap/R4/trunk)
> 启动后快捷访问 url 示例如下
  效果：
  ![拖拽时间轴](./imgs/dragTime.png)
  
  
    http://127.0.0.1:8080/tdap-web/index.html?portalId=4#easyView/modules/decision/transport/cityPassengerAnalysis/views/cityPassengerMainView
    //view 路径
    public/dragTimeline/views/dragTimelineView.js
    /**
     * Created by cao.gy on 2017/5/18.
     * 基于fish 的拖动时间轴
     *
     * 可接收入参
     * this.options.playSpeed 播放步长【时间轴变动的单位时间】
     * this.options.timerSpeed 计时器 步长[刷新时间轴本身]。
     *
     * 通过 this.trigger('timeChage',param) 触发其它视图的回调函数
     * param 为回传参数 {startTime:'',endTime:''}  开始&结束 时间
     *
     */
    //使用参考
     var dragTimelineViewT = new dragTimelineView({});//实例化
     this.setView('.dragTimeContent',dragTimelineViewT);//挂载到视图
     this.listenTo(dragTimelineViewT,'timeChange',this.updateTrafficJamVue);//监听时间轴 时变化事件 传入回调
    
