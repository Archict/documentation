# Brick

In Archict a Brick is a composer package consisting of a collection of [Service](./services.md) and [Event](./events.md). Through [Archict/Core](../bricks/core.md) (which is also a Brick) they can be loaded and interact between them.

In the rest of this documentation all core features are described. Some features from official Bricks are also detailled.

## Create a Brick

Creating a Brick is pretty simple. A template is provided on Github <https://github.com/Archict/brick-template>, but it is also possible to begin from scratch.

As said previously, a Brick is a composer package. But there is 2 points to respect:

1. The composer package type MUST be `archict-brick`. Unless Core will not be able to load it
2. It SHOULD require package `archict/brick`. It's not mandatory but interface to create Service will not be available.

And that's all!
