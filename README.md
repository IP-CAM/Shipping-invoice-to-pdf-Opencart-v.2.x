# 配送 and invoice export PDF

For OpenCART, you can export it to a PDF file for the order delivery list and invoice in the background.

HTML2PDF class, [github address] (https://github.com/spipu/html2pdf/).

#installation

Make sure OpenCART has already installed VAMOD.

Install the XML file, then refresh and add permissions to the administrator group. Can be found under Sales / Orders.

#vqmod installation

Download [VQMOD for OpenCart] (http://www.opencart.com/index.php?route=extension/extension/info&ofo ts ion_id=19501), [VQMOD] (https://github.com/vqmod/vqmod)

Put the VQMOD file in the SYSTEM in the same directory, execute the example.com/vqmod/install, pay attention to permissions;

Replace the file of VQMOD for OpenCart2.

#note

Exporting Chinese will garble, need additional fonts and add to HTML2PDF / _TCPDF_5.0.002 / fonts.

Create a custom font to see [here] (https://github.com/spipu/html2pdf/tree/master/_tcpdf_5.0.002/FONTS/UTILS).

Specific: Find a letter to Chinese, such as Microsoft Ya-black (MSYH.TTF), copy to HTML2PDF / * / FONTS / UTILS / Under the Utils folder, there should be a TTF2ufm.exe file, Shift + mouse button to open DOS, run The following command.
`` `
TTF2UFM -A -F MSYH.TTF
PHP -Q Makefont.php msyh.ttf msyh.ufm
`` `
At this time, three files are generated under the folder: msyh.ctg.z msyh.php msyh.z, copy this three files to the previous directory fonts, then call fonts in PHP, for example:
`` `
Include (HTML2PDF.CLASS.PHP ');
$ HTML2PDF = New HTML2PDF ('P', 'A4', 'En', True, 'UTF-8', Array (0, 0, 0, 0));
$ html2pdf-> pdf-> setDisplaymode ('fullpage ");
$ html2pdf-> setdefaultfont ('msyh');
$ HTML2PDF-> Writehtml ($ Content, False);
$ html2pdf-> Output ('Test.pdf', 'D');
`` `
