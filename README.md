˵����
�������һ���򵥵ķ�ҳ���(����bootstrap3)
ʹ�÷����� page-test.html�ļ�

ע�⣺
    1����������д��ڵ�bug����pageNumSize����Ϊż����ʱ��������⣬�������û���������Ժ������
       ����������ʱû���֣�����bug����ϵ��(mxdyxzy@163.com)
    2�����ں�ʵ��Ӧ�ü��ɣ�
       1����������:
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
       Article.page() ��ҳ���״μ��ص�ʱ���ʼ����ҳ�õģ�Article.list()�ǵ����ҳ�ϱ�ǩ��ѯ�õģ�ֻ�в�ѯ����������ֱ��
       ��ҳ��input�������ȡ��Ҳ�����񴫵�(������conditions)

    3������֮�����������ѯ��������2��(����һ��)������һ������ʱ��û����ð취�����