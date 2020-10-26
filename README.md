<<<<<<< HEAD
# 项目发布正式修改
1、router.js 文件
这两个本地调试的时候可以注释掉（不注释掉会报错），发布时 history 要放开。
mode:'history', //正式 测试
base:'hsfront',  //正式 测试

2、store -> index.js 文件
orderSysSource: "HS_formal", // 可回溯渠道来源 正式:HS_formal 测试:HS_test
//因为接口图片返的是相对路径，本地调试时图片展示不出来，所以在这里添加了状态（可根据api代理正式、测试地址修改图片路径）， appid 发布测试时也要修改
baseImagePath: 'https://www.zgbxjj.com',  //所有图片路径
bannerImagePath: 'https://www.zgbxjj.com/hsFileData',  //banner图路径
JumpPath:'https://www.zgbxjj.com',  //弹出pdf文件路径
upLoadImg: 'https://www.zgbxjj.com',  //上传图片路径
appid: 'wxec19abc8795c0014', //测试:wx09f6d091df15b1f8    正式:wxec19abc8795c0014  
=======
# 项目介绍
移动端微商城
vue-cli 2.0，使用vant、layui UI框架
>>>>>>> 106c5c72fd0da5d774c0fe49568b8bb99c984365

3、可回溯打包修改
index.html 文件
pdf.html 文件
打包正式的时候，这两个文件里面的 SDK 引入正式的（相对路径）

4、打包文件名称修改为hsfront对应服务器上的hsfront文件夹，可在config文件下的index文件进行修改



# 项目难点
（1）投保页面：
    投保页面可配置：根据后台配置字段，前台进行展示，根据用户填写投保信息，传给后台，由于每个产品需求不一样，投保字段不一样，前台页面展示也是有些差异，导致实施起来比较麻烦（可能比较菜，无法实现业务需求）
    前台投保字段展示：投保页面展示使用的vantUI的框架，根据后台配置投保字段进行页面渲染，这里使用vantUI框架的组件就使得灵活性更加的差。
        例如：vant的van-action-sheet（相当于select效果）要处理回调，这点就无法实现配置字段进行前台渲染，就算渲染出vant组件，回调就无法处理，投保页面的省市区，有些是根据保险公司的数据库编码进行展示省市区（不同保险公司的省市区code编码不一样），由于保险公司的省市区编码都不一样，数据格式也不一样，这也无法实现可配置（也许可以实现，但是臣妾做不到=.=）,现在实现方法，一些无法根据配置就渲染出来的字段特殊处理，如果所有保险产品都是用同一个组件的话，因为产品需求不一样，这样代码会越写越多，所以按照保险公司进行了分类，以防后期好维护（虽然说这块已经写烂了）。
        这里根据保险公司进行了分类，产品详情页面跳转哪个投保页面，在detailsTow.vue组件中可以进行修改。
    *还有新添加投保页面时，可以复制别的投保页面，但是不需要的字段一定要删除掉*

    投保页面多个被保人：根据后台配置展示被保人字段，用户可添加，填写信息之后传给后台，这个已经写了公用的模板，可以参考insuranceRenBao.vue（老年人产品），MultipleInsured.vue（多个被保人组件单独抽离了出来）多个被保人组件

（2）预览页面：
    预览页面policyPreview.vue组件 （公共预览页面），预览页面其实也有好几个，没有特殊需求大部分都是使用的policyPreview组件。
    预览页面比较麻烦的是，预览页面返回的数据都是你投保的时候传的，例如
    {
        holderName: "小明",
        holderAge: "18",
        otherJson:"{'holderCertificateNo':'123'}"
    }
    这样的数据格式，你要知道holderName映射什么样的中文，这个可以根据投保信息配置的接口进行映射。
    映射麻烦的点1：比如上面的otherJson，otherJson是干嘛的，投保页面的一些字段，在投保信息表里面没有这个字段，统一放到了otherJson里面，你要单独拿出来解析JSON，在去映射成中文。
    映射麻烦的点2：比如投保页面的省市区，你传的时候是这样传的
    {
        province:'河南省',
        city:'郑州市',
        county:'高新区'
    }
    然而你在预览的时候要这样展示：投保人地址：河南省 郑州市 高新区（你要特殊处理，取到这些值拼接起来展示，貌似说起来也不难），后面特殊处理的东西多了，就感觉特别复杂了（架构没有设计好，那那都是问题，还是我太菜了=.=）

（3）产品详情页面（产品规格）：
    产品详情页面比较难的可能是产品计划、产品规格了。
    产品规格、保障清单、都会根据产品计划进行切换，价格试算。
    由于一些产品的特殊需求，我这边一共有4个产品规格组件，GeneralSpecification.vue（公用产品规格组件）、DDB_Specification.vue（多多宝产品规格组件）、kLYS_Specification.vue（康乐一生产品规格组件）、MaMi_Specification.vue（妈咪宝贝产品规格组件）

完结。

    
    

    



