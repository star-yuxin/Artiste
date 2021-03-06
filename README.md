[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-Artiste-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/1177)

Artiste
=======

Android library for drawing shapes on a canvas

<img src="https://raw.githubusercontent.com/mattlogan/Artiste/master/github_assets/artiste_shapes.png" width="350"/>

## Add as Dependency

Artiste is on jCenter.

```groovy
repositories {
    jcenter()
}
```

```groovy
dependencies {
    compile 'me.mattlogan.artiste:artiste:2.0.0'
}
```

## Overview

In a `View` class, create a subclass of `Shape`.

```java
fivePointedStar = new FivePointedStar();
```

Call `calculatePath(Rect rect, float rotationDegrees)` to create the `Shape`'s `Path`.

```java
@Override
protected void onSizeChanged(int w, int h, int oldw, int oldh) {
    super.onSizeChanged(w, h, oldw, oldh);
    fivePointedStar.calculatePath(new Rect(0, 0, w, h), 10);
}
```

Get your `Shape`'s `Path` with `getPath()`, and draw it on a `Canvas`.

```java
@Override
protected void onDraw(Canvas canvas) {
    super.onDraw(canvas);
    canvas.drawPath(fivePointedStar.getPath(), paint);
}
```

## Ready-made Shapes

The `Shapes` class contains some ready-made shapes: `Triangle`, `Square`, `Pentagon`, `Hexagon`, `FivePointedStar`, and `Circle`. These shapes are interchangeable and can be used as in the example above.

`Triangle`, `Square`, `Pentagon`, and `Hexagon` inherit from `RegularConvexPolygon`, which inherits from `Shape`.

`FivePointedStar` inherits from `RegularStarPolygon`, which also inherits from `Shape`.

`Circle` inherits directly from `Shape`.

## Configuration

Any `Shape` can be rotated with the `rotationDegrees` parameter of `calculatePath(Rect rect, float rotationDegrees)`.

Any subclass of `RegularStarPolygon`, including `FivePointedStar`, can be drawn with strokes connecting each vertex or with only the outline of the star. This is set by overriding `isOutlined(boolean outlined)`.

For example, the value of `outlined` for the red five-pointed star above is `true`. For the green eight-pointed star above, it's `false`.

## Unlimited Shapes

To create a new shape, extend `RegularConvexPolygon` or `RegularStarPolygon` if the shape you wish to draw is either of these kinds of shapes (search for "Regular Polygon" on Wikipedia for reference). For example:

```java
public static class Tridecagon extends RegularConvexPolygon {
    @Override
    public int getNumberOfSides() {
        return 13;
    }
}

public static class Octagram extends RegularStarPolygon {
    @Override
    public int getNumberOfPoints() {
        return 8;
    }
    
    @Override
    public int getDensity() {
        return 3;
    }

    @Override
    public boolean isOutlined() {
        return false;
    }
}
```

*Note: the "density" of a regular star polygon is the number of vertices, or points, to skip when drawing a line connecting two vertices. For example, one line of a five-pointed star starts at the first vertex, skips the second vertex (moving CW or CCW), and connects with the third vertex. Thus, a five-pointed star has a density of two.*

If your shape is not a regular convex polygon or a regular star polygon, you can directly extend `Shape`. This is a little trickier. Look at `RegularConvexPolygon`, `RegularStarPolygon`, or `Circle` for guidance.

## License

```
The MIT License (MIT)

Copyright (c) 2014 Matthew Logan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
