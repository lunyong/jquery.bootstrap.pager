# jQuery.bootstrap.pager插件的用法

标签（空格分隔）： jQuery插件 Bootstrap pagination

---

在Bootstrap组件中，有一个分页组件pagination，它很方便的为我们提供了分页条的代码。但它并没有提供用户与服务器交互的功能，因此在分页获取服务端数据时，需要自己处理分页条页码变化时的显示效果。jQuery.bootstrap.pager就是为了在分页获取数据时，coder能仅仅只关注如何展现数据，而无需频繁关注分页条的变化。
在使用的时候，coder可以像jQuery的ajax请求那样，直接传入一个数据接口的url地址，然后在success方法中处理返回的数据。调用示例如下：

    $.pager({
        renderTo: "#pager",   //分页条将要被渲染的地方，
        url: "/",    //请求数据的路径，
        type: "post",    //请求方式，可以不设置，默认为get，
        data: {},    //ajax请求所需参数，默认为空对象，
        dataType: "json",      //返回的数据类型，默认为json，
        displayNum: 20, //每次分页时，页面需要显示的记录数，默认为10，
        pageButtonNum: 7,              //最多显示数字按钮的个数，默认为10，
        requestPageName: 'page',    //请求参数中的页码参数名，默认为pageIndex，需要根据接口的实际参数名来定义
        requestSizeName: 'rows',    //请求参数中的代表每页显示几条数据的参数名，默认为pageSize，需要根据接口的实际参数名来定义
        responsePageName: 'page',   //返回数据中的页码字段名，默认为pageIndex，需要根据接口返回数据的实际字段名来定义
        responseTotalName: 'total', //返回数据中的总页数字段名，默认为totalPage，需要根据接口返回数据的实际字段名来定义
        responseRecordsName: 'records', //返回数据中的总记录数字段名，默认为totalRecords，需要根据接口返回数据的实际字段名来定义
        dataName: 'data',   //返回数据中需要分页显示的数据，默认为data，需要根据接口返回数据的实际字段名来定义
        pagerInfoEnabled: true, //是否显示分页信息模块(共0页，0条)，默认不显示
        pagerGoEnabled: true,   //是否显示跳转模块，默认不显示
        pagerInfoClass: 'pager-info',   //自定义分页信息模块的样式，如果没有将显示默认样式
        pagerGoClass: 'pager-go',   //自定义跳转模块的样式，如果没有将显示默认样式
        beforeSend: function(){},
        isTest: true,	//如果只是测试前端效果，那么可以加上isTest属性，正式使用时不需要
        success: function(data){
        
        },
        complete: function(){},
        error: function(){}
    });


在以上选项中，renderTo是必需的，它将决定分页条显示在哪里。url也是必需的，这是请求数据的地址。其它选项都可视情况而定，在没有设定的情况下，这些选项都会有自己的默认值。其中要注意的一点是，如果request参数名或response字段名没有设置，那么一定要确保数据接口的参数名和返回数据的字段名与本插件的默认值保持一致，这些默认值只涉及分页信息数据，与返回数据的其它部分无关。但返回的数据要遵循以下的json格式：{"data":[],"pageIndex":1,"totalRecords":2,"totalPage":1}，其中data是不可变的，其它三个字段可自由设置，但一定要有。
使用默认样式的完整的分页条如下图所示：
![分页条][1]
  [1]: https://raw.githubusercontent.com/lunyong/jquery.bootstrap.pager/master/image/page1.png
中间数字按钮样式是Bootstrap提供的，如果想定制自己的样式，直接使用新的css覆盖bootstrap的即可，info部分和go部分可以传入自己的class。

