# ����fish�Ŀ���ק����ʱ����
  ��������ϵͳ(http://10.45.7.208/svnzqzhjt/sts_dev/Product/Transport/tdap/R4/trunk)
> �������ݷ��� url ʾ������
  Ч����
  ![��קʱ����](./imgs/dragTime.png)
  
  
    http://127.0.0.1:8080/tdap-web/index.html?portalId=4#easyView/modules/decision/transport/cityPassengerAnalysis/views/cityPassengerMainView
    //view ·��
    public/dragTimeline/views/dragTimelineView.js
    /**
     * Created by cao.gy on 2017/5/18.
     * ����fish ���϶�ʱ����
     *
     * �ɽ������
     * this.options.playSpeed ���Ų�����ʱ����䶯�ĵ�λʱ�䡿
     * this.options.timerSpeed ��ʱ�� ����[ˢ��ʱ���᱾��]��
     *
     * ͨ�� this.trigger('timeChage',param) ����������ͼ�Ļص�����
     * param Ϊ�ش����� {startTime:'',endTime:''}  ��ʼ&���� ʱ��
     *
     */
    //ʹ�òο�
     var dragTimelineViewT = new dragTimelineView({});//ʵ����
     this.setView('.dragTimeContent',dragTimelineViewT);//���ص���ͼ
     this.listenTo(dragTimelineViewT,'timeChange',this.updateTrafficJamVue);//����ʱ���� ʱ�仯�¼� ����ص�
    
