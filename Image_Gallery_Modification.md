# Modifying the Image Gallery in the eBay Template

This guide explains how to add or remove images from the 8-image gallery in the eBay listing template (`WIP.html`).

## Current Setup
The template currently has 8 images in the gallery. Each image consists of:
- A thumbnail for navigation
- A main image view with zoom functionality
- Navigation arrows (prev/next)
- Image counter (e.g., "1 of 8")

## Special Case: Single Image
If you only have one image:
1. Keep only the first `<div class="image" ...>` block.
2. Remove the `<label for="thumbnail-control-2" class="next"></label>` (since there's no next).
3. Optionally, remove the prev label as well, or leave it pointing to itself if you want a loop.
4. Update the count to "1 of 1".
5. The zoom icon and close button remain functional.
6. On mobile, swipe gestures won't navigate since there's only one image.

## Adding More Images
1. **Duplicate an existing image div**: Copy one of the `<div class="image" ...>` blocks (from `<div class="image" data-image="images/...">` to `</div>`).

2. **Update the data-image attribute**: Change `data-image="images/YOUR_NEW_IMAGE.jpg"` to your new image filename.

3. **Update IDs and labels**:
   - Change `id="thumbnail-control-X"` to the next number (e.g., 9 for the 9th image).
   - Change `id="thumbnail-X"` and `for="thumbnail-control-X"`.
   - Change `id="image-control-X"` and `for="image-control-X"`.
   - Change `id="image-X"` and `for="image-control-X"`.
   - Update `label for="thumbnail-control-Y"` where Y is the previous/next image number.

4. **Update navigation labels**:
   - For prev: `label for="thumbnail-control-(X-1)" class="prev"`
   - For next: `label for="thumbnail-control-(X+1)" class="next"` (or loop back to 1 if it's the last).

5. **Update the count span**: Change `<span data-count="images/...">8</span>` to the new total number.

6. **Update the first image's next label**: If adding after the last, update the last image's next to point to the new one, and the new one's next to 1.

## Removing Images (for Lower Numbers)
1. **Delete the image div**: Remove the entire `<div class="image" ...>` block for the image you want to remove.

2. **Update IDs and references**: Renumber the remaining images sequentially starting from 1.

3. **Update navigation**: Ensure prev/next labels point to the correct remaining images. For the first image, prev should point to the last (for looping). For the last, next to 1.

4. **Update count**: Change the total count in all `<span data-count="...">X</span>` to the new number.

5. **Handle low numbers**: With 2-3 images, the navigation will loop. With 1, see special case above.

## Important Notes
- Image files should be placed in the `images/` folder.
- Ensure all IDs are unique.
- Test the gallery on different screen sizes, especially mobile for swipe functionality.
- The JavaScript for swipe gestures assumes the structure; if you change the number significantly, you may need to adjust the script.

## Example: Adding a 9th Image
After the 8th image div, add:

```html
<div class="image" data-image="images/YOUR_IMAGE_9.jpg">
    <input id="thumbnail-control-9" type="radio" name="thumbnails" class="thumbnails-control" />
    <label for="thumbnail-control-9" id="thumbnail-9" class="thumbnail">
        <img src="images/YOUR_IMAGE_9.jpg" alt="Thumbnail 9" />
    </label>

    <input id="image-control-9" type="checkbox" class="main-control">
    <label for="image-control-9" id="image-9" class="main transition">
        <div class="main-content">
            <img src="images/YOUR_IMAGE_9.jpg" alt="Title" />
            <div class="zoom-icon"></div>
            <label for="image-control-9" class="close-button"></label>
            <label for="thumbnail-control-8" class="prev"></label>
            <label for="thumbnail-control-1" class="next"></label>
            <div class="count-label">
                <div>9 of</div>
                <div><span data-count="images/YOUR_IMAGE_9.jpg">9</span></div>
            </div>
        </div>
    </label>
</div>
```

Then update all count spans to 9, and adjust the 8th image's next to 9, and 9th's next to 1.