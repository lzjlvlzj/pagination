说明： 本插件是一个简单的分页插件(基于bootstrap3) 使用方法见 page-test.html文件

注意： 1、本插件还有存在的bug，当pageNumSize参数为偶数的时候会有问题，这个问题没有作处理，以后更正。
其他问题暂时没发现，如有bug请联系我(mxdyxzy@163.com)
2、关于和实际应用集成：
1）如下例子:
 var Article = {};
 Article.page = function(conditions){
     var url = "/article/list";
     var data = {};
     data.conditions = conditions;
     $.ajax({
         url:url,
         type:"post",
         data:data,
         dataType:'json',
         contentType: "application/x-www-form-urlencoded; charset=utf-8",
         success : function(resObj) {
             if( resObj ){
                 var option = {totalPage:resObj.totalPage, pageNumSize :5, callback : Article.list,conditions : conditions};
                 $("#page").paginator(option);
                 Article.show(resObj);
             }
         }
     });
 };
 Article.list = function(currentPage,conditions){
     var url = "/article/list";
     var data = {};
     data.conditions = conditions;
     data.currentPage = currentPage;
     $.ajax({
         url:url,
         type:"post",
         data:data,
         dataType:'json',
         contentType: "application/x-www-form-urlencoded; charset=utf-8",
         success : function(resObj) {
             if( resObj ){
                 Article.show(resObj);
             }
         }
     });
 };

3、不足之处：如上面查询，方法是2个(功能一样)，不是一个。暂时还没有想好办法解决。