# HEXO框架改动记录

1. 原本使用google服务器的jquery访问不到，修改文件`themes/landscape/layout/_partial/after-footer.ejs`中的script行

   ```
   <script src="//cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
   ```

2. 原本Search按钮使用的google搜索，被屏蔽了无法搜索，修改成百度搜索，修改文件`node_modules/hexo/lib/plugins/helper/search_form.js`中的return行

   ```
   var url = config.url || '';
   if (url.startsWith('http://')) {
       url = url.substr(7);
   } else if (url.startsWith('https://')) {
       url = url.substr(8);
   }
     
   return `<form action="//www.baidu.com/s" method="get" accept-charset="UTF-8" class="${className}"><input type="search" name="q1" class="${className}-input"${text ? ` placeholder="${text}"` : ''}>${button ? `<button type="submit" class="${className}-submit">${typeof button === 'string' ? button : text}</button>` : ''}<input type="hidden" name="q6" value="${url}"></form>`;
   ```

3. 原本页面ARCHIVES下的年月显示为`九月 2019`，重定义`2019-09`格式，修改文件`node_modules/hexo/lib/plugins/helper/list_archives.js`中的`format = type === `行

   ```
   format = type === 'monthly' ? 'YYYY-MM' : 'YYYY';
   ```

   