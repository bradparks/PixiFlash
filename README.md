# PIXI Flash [![Build Status](https://travis-ci.org/SpringRoll/PixiFlash.svg)](https://travis-ci.org/SpringRoll/PixiFlash) [![Dependency Status](https://david-dm.org/SpringRoll/PixiFlash.svg)](https://david-dm.org/SpringRoll/PixiFlash)

A library for bridging CreateJS animations from Flash for use in PIXI. Publish Flash content like you normally would for CreateJS, but export for Flash. There can be _no_ vectors used, this publishing process only supports bitmaps, movieclips and timeline animations.

## Flash Publishing 

### Installing

Install the post-publish tool by running **tools/install.jsfl**. This will allow for some error checking when publishing for PIXI Flash.

### Flash Setup

* Make sure you use a Flash "HTML5 Canvas" document type 
* Change the publishing settings under JavaScript Namespaces
 * Symbols: **pixiflash_lib**
 * Images: **pixiflash_images**
 * CreateJS: **pixiflash**
* Publishing document

## Running Content

### Installing Library

To run content exported with PixiFlash, you must load the JavaScript library within your project. You can install using [Bower](http://bower.io):

```
bower install pixi-flash
```

### Dependencies

* [Pixi.js](http://pixijs.com) is required
* [TweenJS](http://createjs.com/tweenjs) is a dependency for doing timeline animation


### Example

Here's a example using PIXI where the images were assembled using TexturePacker. See the **example** folder for an example which uses the Flash SpriteSheet exporting.

```js
var renderer = new PIXI.autoDetectRenderer(800, 500);
var stage = new PIXI.Container();

// Load the atlas for the character
var loader = new PIXI.loaders.Loader();

// This atlas is created with TexturePacker from the 
// output individual images from Flash publishing
loader.add('CharacterAtlas',"CharacterAtlas.json");
loader.once('complete',function(loader, resources)
{
	// Assign the atlas to global images in pixiflash_images
	pixiflash.utils.addImages(resources.CharacterAtlas);

	// Create the character, all library symbols live
	// on the pixiflash_lib window object
	var character = new pixiflash_lib.Character();
	character.framerate = 30;
	character.play();

	// Add to stage
	stage.addChild(character);
});
loader.load();

// Normal render
update();
function update()
{
    requestAnimationFrame(update);
    renderer.render(stage);
}
```

##License

Copyright (c) 2015 [CloudKid](http://github.com/cloudkidstudio)

Released under the MIT License.
