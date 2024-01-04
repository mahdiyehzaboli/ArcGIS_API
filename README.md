# ArcGIS_API
from time import strftime
print(strftime('%c'))

from arcgis.gis import GIS

### Input Variables
itemid = 'c8e1c7240b734e45bf0b3fc24bdc09ab'
output = r'D:\Baylink Networks\Mega Projects - Mega Project\Connected Coast\Site Details\00. General Blocks\Design\DataBase\Connected Coast gdb\Online Backup\Design'
tempfile = strftime('P20002__CCN__Layer__Design_%Y-%m-%d')


### Create Backup
gis = GIS('https://byl.maps.arcgis.com', 'BaylinkNetworks_Admin', 'BYLAdmin1923!')
dataitem = gis.content.get(itemid)
dataitem.export(tempfile, 'File Geodatabase', parameters = None, wait = True)
myexport = gis.content.search(tempfile, item_type = 'File Geodatabase')
fgdb = gis.content.get(myexport[0].itemid)
fgdb.download(save_path = output)
fgdb.delete()

print('Script Complete at {}'.format(strftime('%c')))
