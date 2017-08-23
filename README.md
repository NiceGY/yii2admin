全站打包：https://share.weiyun.com/92c0d3e52e99d94255e001c76689b0a1 （不定期更新，安装出错的朋友可以试试这个）


## 一、开发基础说明
* 系统配置文件为.env文件。

* gii生成的模型统一放在 common\models下，模型统一继承 common\core\BaseActiveRecord  方便扩展yii核心；

* 所有表单模型都继承 common\core\BaseModel；

* 所有控制器都继承 common\core\Controller ，每个应用下面应有一个BaseController控制器，做为该应用的父控制器，方便做一些公共操作；

* 所有 自定义助手函数都放在 common\helpers\ 且方法都未static方法；

* 公共别名在common/config/bootstarp.php中定义，使用Yii::getAlias()访问；

* 超级管理员在\backend\comfig\params.php的“admin”项中定义其UID，超级管理员不需要进行RBAC权限检查；

* 关于后台中的配置项目，实际是经过转化后(通常在BaseController控制器的init构造函数中转化)，变为Yii::$app->params['web']中；
```php
Yii::$app->params['web'] = Config::lists();
```
* 在后台的BaseController中有一些通用的方法，例如saveRow（添加或编辑一行）、delRow（删除一行）、error（错误提示）、success（成功提示）、setForward（标记当前列表url，通常在列表中标记）、getForward（获取列表url方便跳转，通常结合error或success使用）；

* 多语言配置在/common/config/main.php中“i18n”项中，源语言设置的是中文，具体可自行查看；

* 后台项目的js和css资源文件放在/common/metronic中；

* 由于我使用的是模板自带的jQuery和bootstrap，所以我再后台main.php的assetManager项中清空了系统自带的jQuery和bootstrap，为了模板全局的js/css放在其他插件的前面，这里我设置了yii\web\JqueryAsset依赖backend\assets\AppAsset，这里要注意循环依赖的问题；

* RBAC权限系统没有使用第三方扩展，其实现大致思路为：一个后台用户对于一个用户组，用户权限和后台栏目一一对应；

* API接口主要使用模块做版本控制，使用RESTfull标准，权限及接口限制参考/api/models/User.php；

* 关于后台权限问题，后台权限是与Menu绑定的，在添加功能时先在后台【系统-菜单管理】中添加列表、增、删、改等菜单，然后到【用户-后台用户-权限管理】中【授权】，可以看到刚刚添加的菜单，勾选并提交后对应的用户组就有了该权限；

## 二、上传图片说明

#### 1、上传单图和多图

* 图片上传使用/common/widgets/images，需要扩展的可以自行修改，使用的是ajax将图片转化为base64编码后上传的；

* 图片存储在storage/web/image目录下面。如果服务器解析到/web目录，则图片上传地址须修改，详情参考/web目录；

* 图片上传配置文件在/common/config/params的upload配置项中；

* 后台图片上传使用的是backend/controllers/PbulicController控制器，上传成功后返回“201610/123456789123.jpg”。结合Yii::$app->params['upload']就可以生成图片路径。

* 同时也可以使用\common\helpers\Html::src()方法生成图片路径。这个函数还可以生成类似“URL/index.php?path=201910/123456789123.jpg&w=100&h=100&fit=crop”的裁剪后的图片。其中URL可以是完整的路径，包含http，其配置在common/config/bootstarp.php的“@storageUrl”中配置。

#### 2、编辑器使用UEditer(百度的编辑器)

* 百度编辑器使用的是大裤衩的扩展，请自行查看；

* 百度编辑器的上传路径配置在\common\comfig\params.php的ueditorConfig配置项；






超级管理员账号： admin 123456
普通管理员： guanli 123456
编辑人员： feifei 123456
```

