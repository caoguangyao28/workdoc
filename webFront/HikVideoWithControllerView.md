# ���ӵ���Ƶ����ҳ�棬���ڼ��ϵͳ ��Ƶ�˵��� �� ��Ƶ������ ����
  �������ϵͳ(http://10.45.7.208/svnzqzhjt/sts_dev/Product/Transport/tmsp/R4/trunk)
> ҳ��ʹ�÷�ʽ ʾ������

    //view ����HikVideoWithControllerView
    /**
     * Created by cao.gy on 2017/8/16.
     * ����fish ���϶�ʱ����
     *
     * �ɽ������
     * obj json ����
     * obj.resourceType  singleVideo|multiVideo|recordVideo ����/����/��ʷ ģʽ
     * obj.videos []  ��Ƶ�豸���� ����������
     *
     */
    //ʹ�òο�
            fish.popupView({
                url: "modules/video/views/HikVideoWithControllerView",
                width: 980,
                height: 550,
                modal: false,
                viewOption: {
                    videos:[{teId:888,teName:'�豸1'}],//��Ƶ�豸��Ϣ�б�
                    resourceType:'singleVideo',//singleVideo|multiVideo|recordVideo
                }
            });
    //�����Ƶ�����Ѵ��ڵ������ �жϷ�ʽ $('div.video-player-controller').length �Ƿ� ��Ϊ0
    //��Ҫ�����¼� ֪ͨ ��Ƶ��ͼ  portal``` ���Ϊȫ���¼� ���� ������ �¼��������� ����Ƶ��ͼ
    this.trigger(portal.eventBus,portal.const.VIDEO_RESOURCE_CHANGE,paramObj);//paramObj ��ʽͬ���� ��ʼ����Ҫ����