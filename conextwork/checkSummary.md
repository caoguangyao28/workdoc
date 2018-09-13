# 前端地址搜索效果实现
  实现基于 handlebar Underscore jquery

>## 模板部分代码 通过 script type="text/x-handlebars-template" id 定义
    <script type="text/x-handlebars-template" id="checkout-address-template">
    {{#each list}}
        <div class="address-info address-detail hover">
            <div class="address-name bold">
                <div class="radio">
                    <input type="hidden" name="id" value="{{id}}" />
                    <input type="hidden" name="addressId" value="{{addressId}}" />
                    {{#if deliveryAddressIdEqualId}}
                        <input name="data-address" type="radio" checked="checked" id="address-list{{@index}}">
                    {{else}}
                        <input name="data-address" type="radio" id="address-list{{@index}}">     
                    {{/if}}
                    <label for="address-list{{@index}}">
                        <span class="name">{{firstName}}</span>
                        <span class="phone" data-cellphone="{{cellphone}}" data-telCode="{{telCode}}" data-phone="{{phone}}">
                            {{#if cellphone}}
                                {{cellphone}}
                            {{else}}
                                {{phone}}
                            {{/if}}
                        </span>
                        <div class="red-default {{#if defaultAddress}} {{else}} hidden {{/if}}">
                            默认
                        </div>
                        <div class="attr-default {{#if defaultAddress}} hidden {{/if}}">
                            设置默认
                        </div>
                        <p>
                            <em data-region>
                                {{#if regionIsocode}}
                                    {{regionIsocode}}
                                {{/if}}
                            </em>
                            <em data-city>
                                {{#if lynxCityCode}}
                                    {{lynxCityCode}}
                                {{/if}}
                            </em>
                            <em data-district>
                                {{#if lynxDistrictCode}}
                                    {{lynxDistrictCode}}
                                {{/if}}
                            </em>
                            <em data-streetname>{{streetName}}</em>
                            <span class="edit add">
                                编辑
                            </span>
                        </p>
                    </label>
                </div>
            </div>
            <div class="default">
                    <em class="{{#if defaultAddress}} icon-swiper-h {{else}} icon-swiper {{/if}}"></em>
                    <span class="add-default {{#if defaultAddress}} {{else}} hidden {{/if}}">
                        默认
                    </span>
                    <span class="edit">
                        编辑
                    </span>
                </div>
        </div>
    {{/each}}
    </script>

>## js 部分

    <script type="text/javascript">
        var isChecking = null;//用于跟踪是否正在过滤数据
		var originalHtml;
		function filterData(){
			if(isChecking){
                clearTimeout(isChecking);
            }
            isChecking = setTimeout(function () {
				filterAndRender();
				//获取原始全量数据 
                clearTimeout(isChecking);
            },500);
        }
        
        function upDefaultDatas(data){
            var retData,falseDatas;
            var truesDatas = _.where(data,{defaultAddress:true});
            if(truesDatas.length > 0){
                falseDatas = _.where(data,{defaultAddress:false});
                retData = truesDatas.concat(falseDatas);
            }else{
                retData = data;
            }
            return retData;
        }

		function filterAndRender() {
			console.log($('input[name="searchName"]').val());
			var inputVal = $.trim($('input[name="searchName"]').val().toUpperCase());
			var retData = [];//过滤后的
            var retDataBy = [];
            var retDataWithDefault = [];
			//获取模板
			var sourse = $('#checkout-address-template').html();
			var template = Handlebars.compile(sourse);
            // var dataSourse = $('.addressDto').data('objectdto');
            var dataSourse = [{
						"id": 800002811537,
						"addressId": "800002811537",
						"firstName": "张三",
						"cellphone": "13766666666",
						"telCode": "",
						"phone": "",
						"streetName": "顶顶顶顶顶顶顶顶顶顶顶",
						"defaultAddress": true,
						"regionIsocode": "广东省",
						"lynxCityCode": "中山市",
						"lynxDistrictCode": "黄圃",
                        "pickupAddressFirstName": "",
                        "deliveryAddressId":1
					},{
						"id": null,
						"addressId": "800002811537",
						"firstName": "张二合",
						"line1": "顶顶顶顶顶顶顶顶顶顶顶",
						"line2": "",
						"cellphone": "13766666666",
						"telCode": "",
						"phone": "",
						"streetName": "顶顶顶顶顶顶顶顶顶顶顶",
						"defaultAddress": false,
						"regionIsocode": "广东省",
						"lynxCityCode": "中山市",
						"lynxDistrictCode": "黄圃",
                        "pickupAddressFirstName": "",
                        "deliveryAddressId":2
					}];//获取绑定的数据
			
			if(inputVal){
				//匹配过滤
				retData = _.filter(dataSourse,function(item,index){
                    var reg = /.*[\u4e00-\u9fa5]+.*$/;
                    var isExit;
                    if(reg.test(inputVal)){//输入含中文
					    isExit = item.firstName.toUpperCase().indexOf(inputVal);                        
                    }else{//拼音输入（只支持 全拼）
                        isExit = item.pinyin.toUpperCase().indexOf(inputVal);
                    }
					if(isExit >= 0){
                        if(item.deliveryAddressId == item.id){
                            item.deliveryAddressIdEqualId = true;
                        }else{
                            item.deliveryAddressIdEqualId = false;
                        }
						return true;
					}else{
						return false;
					}
				});
				//根据收货人排序
				retData = retData.sort(function compareFunction(item1,item2){
					return item1.firstName.localeCompare(item2.firstName);
                });
                
				if(retData.length > 0){
                    //执行渲染
                    $('span.filterNullInfo').addClass('hidden');
                    //将defaultAddress 为true 提升排序
                    retData = upDefaultDatas(retData);
					var html = template({list:retData});//可行
					// console.log(html);
					$('div.address-content').html(html);
				}else{
                    //需要添加无匹配数据提示信息
                    $('span.filterNullInfo').removeClass('hidden');
                }
			}else{
                $('span.filterNullInfo').addClass('hidden');
				$('div.address-content').html(originalHtml);
				return false;
			}
		}
		$(function(){
			isChecking = null;//用于跟踪是否正在过滤数据
			originalHtml = $('div.address-content').clone().html();//克隆原始数据dom
		});
    </script>

>## html部分
    <div class="cation">
         <span><i class="icon iconfont icon-xingzhuang2"></i></span>
         <p>您已创建7个送货地址，还能新建143个</p>
         <div class="search-wrapper clearfix" style="border: 1px solid #ededed;font-size: .12rem;line-height: .29rem;width: 5.89rem;background-color: #f5f5f5;position: relative;">
            <input style="height: 0.3rem;;width:95%;color:#222;background:#f5f5f5;font-size: .14rem;outline: 0;border: 0;" type="text" name="searchName" placeholder="请输入收货人姓名" value="" oninput="filterData()">
            <a style="background: inherit;position: absolute;padding-top: 10px;right: 10px;" data-icon="" href="#" class="ambtn searchbuyericon"></a>
         </div>
         <span style="display:inline-block;font-size: .12rem;margin-top:-8px;" class="red hidden filterNullInfo">你输入的姓名不存在，请重新输入</span>
    </div>

    <div class="address-content" style="top:1.68rem"></div>    <!-- 这个标签 修改的 style 属性 -->