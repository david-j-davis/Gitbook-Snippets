# HTML5

Example:

```<video autoplay loop poster="polina.jpg" class="bgvid">
<source src="polina.webm" type="video/webm">
<source src="polina.mp4" type="video/mp4">
</video>```

```video.bgvid {
position: fixed; right: 0; bottom: 0;
min-width: 100%; min-height: 100%;
width: auto; height: auto; z-index: -100;
background: url(polina.jpg) no-repeat;
background-size: cover;
}```

```<!--[if lt IE 9]>
<script>
document.createElement('video');
</script>
<![endif]-->```

And, inside your CSS, a declaration that allows IE to understand that this is a block-level element:

video { display: block; }
With these in place, IE8 can at least style the <video> element with a background image.

While it is possible to feature-detect support for video autoplay with JavaScript (a technique I will cover in a future article), the easiest solution is to use a media query that switches off the video entirely on smaller screens, substituting the placeholder image in the background. To the existing CSS, add:

    @media screen and (max-device-width: 800px) {

    html { background: url(polina.jpg) #000 no-repeat center center fixed;}

    .bgvid { display: none; }

    }


