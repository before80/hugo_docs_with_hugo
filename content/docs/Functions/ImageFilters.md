+++
title = "Image Filters"
weight = 53
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# Image Filters

[https://gohugo.io/functions/images/](https://gohugo.io/functions/images/)

The images namespace provides a list of filters and other image related functions.

See [images.Filter](https://gohugo.io/functions/images/#filter) for how to apply these filters to an image.

## Overlay 

Overlay creates a filter that overlays the source image at position x y, e.g:

```go-html-template
{{ $logoFilter := (images.Overlay $logo 50 50 ) }}
{{ $img := $img | images.Filter $logoFilter }}
```

A shorter version of the above, if you only need to apply the filter once:

```go-html-template
{{ $img := $img.Filter (images.Overlay $logo 50 50 )}}
```

The above will overlay `$logo` in the upper left corner of `$img` (at position `x=50, y=50`).

## Text 

Using the `Text` filter, you can add text to an image.

The following example will add the text `Hugo rocks!` to the image with the specified color, size and position.

```go-html-template
{{ $img := resources.Get "/images/background.png" }}
{{ $img = $img.Filter (images.Text "Hugo rocks!" (dict
    "color" "#ffffff"
    "size" 60
    "linespacing" 2
    "x" 10
    "y" 20
))}}
```

You can load a custom font if needed. Load the font as a Hugo `Resource` and set it as an option:

```go-html-template
{{ $font := resources.GetRemote "https://github.com/google/fonts/raw/main/apache/roboto/static/Roboto-Black.ttf" }}
{{ $img := resources.Get "/images/background.png" }}
{{ $img = $img.Filter (images.Text "Hugo rocks!" (dict
    "font" $font
))}}
```

## Brightness 

Brightness creates a filter that changes the brightness of an image. The percentage parameter must be in range (-100, 100).

### ColorBalance 

ColorBalance creates a filter that changes the color balance of an image. The percentage parameters for each color channel (red, green, blue) must be in range (-100, 500).

## Colorize 

Colorize creates a filter that produces a colorized version of an image. The hue parameter is the angle on the color wheel, typically in range (0, 360). The saturation parameter must be in range (0, 100). The percentage parameter specifies the strength of the effect, it must be in range (0, 100).

## Contrast 

Contrast creates a filter that changes the contrast of an image. The percentage parameter must be in range (-100, 100).

## Gamma 

Gamma creates a filter that performs a gamma correction on an image. The gamma parameter must be positive. Gamma = 1 gives the original image. Gamma less than 1 darkens the image and gamma greater than 1 lightens it.

## GaussianBlur 

GaussianBlur creates a filter that applies a gaussian blur to an image.

## Grayscale 

Grayscale creates a filter that produces a grayscale version of an image.

## Hue 

Hue creates a filter that rotates the hue of an image. The hue angle shift is typically in range -180 to 180.

## Invert 

Invert creates a filter that negates the colors of an image.

## Pixelate 

Pixelate creates a filter that applies a pixelation effect to an image.

## Saturation 

Saturation creates a filter that changes the saturation of an image.

## Sepia 

Sepia creates a filter that produces a sepia-toned version of an image.

## Sigmoid 

Sigmoid creates a filter that changes the contrast of an image using a sigmoidal function and returns the adjusted image. It’s a non-linear contrast change useful for photo adjustments as it preserves highlight and shadow detail.

## UnsharpMask 

UnsharpMask creates a filter that sharpens an image. The sigma parameter is used in a gaussian function and affects the radius of effect. Sigma must be positive. Sharpen radius roughly equals 3 * sigma. The amount parameter controls how much darker and how much lighter the edge borders become. Typically between 0.5 and 1.5. The threshold parameter controls the minimum brightness change that will be sharpened. Typically between 0 and 0.05.

## Other Functions 

### Filter 

Can be used to apply a set of filters to an image:

```go-html-template
{{ $img := $img | images.Filter (images.GaussianBlur 6) (images.Pixelate 8) }}
```

Also see the [Filter Method](https://gohugo.io/content-management/image-processing/#filter).

### ImageConfig 

Parses the image and returns the height, width, and color model.

The `imageConfig` function takes a single parameter, a file path (*string*) relative to the *project’s root directory*, with or without a leading slash.

```go-html-template
{{ with (imageConfig "favicon.ico") }}
favicon.ico: {{ .Width }} x {{ .Height }}
{{ end }}
```

## 另请参阅

- [Image Processing](https://gohugo.io/content-management/image-processing/)
