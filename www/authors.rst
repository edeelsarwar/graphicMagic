.. -*- mode: rst -*-
.. This text is in reStucturedText format, so it may look a bit odd.
.. See http://docutils.sourceforge.net/rst.html for details.

======================
GraphicsMagick Authors
======================

The following people have contributed substantially to the development
of GraphicsMagick.  Please let us know if an author is missing, or a
significant contribution was made and not recorded.

.. contents::
  :local:


Active GraphicsMagick Contributors
==================================

Bob Friesenhahn
                Principal maintainer of GraphicsMagick. Author of
                Magick++ (C++ API to ImageMagick and GraphicsMagick).
                Author of module loader facility, automatic file
                identification (magic) support, Unix/Cygwin/MinGW
                configure/make facility, Windows setup.exe style
                installer, WMF renderer, C API documentation formatter,
                and the C, C++, and Perl test suites used by ImageMagick
                and GraphicsMagick.

Jaroslav Fojtik
                Authored the ART, CUT, HRZ, JNX, MAC, MATLAB, TOPOL,
                and WPG coder modules. Improved the FITS and TXT coder
                modules.  VisualMagick 'configure' improvements and
                build testing/fixes for many versions of Microsoft
                Visual Studio.

Tobias Mark
                Authored the HEIF and JPEG XL coder modules.


Former GraphicsMagick Contributors
==================================

Glenn Randers-Pehrson
                Contributed significantly to the utilities, including
                writing the 'gm' utility wrapper. Authored support for
                JNG, MNG, and PNG formats. Provided significant
                support for the BMP format. Significant improvements
                to the documentation, including creating a
                documentation authoring environment based on the
                <imdoc> format.  Maintained the SourceForge mailing
                lists.  GraphicsMagick would not be what it is today
                without Glenn and he will always be remembered.

Gregory J Wolfe
                Contributed significant improvements to the SVG
                parsing and rendering code.

Troy Patteson
                Contributed a several significant patches to fix image
                rotation bugs and improve image rotation performance,
                as well as an improved bi-linear interpolation
                implementation.

Kenneth Xu
                Contributed the implementation of 'gm batch', a simple
                batch mode for GraphicsMagick.

Sara Shafaei
                Contributed a number of Wand API functions as well as
                fixes for several composition operators.

Brendan Lane
                Contributed a large number of new Photoshop
                composition operators and alpha-channel fixes for
                existing ones.

Dirk Lemstra
                Contributed improvements to the VisualMagick configure
                program to support configuring more build options via
                the GUI dialogs and to deal with similarly named
                files.

Roman Hiestand
                Contributed WebP coder improvements.

Mike Chiarappa
                Created and maintains the Borland C++ Builder 6.0 build
                environment for GraphicsMagick.

Daniel Kobras
                Provided many security patches and fixes from the Debian
                project.

William Radcliffe
                Author of the VisualMagick project configure facility for
                Visual C++. Author of FlashPix module. Author of the
                ImageMagickObject COM object for Windows. Author of the
                EMF, XTRN, and META coders. Significant contributions to
                the MSL, JPEG, TIFF, SVG, and URL coders. Authored
                "process" module support. Wrote the micro-timer facility
                used by 'identify'. Ported module loader support to
                Windows. Significantly improved polygon rendering
                performance.

Leonard Rosenthol
                Authored the 'conjure' utility and associated MSL
                execution environment. Provided MacOS support. Authored
                the CLIPBOARD, XCF, and PSD coders. Postscript and PDF
                expertise. Significant drawing enhancements including
                support for dash patterns, linecap stroking, clipping
                masks and a mask image.

Lars Ruben Skyum
                Contributed the -clippath functionality, added
                -define support, improved color profile support,
                and re-wrote the PS3 coder.

Rolf Schroedter
                Principal author of TclMagick.

David N. Welton
                Co-author of TclMagick, particularly in the Unix environment.

Mark Mitchell
                Contributed a new design for the web pages, including the
                formatting scripts, and converted many pages to the new
                format.

Richard Nolde
                Contributed code for converting between native floating
                point types, and short (16/24) bit float types.

Cl�ment Follet
                Contributed Hald CLUT and ASC-CDL implementations.

John Sergeant
                Re-wrote the HP PCL writer to work much better,
                including support for compression.  Implemented
                support for CALS type 1 format.  Re-wrote the DICOM
                reader.

Roberto de Deus Barbosa Murta
                Contributed the adaptive threshold implementation
                (-lat), which executes in linear rather than quadratic
                time.

Samuel Thibault
                Contributed support for the Braille image format.


Other Contributors (via ImageMagick)
====================================

John Cristy
                Creator, principal author, and principal maintainer of
                ImageMagick, from which GraphicsMagick is originally
                derived (from ImageMagick 5.5.2).  Also the author of
                the Wand API to ImageMagick which is incorporated as
                a stand-alone library by GraphicsMagick.

Kelly Bergougnoux
                Authored the initial Cineon coder (which has since been
                replaced).

Christopher R. Hawks
                Authored the PALM coder.

Francis J. Franklin
                Ported the WMF coder to the libwmf 0.2 API.

Rick Mabry
                Contributed code to support filling drawn objects using a
                pattern image.
Nathan Brown
                Original author of the JP2 coder.

Kyle Shorter
                Original author of PerlMagick. Original author of the
                LOCALE coder.

Markus Friedl
                Original author of Base64 encode/decode sources.

David Harr
                Contributed (with Leonard Rosenthol) dash pattern,
                linecap stroking algorithm, and minor rendering
                improvements.

Troy Edwards
                Authored the source RPM spec file for GraphicsMagick.

Milan Votava
                Contributed support for Wireless BitMap, used in WAP -
                Wireless Access Protocol.

Mike Edmonds
                Contributed the median filter algorithm.
