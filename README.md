# En avant toute !
Ceci est un ensemble de lien et de source 

## Sommaire
 - [Boutton](#boutton)
 - [LED](#led)
 - [Écran](#écran)
 - [Moteur](#moteur)

## Boutton
```python
import digitalio

boutton = digitalio.DigitalInOut(board.GP4) # GP doit il faut choisir en fonction du cablage
boutton.direction = Direction.INPUT
boutton.pull = Pull.UP # ou bien Pull.DOWN

#Pour lire la valeur du boutton
#cela depand de la valeur du pull
# if boutton.value:
# if not boutton.value:
```

## LED
```python
import digitalio

LED = digitalio.DigitalInOut(board.GP4) # GP doit il faut choisir en fonction du cablage
LED.direction = digitalio.Direction.OUTPUT
LED.value = True # Pour allumer la led
LED.value = False # Pour éteindre la led 
```

## Écran
Pour plus d'information: https://docs.circuitpython.org/projects/st7789/en/latest/
### code
```python
import displayio
import busio

# module externe, a importé le fichier
from adafruit_st7789 import ST7789

#Connection avec l'ecran
displayio.release_displays()
bus_spi = busio.SPI(clock = board.GP18, MOSI = board.GP19)
bus_affichage = displayio.FourWire(
                                    bus_spi,
                                    command = board.GP16,
                                    chip_select=board.GP17
                                    )

ecran = ST7789(bus_affichage, width=240, height=240, rowstart=80, rotation = 180)
groupe_elements = displayio.Group()
ecran.show(groupe_elements)
```
### Cablage
Aucun cablage n'est pas nécessaire 

### Insertion d'image
```python
#image
file = open('img/Indicateur_de_vitesse.bmp', "rb")
image = displayio.OnDiskBitmap(file)
grid = displayio.TileGrid(image, pixel_shader=displayio.ColorConverter())

#ajouté l'image sur l'ecran
groupe_elements.append(grid)
```
### Dessiner une forme géometrique une forme géometrique
Pour plus d'information: https://docs.circuitpython.org/projects/display-shapes/en/latest/api.html
```python
#ceci est un exemple; N'oublie pas de charger le ficher sur la pico 
from adafruit_display_shapes.circle import Circle

circle = Circle()#N'oublié pas les coordoonées x, y, le rayon et la couleur exemple Circle(100, 100, 10, fill=0xFF00FF)

#ajouté l'image sur l'ecran
groupe_elements = displayio.Group()
groupe_elements.append(grid)
```

## Moteur
Pour plus d'information: https://docs.circuitpython.org/en/latest/shared-bindings/pwmio/index.html
```python
import pwmio
import board

mot1Moins = pwmio.PWMOut(board.GP9, frequency = 10000)
mot1Plus = pwmio.PWMOut(board.GP8, frequency = 10000)

# Le moteur, dont la valeur maximale est de 2**15
# mot1Moins est pour avancer et mot1Plus est pour reculer 
mot1Moins.duty_cycle = 0
mot1Plus.duty_cycle = 0
```
