# Camera_Wave_Analysis
Scripts and ideas on wave analysis from a single video camera

## Split MP4 file into .jpeg files

```
ffmpeg -i rec25.mp4 -r  4 -f image2 image-%3d.jpeg
```

## Selecy x,y coordinate of points of interest

```
import imageio
import matplotlib.pyplot as plt
import numpy as np

# Poste: x = 748, y = 1500-1530
# Virtual Buoy: X = 1200, y = 1500

bv1=[]
poste=[]
for i in range(241):
   m = i+1
   print(m)
   if m < 10:
      filename = 'image-00' + str(m) + '.jpeg'
   if m > 9 and m < 100:
      filename = 'image-0'  + str(m) + '.jpeg'
   if m > 99:
      filename = 'image-'   + str(m) + '.jpeg'
#   print(filename)
   pic = imageio.imread(filename) # 2560 1920 (x,y)
                             #  Origin in UL corner
   bv1_aux = pic[1200,1500]  #
   poste_aux = pic[748,1500:1530,[0,1,2]]
   
#   print(bv1_aux) 
   bv1.append(bv1_aux)
   poste.append(poste_aux)

bv01=np.asarray(bv1)
poste01=np.asarray(poste)

print(bv01.shape)    # (241,3)
print(poste01.shape) # (241,30,3)

plt.plot(bv01[:,0])
plt.show()
```

Obtainig:

![Time Series at Virtual Buoy](plots/ts_vb.png?raw=true "Time Series at Virtual Buoy 01")
