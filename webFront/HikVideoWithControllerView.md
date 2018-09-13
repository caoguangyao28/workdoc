# 复杂的视频弹窗页面，用于监测系统 视频菜单下 与 视频树数据 联动
  宁波监测系统(http://10.45.7.208/svnzqzhjt/sts_dev/Product/Transport/tmsp/R4/trunk)
> 页面使用方式 示例如下

    //view 名称HikVideoWithControllerView
    /**
     * Created by cao.gy on 2017/8/16.
     * 基于fish 的拖动时间轴
     *
     * 可接收入参
     * obj json 对象
     * obj.resourceType  singleVideo|multiVideo|recordVideo 单屏/多屏/历史 模式
     * obj.videos []  视频设备数组 必须是数组
     *
     */
    //使用参考
            fish.popupView({
                url: "modules/video/views/HikVideoWithControllerView",
                width: 980,
                height: 550,
                modal: false,
                viewOption: {
                    videos:[{teId:888,teName:'设备1'}],//视频设备信息列表
                    resourceType:'singleVideo',//singleVideo|multiVideo|recordVideo
                }
            });
    //如果视频弹窗已存在的情况下 判断方式 $('div.video-player-controller').length 是否 不为0
    //需要触发事件 通知 视频视图  portal``` 相关为全局事件 监听 及定义 事件监听创建 在视频视图
    this.trigger(portal.eventBus,portal.const.VIDEO_RESOURCE_CHANGE,paramObj);//paramObj 格式同上面 初始化需要参数