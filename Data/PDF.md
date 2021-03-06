# PDF

* [How I parse PDF files](https://thomaslevine.com/!/computing/parsing-pdfs/)
* [Tabula - liberating data tables](http://tabula.technology/)
* [easyInvoice](https://github.com/smhutch/easyInvoice)
* [jsPDF](https://parall.ax/products/jspdf)
* [PanDoc](http://johnmacfarlane.net/pandoc/)
* [PDF Viewing in GitHub](https://github.com/blog/1974-pdf-viewing)
* [PDF.js](https://github.com/mozilla/pdf.js)
* [HTML to PDF](https://www.designernews.co/stories/51286-html-to-pdf)
* [Generating complex PDF with Prawn](http://www.yoniweisbrod.com/generating-complex-pdf-documents-in-rails-with-prawn/)
* [PDF Object Representation in HexaPDF](https://gettalong.org/blog/2016/pdf-object-representation-in-hexapdf.html)
* [react-pdf](https://github.com/diegomura/react-pdf)
* [Puppeteer - Headless Chrome](https://try-puppeteer.appspot.com/)
* [WebAssembly and PDF](https://pspdfkit.com/blog/2017/webassembly-a-new-hope/)
* [A command-line tool to turn web pages into beautifully formatted PDFs](https://github.com/danburzo/percollate)

```
▶ mdls INR123.pdf
▶ mdls -raw -name kMDItemCreator INR123.pdf

▶ for file in *.pdf; do mdls -raw -name kMDItemCreator $file && echo; done
```

## Compression

* [ImageMagick's `-compress` option](https://www.imagemagick.org/script/command-line-options.php#compress)
* [GhostScript options](https://www.ghostscript.com/doc/9.20/VectorDevices.htm)
* [How to use GhostScript](https://www.ghostscript.com/doc/9.21/Use.htm)
* `-dAutoRotatePages` - Algorithm is heuristic based on majority of the pages' left to right flow, thus could be unreliable

```
// If PDF is mostly scanned images and no selectable text
// Uses GhostScript behind the scenes
// 150 dpi
▶ convert -density 150 -compress JPEG in.pdf out.pdf

// Best so far, similar size to smallpdf
// dPDFSETTINGS=/screen (screen-view-only quality, 72 dpi images)
// dPDFSETTINGS=/ebook (low quality, 150 dpi images)
// dPDFSETTINGS=/printer (high quality, 300 dpi images)
▶ gs -sDEVICE=pdfwrite \
     -dCompatibilityLevel=1.4 \
     -dPDFSETTINGS=/ebook \
     -dAutoRotatePages=/None \
     -dNOPAUSE \
     -dQUIET \
     -dBATCH \
     -sOutputFile=out.pdf in.pdf
     
// -dCompressFonts=true
// -r150

▶ gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dCompressFonts=true -dPDFSETTINGS=/ebook -dAutoRotatePages=/None -dNOPAUSE -dQUIET -dBATCH -sOutputFile=out.pdf in.pdf
```

### Problem

```
// When dealing with monochrome images
The only Downsample filter for monochrome images is Subsample, ignoring request.
```

## JavaScript inside PDF

Don't be surprise when you open a PDF inside a browser, it automatically display a Print dialog for you.

Can we strip off all JavaScript inside PDF? Is it a security concern?

```
<<
/Type /Action
/S /JavaScript
/JS (this.print\({bUI:true,bSilent:false,bShrinkToFit:true}\);)
>>
```

Seems like using GhostScript can remove all active content (JavaScript) and embedded data (Videos, Flash, etc.)

```
▶ gs -dSAFER -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook -dAutoRotatePages=/None -dNOPAUSE -dQUIET -dBATCH -sOutputFile=matta_fair_2019-removed.pdf matta_fair_2019.pdf
```

* [Effectiveness of flattening a PDF to remove malware](https://security.stackexchange.com/questions/103323/effectiveness-of-flattening-a-pdf-to-remove-malware)

## Prawn

* [#28 - Table overflowing without needing to?](https://github.com/prawnpdf/prawn-table/issues/10)

## Image Compression

* [image_processing - libvips](https://github.com/janko/image_processing)

```
// From PNG to JPEG
▶ convert from.png to.jpg

▶ jpegtran -copy none -optimize -progressive -outfile out.jpg in.jpg
```

