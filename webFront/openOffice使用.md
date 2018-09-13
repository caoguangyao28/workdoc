安装软件openoffice和swftools

修改DocConverter类

    //zsmartcity-biz/src/main/java/com/ztesoft/zsmartcity/emgc/util/DocConverter.java
    private static final int environment = 2;// 环境 1：windows 2:linux 
    //开发环境中改为1
    Process p = r.exec("F:/swftools/swftools/pdf2swf.exe "+ pdfFile.getPath() + " -o "+ swfFile.getPath())
    /**
    *路径修改为本地安装的swftools的路径
    *system.conf
    *#上传路径,修改为实践运行的路径
    *uploadPath=D:/myWorkspace/zhcs/first/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/zsmartcityWeb/repository
    *
    */

    
