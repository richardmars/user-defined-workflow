# User-defined Workflow

# 1. 实现日志
## 1.1 Debug
* MultipartHttpServletRequest is required  
  主要原因是@SpringBootApplication所自带的自动配置MultipartSolver不能支持PUT方法，在Application.java中实现MultipartResolver Bean即可。  
  搜索问题时需要将问题拆分查找最可能出问题的地方，此例中需要注意Http Method的支持问题，用多种method进行测试。
* `new File(path)`和`new ClassPathResource(path)`两者需要的path不同  
  前者对应的是虚拟机启动的path，在eclipse中启动一般为项目的根路径；后者是类目录。因此需要`this.getClass().getResource("/" + path).toURI()`，让前者也加载类路径的文件。详见`com.xicoder.workflow.manage.rest.editor.Models.java`
* 类路径文件变化导致项目重启  
  这是因为spring-boot-devtools的特点，将文件放到public或者static文件夹即可。详见spring-boot-reference.pdf。

