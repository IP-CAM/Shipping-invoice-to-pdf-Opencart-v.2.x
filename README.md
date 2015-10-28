#配送及发票导出PDF

用于Opencart，可以在后台为订单配送列表和发票导出为PDF文件。

使用了html2pdf类，[Github地址](https://github.com/spipu/html2pdf/)。

#安装

确保Opencart已经安装vamod。

安装xml文件，然后刷新并为管理员组添加权限。可以在Sales/Orders下找到。

#vqmod安装

下载[vqmod for opencart](http://www.opencart.com/index.php?route=extension/extension/info&extension_id=19501)，[vqmod](https://github.com/vqmod/vqmod)

把vqmod文件放到system同级的目录下，执行example.com/vqmod/install，注意权限；

把vqmod for opencart2 的文件解压替换。

#注意

导出中文会乱码，需要另外选择字体并添加到html2pdf/_tcpdf_5.0.002/fonts/。

创建自定义字体看[这里](https://github.com/spipu/html2pdf/tree/master/_tcpdf_5.0.002/fonts/utils)。

具体：找一个支持中文的字体，例如微软雅黑（msyh.ttf），复制到html2pdf/*/fonts/utils/下，在utils文件夹下应该有ttf2ufm.exe文件，shift+鼠标右键打开dos，运行以下命令。
```
ttf2ufm -a -F msyh.ttf
php -q makefont.php msyh.ttf msyh.ufm
```
这时文件夹下会生成三个文件：msyh.ctg.z  msyh.php  msyh.z，将这个三个文件复制到上一级目录fonts下，然后就可以在php中调用字体，例如：
```
include(html2pdf.class.php'); 
$html2pdf = new HTML2PDF('P', 'A4', 'en', true, 'utf-8', array(0, 0, 0, 0));
$html2pdf->pdf->SetDisplayMode('fullpage');
$html2pdf->setDefaultFont('msyh');
$html2pdf->writeHTML($content, false); 
$html2pdf->Output('test.pdf','D');
```