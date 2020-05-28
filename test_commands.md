```
python test_background-matting_image.py -m real-fixed-cam -i data/grey/input/ -o data/grey/output/ -tb data/grey/background/ -b data/grey/teaser_back.png
```

ffmpeg -r 29.97 -f image2 -i output/%04d_matte.png -vcodec libx264 -crf 15 -pix_fmt yuv420p teaser_matte.mp4
ffmpeg -r 29.97 -f image2 -i output/%04d_compose.png -vcodec libx264 -crf 15 -pix_fmt yuv420p teaser_compose.mp4

ffmpeg -f concat -i files.txt -c copy background.mp4

ffmpeg -ss 2:0 -i milkyway.webm -vf scale=1080:-1 miklyway/%04d_img.png -hide_banner

ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=s=x:p=0 milkyway.webm


python test_background-matting_image.py -m real-fixed-cam -i data/grey/input/ -o data/grey/output/ -tb data/grey/milkyway/ -b data/grey/teaser_back.png


ffmpeg -r 29.97 -f image2 -i _output3/%04d_matte.png -vcodec libx264 -crf 15 -pix_fmt yuv420p teaser_matte3.mp4
ffmpeg -r 29.97 -f image2 -i _output3/%04d_compose.png -vcodec libx264 -crf 15 -pix_fmt yuv420p teaser_compose3.mp4

Traceback (most recent call last):
  File "test_background-matting_image.py", line 122, in <module>
    bbox=get_bbox(rcnn,R=bgr_img0.shape[0],C=bgr_img0.shape[1])
  File "/home/tetsu/github/Background-Matting/functions.py", line 38, in get_bbox
    x1, y1 = np.amin(where, axis=1)
  File "<__array_function__ internals>", line 6, in amin
  File "/home/tetsu/anaconda3/envs/Background-Matting/lib/python3.6/site-packages/numpy/core/fromnumeric.py", line 2746, in amin
    keepdims=keepdims, initial=initial, where=where)
  File "/home/tetsu/anaconda3/envs/Background-Matting/lib/python3.6/site-packages/numpy/core/fromnumeric.py", line 90, in _wrapreduction
    return ufunc.reduce(obj, axis, dtype, out, **passkwargs)
ValueError: zero-size array to reduction operation minimum which has no identity

ffmpeg -r 29.97 -f image2 -i output/%04d_matte.png -vcodec libx264 -crf 15 -pix_fmt yuv420p teaser_matte4.mp4
ffmpeg -r 29.97 -f image2 -i output/%04d_compose.png -vcodec libx264 -crf 15 -pix_fmt yuv420p teaser_compose4.mp4

python test_background-matting_image.py -m real-fixed-cam -i data/blue/input/ -o data/blue/output/ -tb data/blue/background/ -b data/blue/blue_back.png

ffmpeg -r 29.97 -f image2 -i output/%04d_matte.png -vcodec libx264 -crf 15 -pix_fmt yuv420p blue_matte.mp4
ffmpeg -r 29.97 -f image2 -i output/%04d_compose.png -vcodec libx264 -crf 15 -pix_fmt yuv420p blue_compose.mp4

## manako

Split video into images

```
cd data/manako
ffmpeg -i manako.webm -vf scale=1080:-1 input/%04d_img.png -hide_banner
cd ../..
```

create human segmentation masks

```
python test_segmentation_deeplab.py -i data/manako/input
```

Background matting

```
python test_background-matting_image.py -m real-fixed-cam -i data/manako/input/ -o data/manako/output/ -tb data/manako/background/ -b data/manako/manako_back.png
```