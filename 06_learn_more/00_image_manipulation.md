# Image manipulation

--------------------------------------------------------

* [Usage](#usage)

--------------------------------------------------------

The pixl library allows you to manipulate images through a consistent API using either GD or ImageMagick.

--------------------------------------------------------

<a id="usage"></a>

### Usage

First you'll have to decide whether to use GD or ImageMagick. In this example we'll use GD.

	$image = new Image('my_image.png', new GD);

> You can use the same processor instance for multiple images

The ```rotate``` method allows you to rotate an image n degrees.

	$image->rotate(90);

The ```resize``` method allows you to resize an image.

	// Resize to 50% of original size

	$image->resize(50);

	// Resize to 300 x 300 pixels

	$image->resize(300, 300);

	// Resize to closest possible match while maintaining aspect ratio

	$image->resize(300, 300, Image::RESIZE_AUTO);

	// Base new size on given width while maintaining aspect ratio

	$image->resize(300, 300, Image::RESIZE_WIDTH);

	// Base new size on given height while maintaining aspect ratio

	$image->resize(300, 300, Image::RESIZE_HEIGHT);

The ```crop``` method allows you to crop an image. The two first parameters are the crop size while the last two are the X and Y coordinates of the cropped region's top left corner.

	$image->crop(200, 200, 50, 50);

The ```flip``` method allows you to flip and image.

	$image->flip();

	// Flip the image vertiaclly

	$image->flip(Image::FLIP_VERTICAL);

The ```watermark``` method allows you to add a watermark to your image.

	$image->watermark('watermark.png');

	// You can also position the watermark (default is top left)

	$image->watermark('watermark.png', Image::WATERMARK_TOP_RIGHT);

	$image->watermark('watermark.png', Image::WATERMARK_BOTTOM_LEFT);

	$image->watermark('watermark.png', Image::WATERMARK_BOTTOM_RIGHT);

	$image->watermark('watermark.png', Image::WATERMARK_CENTER);

	// You can also set the watermark opacity in percent

	$image->watermark('watermark.png', Image::WATERMARK_BOTTOM_RIGHT, 50);

The ```greyscale``` method converts the image to greyscale.

	$image->greyscale();

The ```colorize``` method allows you to colorize an image.

	$image->colorize('FF0000');

The ```getImageBlob``` returns the raw binary image data.

	$image = $image->getImageBlob();

	// You can also tell it to return a different image type

	$image = $image->getImageBlob('jpg');

	// You can also adjust the image quality in percent (default is 95%)

	$image = $image->getImageBlob('jpg', 70);

The ```save``` method allows you to save the image to a file.

	$image->save('edited_image.png');

	// You can also adjust the image quality in percent (default is 95%)

	$image->save('edited_image.png', 70);