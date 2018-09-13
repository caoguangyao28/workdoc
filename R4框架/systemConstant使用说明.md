### SystemConstant.java 配置文件、数据库配置 信息设置 读取
> svn路径：http://10.45.7.208/svnzqzhjt/platform_dev/ZSmartCityFramework/trunk/zsmartcity/zsmartcity-context/src/main/java/com/ztesoft/zsmartcity/commons

常用的静态方法：

- getProperty 获得配置的系统常量的值
    - （String key） 根据key 获取配置文件中对应的值
    - （String key,String defaultValue） key 对应没有配置时 返回 defaultValue
- getSystemParam 获得数据库中配置的系统参数
    - （String paramKey）
    - （String paramKey, Class<T> type）返回数据类型映射为 type
    - （String[] paramKeys）
    - （String[] paramKeys, Class<T> type）每个返回数据类型映射为 type
- getRealPath 获得项目部署的真是路径
