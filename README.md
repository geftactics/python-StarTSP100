# python-StarTSPImage

**Print from Python to Star TSP100/143/650/654**

Star TSP100/TSP143 printers do not have any font sets etc on board the printer, so any data being sent directly to the printer must first be converted into a raster image using the appropriate graphic mode commands. (Star do provide a driver that emulates Star line mode commands, but we can't use this if we want to interact directly with the printer)

This project will take an image file (Either as a PIL image, or from file on disk), scale it to the appropriate width for the printer, and then create a binary output of the graphic mode raster commands, which then can be sent directly to the device. You could use `Pillow` or `imgkit` to programmatically build images.

For more detailed reading, you can find the graphic mode command manual at: http://www.starasia.com/Download/Manual/star_graphic_cm_en.pdf

## Installing
`pip install StarTSPImage`

## Examples

Print a file from disk:
```
import StarTSPImage

raster = StarTSPImage.imageFileToRaster('file.bmp', cut=True))

printer = open('/dev/usb/lp0', 'wb')
printer.write(raster)
```


Create a PIL image and print:
```
import StarTSPImage
from PIL import Image, ImageDraw

image = Image.new('RGB', (500, 500), color='White')
draw = ImageDraw.Draw(image)
draw.ellipse((10, 10, 490, 490), fill='White')

raster = StarTSPImage.imageToRaster(image, cut=True)

printer = open('/dev/usb/lp0', "wb")
printer.write(raster)
```
