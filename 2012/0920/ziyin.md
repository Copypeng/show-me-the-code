# nodejs�ļ����ط���

�ȵ��ļ����ӣ�
1.Excel2007 ��utf-8�����csv�ļ�Ĭ������
�����Ϣ��http://www.docin.com/p-31710590.html
2.�ļ����к����ģ����ػ����롣����������ֲ�ͬ
�����Ϣ��http://www.phpv.net/html/1675.html

���������
iconvת�룬utf-8 -> gbk
ת���Ϊbuffer��������ֱ��res.end(buffer), header�е�filename����buffer.toString('binary');



```js
var http = require('http');
var url = require('url');
var Iconv = require('iconv').Iconv;
var crypto = require('crypto');
var server = http.createServer(function(req, res){
  var path = url.parse(req.url).pathname;

  if(path == '/favicon.ico'){
    res.end('');
  }else{
    var filename = '2012-06-01 �� 2012-06-01 (Ůװ��ҵ�ſ�) ���ݱ���.csv';
    var content = "���,����,�ɽ���Ʒ��,�͵���,��ע����,��������,�ղ�����\n1, 2012-06-01, 5061106, 162, 13463027, 5388282, 144738\n1, 2012-06-02, 5011106, 262, 3463027, 538282, 644738";
    //excel2007Ĭ�ϲ�֧��utf-8�����csv�ļ�
    var iconv = new Iconv('UTF-8', 'GBK//IGNORE');
    content = iconv.convert(content);
    res.setHeader('Pragma', 'public');
    res.setHeader('Expires', '0');
    res.setHeader('Cache-Control', 'no-store, no-cache, must-revalidate, max-age=0');
//    res.setHeader('Cache-Control', 'pre-check=0, post-check=0, max-age=0');
//    res.setHeader('Content-Transfer-Encoding', 'none');
    res.setHeader('Content-Type', 'text/csv; charset=GBK');
    filename = iconv.convert(filename).toString('binary');
    res.setHeader('Content-Disposition', 'attachment;filename="'+ filename +'"');
    res.setHeader('Content-Length', content.length);
    res.end(content);
  }
}).listen(22222);
```
