# Imagemagick

Install imagemagick

# Convert PDF to other

`convert doc.pdf doc.jpg`

If you get an error like

    convert: unable to load module `/usr/lib/ImageMagick-6.9.7//modules-Q16HDRI/coders/pdf.la': file not found @error/module.c/OpenModule/1302.
    convert: no decode delegate for this image format `PDF' @ error/constitute.c/ReadImage/504.
    convert: no images defined `teatowel.tif' @ error/convert.c/ConvertImageCommand/3258.

Then install ghostscript. See [here](https://www.imagemagick.org/discourse-server/viewtopic.php?t=25823)

e.g.
`sudo apt-get install ghostscript`
