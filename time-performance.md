# Time performance

Test on Tesla P40, loop each image for 100 times.

1. With original ONet

GPU Mem 573MiB

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

2. With half-sized ONet

GPU Mem 511MiB

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