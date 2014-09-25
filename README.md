##fontrendering

When rendering fonts on the HTML canvas you get different results in different browsers, varying from OK to awful.

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/chrome_plain.png)  
*chrome*

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ie_plain.png)  
*internet explorer*

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ff_plain.png)  
*firefox*

The rendered fonts employ anti-aliasing, but not sub-pixel rendering. When we apply sub-pixel rendering we get the following.

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/chrome_subpixel.png)  
*chrome*

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ie_subpixel.png)  
*internet explorer*

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ff_subpixel.png)  
*firefox*

The outputs are now fairly uniform and very smooth. Even the smallest fontsize (8px) is readable.

###the code
To achieve the sub-pixel rendering the font is rendered on a hidden canvas scaled up three times (i.e. a fontsize of 10px becomes 30px). This resulting image is then scaled back down and written to the visible, normal sized canvas. This means 9 pixels are scaled to 1 pixel but with the understanding that the 1 pixel consists of 3 sub-pixels (RGB assumed). In the vertical direction the pixel values are simply averaged. In the horizontal direction 5 pixels are combined using a weighted average to populate 1 sub-pixel. The 15 pixel matrix for 1 sub-pixel is (divided by 27 to normalize):
```
1 2 3 2 1
1 2 3 2 1
1 2 3 2 1
         /27
```

The weights come about by spreading a sub-pixel out twice:
```
    9      original pixel
  3 3 3    spread out once
1 2 3 2 1  spread out twice
```
The first spreading ensures on average the colour is still black on white, the second spreading ensure more weight on the centre pixel undoing some of the resulting smoothing effect.