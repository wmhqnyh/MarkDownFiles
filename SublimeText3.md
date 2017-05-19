## Sublime Text 3 （3126）版本

* Sublime Text 3 （3126） 在文本编译器上可谓是强大，特别是针对前端开发工程师而言，更是可以称之为神器。相比专门开发用的IDE，作为文	本编辑器的ST3 可谓有IDE的一样强大的功能。ST上面的插件也是功能众多，不免让人眼花缭乱。现在对于ST3的部分功能进行整理：

*	官网：[Sublime Text官网](http://www.sublimetext.com)
*	License: 官方下载的需要导入License（购买），当然现在网上也有不少破解版，或者破解补丁，以及汉化补丁

#####插件安装（注明：部分插件区分ST2和ST3）在安装插件之前，需要安装Package Control组件  

1. 在线安装  
2. 
    按<kbd>ctr+`</kbd>调出console面板,粘贴以下代码（或者[SUBLIME TEXT 3](https://packagecontrol.io/installation#st3)面板中的代码）到命令行并回车    
    
    ```javascript
    import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
    ```  
    
    重启Sublime Text 3。如果在Perferences->package settings中看到package control这一项，则安装成功。 

2. 手动安装  

    如果你的电脑没有外网权限(小编就是这样)，那只能手动安装了  
    点击Preferences 选择Browse Packages… ，打开其上一级文件夹Data并进入Installed Packages文件夹  
    将下载的[Package Control.sublime-package文件](https://packagecontrol.io/Package Control.sublime-package)复制进去，再重启Sublime Text

##### 安装方法介绍

1. 在线安装   
    按下<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>调出命令面板，输入install选择Install Package 选项并回车，  
    再输入你要安装的插件名称(例如sublime tmpl)，然后在列表中选中要安装的插件。  
    安装成功后一般在Perferences->package settings中可看到  
    有些插件有可能在列表中搜索不到，你可以选择手动安装  
2. 手动安装  
    进入[sublimetext安装包管理器官网](https://packagecontrol.io/)在搜索框里输入你所需要的插件名称  
    进入插件的github页面（点击Details下面的github.com）,点击右侧的clone or download -> Download ZIP,将下载的压缩包解压后放在Preferences->Browse Packages（即packages文件夹）里面，并重命名（去掉文件名中的-master）  
    重启Sublimetext3即可安装成功