svn 路径：
http://10.45.7.208/svnzqzhjt/sts_dev/Product/Transport/tmsp/R4/trunk/tmsp-biz/src/main/java/com/ztesoft/zsmartcity/gis/controller/GeometryOprController.java     

# 方法名：qryGeoLayerGisData
>前台代码应用：

```    
    changeLayerData : function(displayCode){
			//displayCode代表
        	var localObj = this;
        	fish.ajax({
                url:'api/gis/GeometryOprController/qryGeoLayerGisData.json',
                data:{
                    gisTableName:"GT_SUBWAY_STT"
                },
                success: function (resultData) {
                	var iconObj ={} ;
                	iconObj.icon = "styles/img/gis/layers/icons/guidao.png";
                	iconObj.icon_selected= "styles/img/gis/layers/icons/guidao_selected.png";
                	resultData.style = iconObj;
                	localObj.layerDataObj = resultData;
              	  	localObj.layer.getSource().clear();
              	  	localObj.loadLayerData(resultData,"GlSubWaySttLayer",GtSubWaySttModel.POPUP_TPL);
                }
            });
        }
```