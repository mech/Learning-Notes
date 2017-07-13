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

## Image Compression

```
// From PNG to JPEG
▶ convert from.png to.jpg

▶ jpegtran -copy none -optimize -progressive -outfile out.jpg in.jpg
```