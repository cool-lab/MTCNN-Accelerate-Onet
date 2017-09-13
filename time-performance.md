# Time performance

Test on Tesla P40, loop each image for 100 times.

1. With original ONet

1.1 minSize=15, GPU Mem 573MiB

```
0_Parade_marchingband_1_364.jpg size: 1024 x 732
Test for 100 loops, takes 68.1018 second, average time: 0.681018s
0_Parade_marchingband_1_408.jpg size: 1024 x 706
Test for 100 loops, takes 76.2543 second, average time: 0.762543s
img_591.jpg size: 450 x 431
Test for 100 loops, takes 16.8168 second, average time: 0.168168s
img_534.jpg size: 410 x 312
Test for 100 loops, takes 21.7024 second, average time: 0.217024s
img_561.jpg size: 292 x 450
Test for 100 loops, takes 12.3542 second, average time: 0.123542s
img_769.jpg size: 318 x 450
Test for 100 loops, takes 14.2046 second, average time: 0.142046s
img_78.jpg size: 450 x 448
Test for 100 loops, takes 25.249 second, average time: 0.25249s
```

minSize=15, GPU Mem 513~601MiB
```
img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 35.5166 second, average time: 0.355166s
got_1280x720.jpg
img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 73.6084 second, average time: 0.736084s
```

minSize=15, On XPS-9550
```
got_640x480.jpg
../img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 10.3145 second, average time: 0.103145s
got_1280x720.jpg
../img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 15.7854 second, average time: 0.157854s
```

1.2 minSize=40, GPU Mem 485MiB

```
0_Parade_marchingband_1_364.jpg size: 1024 x 732
Test for 100 loops, takes 24.1231 second, average time: 0.241231s
0_Parade_marchingband_1_408.jpg size: 1024 x 706
Test for 100 loops, takes 25.3205 second, average time: 0.253205s
img_591.jpg size: 450 x 431
Test for 100 loops, takes 7.51142 second, average time: 0.0751142s
img_534.jpg size: 410 x 312
Test for 100 loops, takes 6.55217 second, average time: 0.0655217s
img_561.jpg size: 292 x 450
Test for 100 loops, takes 5.49258 second, average time: 0.0549258s
img_769.jpg size: 318 x 450
Test for 100 loops, takes 7.21874 second, average time: 0.0721874s
img_78.jpg size: 450 x 448
Test for 100 loops, takes 8.3752 second, average time: 0.083752s
```

minSize=40, GPU Mem 395~477MiB
```
img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 21.3552 second, average time: 0.213552s
got_1280x720.jpg
img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 26.5001 second, average time: 0.265001s
```

minSize=40, On XPS-9550
```
got_640x480.jpg
../img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 6.14451 second, average time: 0.0614451s
got_1280x720.jpg
../img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 7.50647 second, average time: 0.0750647s
```

2. With half-sized ONet

2.1 minSize=15, GPU Mem 511MiB

```
0_Parade_marchingband_1_364.jpg size: 1024 x 732
Test for 100 loops, takes 65.9016 second, average time: 0.659016s
0_Parade_marchingband_1_408.jpg size: 1024 x 706
Test for 100 loops, takes 72.1371 second, average time: 0.721371s
img_591.jpg size: 450 x 431
Test for 100 loops, takes 16.6591 second, average time: 0.166591s
img_534.jpg size: 410 x 312
Test for 100 loops, takes 20.9826 second, average time: 0.209826s
img_561.jpg size: 292 x 450
Test for 100 loops, takes 12.6265 second, average time: 0.126265s
img_769.jpg size: 318 x 450
Test for 100 loops, takes 14.2025 second, average time: 0.142025s
img_78.jpg size: 450 x 448
Test for 100 loops, takes 25.0197 second, average time: 0.250197s
```

minSize=15, GPU Mem 539MiB
```
img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 34.3745 second, average time: 0.343745s
got_1280x720.jpg
img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 72.4398 second, average time: 0.724398s
```

minSize=15, On XPS-9550
```
got_640x480.jpg
../img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 9.59571 second, average time: 0.0959571s
got_1280x720.jpg
../img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 14.629 second, average time: 0.14629s
```

2.2 minSize=40, GPU Mem 423MiB

```
0_Parade_marchingband_1_364.jpg size: 1024 x 732
Test for 100 loops, takes 22.8825 second, average time: 0.228825s
0_Parade_marchingband_1_408.jpg size: 1024 x 706
Test for 100 loops, takes 23.2721 second, average time: 0.232721s
img_591.jpg size: 450 x 431
Test for 100 loops, takes 7.46511 second, average time: 0.0746511s
img_534.jpg size: 410 x 312
Test for 100 loops, takes 6.64397 second, average time: 0.0664397s
img_561.jpg size: 292 x 450
Test for 100 loops, takes 5.54881 second, average time: 0.0554881s
img_769.jpg size: 318 x 450
Test for 100 loops, takes 7.76955 second, average time: 0.0776955s
img_78.jpg size: 450 x 448
Test for 100 loops, takes 8.37166 second, average time: 0.0837166s
```

minSize=40, GPU Mem 415~431MiB
```
img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 21.1098 second, average time: 0.211098s
got_1280x720.jpg
img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 26.2878 second, average time: 0.262878s
```

minSize=40, On XPS-9550
```
got_640x480.jpg
../img2/got_640x480.jpg size: 640 x 480
Test for 100 loops, takes 5.47882 second, average time: 0.0547882s
got_1280x720.jpg
../img2/got_1280x720.jpg size: 1280 x 720
Test for 100 loops, takes 6.68324 second, average time: 0.0668324s
```
