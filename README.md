fontrendering
-------------

When rendering fonts on the HTML canvas you get different results in different browsers, varying from OK to awful.

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/chrome_plain.png)  
chrome

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ie_plain.png)  
internet explorer

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ff_plain.png)  
firefox

The rendered fonts employ anti-aliasing, but not sub-pixel rendering. When we apply sub-pixel rendering we get the following.

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/chrome_subpixel.png)  
chrome

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ie_subpixel.png)  
internet explorer

![examples](https://raw.githubusercontent.com/rodinhart/fontrendering/master/ff_subpixel.png)  
firefox

The outputs are now fairly uniform and very smooth. Even the smallest fontsize (8px) is readable.

(code explanation coming...)