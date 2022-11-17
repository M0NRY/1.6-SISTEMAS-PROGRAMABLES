# 1.6-SISTEMAS-PROGRAMABLES

*PANTALLA OLED*

**CODIGO:**

```

import board
import displayio
import terminalio
import busio
from adafruit_display_text import label
import adafruit_displayio_ssd1306
import time

displayio.release_displays()


i2c = busio.I2C(scl=board.GP21, sda=board.GP20)
display_bus = displayio.I2CDisplay(i2c, device_address=0x3C)

WIDTH = 128
HEIGHT = 64
BORDER = 5

display = adafruit_displayio_ssd1306.SSD1306(display_bus, width=WIDTH, height=HEIGHT)


splash = displayio.Group()
display.show(splash)

color_bitmap = displayio.Bitmap(WIDTH, HEIGHT, 1)
color_palette = displayio.Palette(1)
color_palette[0] = 0xFFFFFF  # White

bg_sprite = displayio.TileGrid(color_bitmap, pixel_shader=color_palette, x=0, y=0)
splash.append(bg_sprite)


inner_bitmap = displayio.Bitmap(WIDTH - BORDER * 2, HEIGHT - BORDER * 2, 1)
inner_palette = displayio.Palette(1)
inner_palette[0] = 0x000000  # Black
inner_sprite = displayio.TileGrid(
    inner_bitmap, pixel_shader=inner_palette, x=BORDER, y=BORDER
)
splash.append(inner_sprite)


text = "HOLA NOMAS :("
text_area = label.Label(
    terminalio.FONT, text=text, color=0xFFFFFF, x=28, y=HEIGHT // 2 - 1
)
splash.append(text_area)
display.refresh()

print("Done! Press Ctrl+C to get into the REPL")
while True:
    time.sleep(1)

```

![ezgif com-gif-maker](https://user-images.githubusercontent.com/112371036/202580806-16ac2651-4e04-48e0-a481-76dc129ab04a.gif)
