
**********************
Freestyle SVG Exporter
**********************

SVG exporting for Freestyle is available through an addon.

.. figure:: /images/render-freestyle_svg_car.png
   :width: 600px
   :align: center

   An example of a .svg result produced by the Freestyle SVG Exporter.
   Model by `Blendergoodies <http://www.blendswap.com/blends/view/76715>`__

This addon can be enabled via *User Preferences* > *Addons* > *Render:Freestyle SVG Exporter*.
The GUI for the exporter should now be visible in the render tab of the properties window.
The exported .svg file is written to the default
output path (*Properties* > *Render* > *Output*).


Options
=======

.. figure:: /images/render-freestyle_ui_svg_exporter.png
   :width: 300px
   :align: right

Mode
   Option between Frame and Animation. Frame will render a single frame, Animation will bundle all rendered frames
   into a single .svg file.
Split at Invisible
   By default the exporter won't take invisible vertices into account and export them like they are visible.
   Some stroke modifiers, like Blueprint, mark vertices as invisible to achieve a certain effect. Enabling this
   option will make the paths split when encountering an invisible vertex, which leads to a better result.
Fill Contours
   The contour of objects is filled with their material color. Note that this features is somewhat unstable -
   especially with animations.
Stroke Cap Style
   Defines the style the stroke caps will have in the SVG output.


Exportable Properties
=====================

Because the representation of Freestyle strokes and SVG path objects is fundamentally different, a one on one
translation between Freestyle and SVG is not possible. The main shortcoming of SVG compared to Freestyle is that
Freestyle defines style per-point, where SVG defines it per-path. This means that Freestyle can produce much more
complex results that are impossible to achieve in SVG.

The properties that can be exported are:

- Base color
- Base alpha
- Base thickness
- Dashes


Animations
==========

The exporter supports the creation of SVG animations. When the Mode is set to Animation, all frames from a render -
one when rendering a frame (f12) or all when rendering an animation (shift f12) - into a single file.
Most modern browsers support the rendering of SVG animations.

.. figure:: /images/render-freestyle_svg_rotating_cube.svg
   :width: 600px
   :align: center

   An SVG animation rendered with the exporter.


Exporting Fills
---------------

Fills are colored areas extracted from a Freestyle render result. Specifically, they are defined by a combination of
the Contour and External Contour edge type, combined with some predicates. The fill result can be unexpected, when
the SVG renderer cannot correctly draw the path that the exporter has generated. This problem is extra apparent in
animations.

.. figure:: /images/render-freestyle_svg_pallet.svg
   :width: 600px
   :align: center

   An example of a .svg result produced by the Freestyle SVG Exporter.
   Model by `Julien Deswaef <https://github.com/xuv>`__

Fills support holes and layering. When using layers, the exporter tries to render objects with the same material as
the patch. The exporting of fills and especially the order in which they are layered is by no means perfect. In most
cases, these problems can be easily solved in Inkscape or a text editor.
