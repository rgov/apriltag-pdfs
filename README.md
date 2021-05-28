# AprilTag PDFs

This repository contains pre-generated PDFs of [AprilTag 3][apriltags] tags. Currently available tags are from the `tag36h11` family, in sizes of 100mm and 200mm, in US Letter and A4 paper sizes.

  [apriltags]: https://github.com/AprilRobotics/apriltag


## Generation

The tags were converted from PNG source files from the [apriltag-imgs][] repository using [ImageMagick][]. Thanks to @cbteeple for initially developing the technique.

  [apriltag-imgs]: https://github.com/AprilRobotics/apriltag-imgs
  [ImageMagick]: https://imagemagick.org/

To reproduce these files you may need to [modify the ImageMagick security policy][policy] to allow writing PDFs.

  [policy]: https://imagemagick.org/script/security-policy.php

The following command creates 300dpi, 8.5 x 11in (US Letter) PDF. The 10-pixel wide tag is scaled to be 200mm. (The constant 25.4 is the conversion factor from inches to mm.) It also adds a thin border around the tag and writes some reference information 0.25in from the bottom of the page; these features can be omitted by deleting the corresponding lines.

    convert tag36h11/tag36_11_00005.png \
        -density 300 \
        -scale $((100 * 200./10 * 300/25.4))% \
        -bordercolor black -border 1 \
        -gravity center -extent $((300*8.5))x$((300*11)) \
        -gravity south -annotate +0+$((300*0.25)) 'AprilTag family = tag36h11, size = 200 mm, id = 5' \
        tag.pdf

For A4-sized PDFs, a density of 120 dots per cm is used.
