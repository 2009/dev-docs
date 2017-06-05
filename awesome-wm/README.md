# Awesome Window Manager

### TODO
* [ ] Add details on manually creating a cairo pattern and link (Colors section).
* [X] Complete shape section (shape function)
* [ ] Complete image section (image file or cairo surface)
* [ ] Consider adding images examples

## Modifying the Theme

> See: [Change Awesome appearance](https://awesomewm.org/doc/api/documentation/06-appearance.md.html)

Awesome has a lot of theme variables to allow you to customize the look of awesome, all theme variables are stored in the `beautiful` module. See the above link for the list.

Below I have listed what format the different variable types you will encounter expect.

### Colors

> See: [gears.color](https://github.com/awesomeWM/awesome/blob/master/lib/gears/color.lua)

Theme variables that expect a color will accept anything that can be passed as an argument to `gears.color()` or a cairo pattern, which happens to be the return value of calling the `gears.color()` function.

Arguments to `gears.color()` are specified in the format `type:arguments` with `arguments` depending on the type.
Alternatively, you can specify them as **table** rather than a **string** like so:

```lua
-- Here 'color' is an argument for type 'solid'
theme.bg_normal = {
  type = 'solid',
  color = '#FF0000'
}
```

#### solid

These are your standard HTML colors `#rrggbb` or with alph `#rrggbbaa`.

```lua
-- shortended version
theme.bg_normal = "#FF0000"

-- string version
theme.bg_normal = "solid:#FF0000"

-- table version
theme.bg_normal = {
  type = "solid",
  color = "#FF0000"
}
```

#### png

From an image file.

```lua
-- string version
theme.bg_normal = "png:/path/to/image.png"

-- table version
theme.bg_normal = {
  type = "png",
  file = "/path/to/image.png"
}
```

#### radial

As a radial gradient.

```lua
-- string version
-- "radial:x0,y0,r0:x1,y1,r1:<stops>"
-- `x0,y0` and `x1,y1` are the start and stop point of the pattern.
-- `r0` and `r1` are the radii of the start / stop circle.
-- <stops> specifies the color stops for the radial pattern and are
-- in the form place,color where place is between 0 and 1.
theme.bg_normal = "radial:20,20,10:20,20,30:0,#FF0000:0.5,#00FF00:1,#0000FF"

-- table version
-- { type = "radial", from = { x0, y0, r0 }, to = { x1, y1, r1 },
--   stops = { <stops> } }
theme.bg_normal = {
  type = "radial",
  from = { 20, 20, 10 },
  to = { 20, 20, 30 },
  stops = { { 0, "#FF0000" }, { 0.5, "#00FF00" }, { 1, "#0000FF" } }
}
```

#### linear

As a linear gradient.

```lua
-- string version
-- "radial:x0,y0:x1,y1:<stops>"
-- `x0,y0` and `x1,y1` are the start and stop point of the pattern.
-- <stops> specifies the color stops for the radial pattern and are
-- in the form place,color where place is between 0 and 1.
theme.bg_normal = "linear:20,20:100,100:0,#FF0000:0.5,#00FF00:1,#0000FF"

-- table version
-- { type = "linear", from = { x0, y0 }, to = { x1, y1 },
--   stops = { <stops> } }
theme.bg_normal = {
  type = "linear",
  from = { 20, 20 },
  to = { 100, 100 },
  stops = { { 0, "#FF0000" }, { 0.5, "#00FF00" }, { 1, "#0000FF" } }
}
```

### Shape

A shape can be set to a function to allow you to set the shape of widgets, it takes three argument `(cr, width, height)` where `cr` is the cairo context, `width` and `height` are the width and height of the widget.

Reading about [Cairo's Drawing Model](https://www.cairographics.org/tutorial/#L1drawingmodel) can help you understand
how the shape will be used. Whatever shape you draw will essentially become the **mask** layer for the widget.

> See [Using Cairo in Awesome](https://awesomewm.org/doc/api/documentation/16-using-cairo.md.html) on details about
> how to require cairo and translating the cairo api to lua.

```lua
-- Set some color variables
theme.bg_normal = "#FF0000"
theme.taglist_bg_focus = "#0000FF"

-- Change the shape of tags in the taglist to a rounded rectangle
theme.taglist_shape = function(cr, width, height)
    radius = 20

    if width / 2 < radius then
        radius = width / 2
    end

    if height / 2 < radius then
        radius = height / 2
    end

    cr:move_to(0, radius)

    cr:arc( radius      , radius       , radius,    math.pi   , 3*(math.pi/2) )
    cr:arc( width-radius, radius       , radius, 3*(math.pi/2),    math.pi*2  )
    cr:arc( width-radius, height-radius, radius,    math.pi*2 ,    math.pi/2  )
    cr:arc( radius      , height-radius, radius,    math.pi/2 ,    math.pi    )

    cr:close_path()
end
```

> For an intro into drawing things with cairo see: [Drawing with Cairo](https://www.cairographics.org/tutorial/#L1drawing).  
> Also see: [Cairo Documentation](https://www.cairographics.org/documentation/) for tutorial, FAQs and API reference.

For examples of shape functions check out [gears.shape](https://github.com/awesomeWM/awesome/blob/master/lib/gears/shape.lua), you can use these functions directly:

```lua
theme.taglist_shape = function(cr, width, height)
  local radius = 20
  return gears.shape.rounded_rect(cr, width, height, radius)
end
```

### Image

Image file or **SURFACE**

Examples of creating surfaces: [https://github.com/awesomeWM/awesome/blob/master/lib/beautiful/theme_assets.lua](https://github.com/awesomeWM/awesome/blob/master/lib/beautiful/theme_assets.lua)
