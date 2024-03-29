2017-12-25  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - tests/rwfile.tap: Add tests for MIFF compressed sub-formats.

2017-12-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/blob.c (OpenBlob): Zlib 1.2.8 does not accept an open
    mode of "w+b" or "wb+".  It seems to be allergic to '+'.  As a
    result, writing to ".gz" files was not working with Zlib 1.2.8.
    Note that "w+b" must be used in the normal case since the test
    suite fails otherwise!

2017-12-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadMNGImage): Fix SourceForge issue #535
    "heap-buffer-overflow in ReadMNGImage".  Problem was caused by
    accessing byte before testing that limit has been reached, rather
    than testing for limit before accessing the byte.  This means that
    it could only ever read one past the buffer allocation size.

  - coders/webp.c (WriteWEBPImage): Fix SourceForge issue #536
    "stack-buffer-overflow in WriteWEBPImage".  Due to a change to use
    WebPMemoryWriter as part of the EXIF and ICC profile support
    addition (enabled with libwebp 0.5.0), the progress indicator
    callback is now passed a pointer to a wrong structure.  This is
    quite unfortunate since the progress indication is useful.  The
    progress indication is temporarily disabled when the
    WebPMemoryWriter is in use until a solution is implemented.
    (ProgressCallback): Re-implement progress callback so that image
    pointer is stored/retrieved as thread-specific data.

  - coders/png.c (ReadMNGImage): Fix SourceForge issue #537 "null
    pointer dereference in ReadMNGImage".  DEFI chunk must be at least
    2 bytes long.

  - coders/tiff.c (ReadNewsProfile): Fix SourceForge issue #533
    "heap-buffer-overflow on LocaleNCompare".  LocaleNCompare() was
    being allowed to read heap data beyond the allocated region.

2017-12-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/shear.c (IntegralRotateImage): Assure that reported error
    in rotate by 270 case does immediately terminate processing.
    Return a NULL Image pointer if there is a problem rather than a
    corrupted image.  Fix is related to SourceForge issue #532
    "heap-buffer-overflow bug in ReadWPGImage".

  - magick/pixel\_cache.c (AcquireCacheNexus): Add a check that the
    pixel cache is compatible with the image dimensions.  Fix is
    related to SourceForge issue #532 "heap-buffer-overflow bug in
    ReadWPGImage".

2017-12-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Fix SourceForge issue #530
    "heap-buffer-overflow in ReadOneJNGImage".  In this case there is
    a read one byte beyond the oFFs chunk allocation size due to an
    error in specifying an offset into the chunk.

  - coders/palm.c (ReadPALMImage): Fix SourceForge issue #529
    "global-buffer-overflow in ReadPALMImage".  This issue only
    occured in builds with QuantumDepth=8 due to the small range of
    IndexPacket.

2017-12-13  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - PerlMagick/{Magick.pm, Magick.pm.in, Makefile.PL.in}: Only base
    PerlMagick version on numeric portion of PACKAGE\_VERSION.

2017-12-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - www/index.rst: Update to 1.3.27.

  - www/Changes.rst: Add 1.3.27

  - version.sh: Update library versioning.

  - NEWS.txt: Update NEWS in preparation for releasing 1.3.27.

2017-12-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dcm.c (DCM\_ReadElement): Change size checks addressing
    CVE-2017-12140 to be based on size\_t rather than magick\_off\_t due
    to apparent instability of the previous check across compilers.

2017-12-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (WriteOnePNGImage): Fix heap read access outside of
    allocated PixelPacket array while testing pixels for opacity.
    Resolves SourceForge issue #526 "heap-buffer-overflow in
    WriteOnePNGImage".

2017-12-06  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pnm.c (WritePNMImage): Fix SourceForge bug #525
    "heap-buffer-overflow in MagickBitStreamMSBWrite".

2017-12-05  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dcm.c (DCM\_ReadElement): Eliminate huge memory allocation
    based on bogus length value. Addresses CVE-2017-12140. Problem was
    reported via email from Petr Gajdos on Tue, 5 Dec 2017.

2017-12-03  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - Magick++/lib/Image.cpp (colorMap): Try to eliminate Coverity CID
    172796 "Dereference after null check" which seems to be bogus.

  - coders/png.c (WriteOnePNGImage): Fix Coverity CID 168053
    "Dereference after null check".  The check for null and the error
    report which attempted to use the null value was not needed at
    all.

  - coders/cut.c (GetCutColors): Fix Coverity CID 10181: "Null
    pointer dereferences". SetImagePixels() may return NULL.

  - coders/rgb.c (ReadRGBImage): Fix SourceForge issue #523
    "heap-buffer-overflow".  Similar issue to cmyk.c.

  - coders/gray.c (ReadGRAYImage): Fix SourceForge issue #522
    "heap-buffer-overflow".  Similar issue to cmyk.c.

  - coders/cmyk.c (ReadCMYKImage): Fix SourceForge issue #521
    "heap-buffer-overflow". The requested tile must be within the
    bounds of the image.  As it happens, 'montage' passes size and
    tile information which is useless for reading a raw image so it is
    not possible to read raw CMYK using 'montage'.

2017-12-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pwp.c (ReadPWPImage): Eliminate dereference of null image
    pointer.  Addresses CVE-2017-11640.  Also address access to
    uninitialized memory.  Problem was reported via email from Petr
    Gajdos on Wed, 29 Nov 2017.

2017-11-22  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - coders/wpg.c Additional check for wrong bpp CVE-2017-14342.


2017-11-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - Magick++/lib/Image.cpp (autoOrient): Add method to auto-orient
    an image so it looks right-side up by default.  Based on patch by
    Przemysław Sobala submitted as SourceForge patch #53 "Add
    Magick::Image::autoOrient() method to Magick++ library".

  - www/download.rst: Change "Czechoslovakian ftp mirror" to "Czech
    ftp mirror".  Resolves SourceForge bug #520 "[web] Download sites:
    non-existent country".

2017-11-21  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/wpg.c (ReadWPGImage): Fix excessive use of disk resources
    due to unreasonable record length.  Addresses CVE-2017-14341.
    Notified of this issue (with suggested patch) via email by Petr
    Gajdos on Tue, 21 Nov 2017.

2017-11-19  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - README.txt: Comprehensive white-space clean-up across
    GraphicsMagick core source files.  Hard TAB character is converted
    to spaces.  Trailing white-space garbage is stripped.

  - magick/colormap.c (MagickConstrainColormapIndex): Deprecate use
    of MagickConstrainColormapIndex() and prefer use of
    VerifyColormapIndex() and VerifyColormapIndexWithColors() due to
    avoiding dependence on index type, allowing provision of colors
    other than image->colors, and capturing more useful source file
    and line information.

  - coders/{rle.c, mat.c, xbm.c, sgi.c, png.c}: Eliminate size\_t vs
    unsigned 32 conversion warnings in WIN64 build.

2017-11-18  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - tiff: Import libtiff 4.0.9.

2017-11-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/bmp.c (DecodeImage): "Right-size" and "Right-type"
    DecodeImage() variables and check for EOF at every point of the
    way.  Pass buffer size as an argument.

  - coders/dib.c (DecodeImage): "Right-size" and "Right-type"
    DecodeImage() variables and check for EOF at every point of the
    way.  Pass buffer size as an argument.

  - coders/bmp.c (\_BMPInfo): "Right-size" BMPInfo members.  The
    'long' type is promoted to 64-bit on LP64 systems and the large
    size is not needed.

2017-11-11  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/webp.c: Incorporate patch by Jan Spitalnik to add EXIF
    and ICC metadata support to the WebP coder.  While WebP is still
    supported back to libwebp 0.1.99, the metadata support requires at
    least libwebp 0.5.0.  Resolves SourceForge patch #52 "Add EXIF/ICC
    metadata support to WebP coder".

  - coders/png.c (ReadOneJNGImage): Fix JNG memory leaks when JPEG
    image fails to be read.
    (WriteOnePNGImage): Promotion of indexed PNG to RGBA lacked
    setting of image matte, resulting in undersized buffer allocation
    and heap overflow.  Fixes SourceForge bug #453 "Heap overflow in
    source-gra/coders/png.c".

2017-11-06  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/sfw.c (SFWScan): Fix heap buffer overflow
    (CVE-2017-13134).  Notified of problem via email (including a
    patch) from Petr Gajdos on Mon, 6 Nov 2017.

2017-11-05  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - coders/wpg.c Wrong MaxMap check condition - fixed.

2017-11-04  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - coders/wpg.c Check for InsertRow() return value.

2017-11-04  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/export.c: Add not-null check for indexes pointer where
    needed.

  - magick/import.c: Add not-null check for indexes pointer with
    associated exception report where the indexes pointer is needed.
    (ImportCMYKQuantumType): Was wrongly importing an opacity channel
    in some cases. Would have crashed if these cases were ever used.

  - coders/wpg.c (ReadWPGImage): Assure that colormapped image is a
    PseudoClass type with valid colormapped indexes.  Fixes
    SourceForge bug 519 "Null Pointer Dereference (Write) with
    malformed WPG Image".

  - coders/sfw.c (ReadSFWImage): Avoid possible heap overflow while
    copying JFIF magic into buffer. Reject runt files.  Fixes
    CVE-2017-12983.  Notified of problem via email from Petr Gajdos on
    Thu, 2 Nov 2017.

2017-10-28  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Fix SourceForge bug #517 "Push
    operations in DrawImage can lead to negative strncpy when looking
    for pop".  Interestingly, valgrind and ASAN only detected a
    problem with one of the test cases since exercised code which
    updated an array using the index.  It appears that Linux strncpy()
    simply ignores the bad request.

2017-10-27  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Make sure that a reasonable
    exception is reported to the user when there is a read failure.

2017-10-26  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Reject JNG files with
    unreasonable dimensions given the file size.

2017-10-25  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Fix SourceForge bug #518 "Null
    pointer in".  Also make sure that errors are reported properly due
    to problems with transferring JPEG scanlines.
    (ReadOneJNGImage): Add more checks for null value returned from
    SetImagePixels().

2017-10-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/describe.c (DescribeImage): Fix possible heap read
    overflow while accessing heap data, and possible information
    disclosure while describing the IPTC profile.  Report was provided
    via email from Maor Shwartz to the graphicsmagick-security mail
    alias on Thu, 19 Oct 2017.  Independent security researchers,
    Jeremy Heng (@nn\_amon) and Terry Chia (Ayrx), reported this
    vulnerability to Beyond Security’s SecuriTeam Secure Disclosure
    program. Please note that this interface is usually (but not
    exclusively) used from within the command-line utility program, in
    which case there is not much useful information which might be
    disclosed.
    (DescribeImage): Fix possible heap write overflow when describing
    visual image directory.  Report was provided via email from Maor
    Shwartz to the graphicsmagick-security mail alias on Thu, 19 Oct
    2017.  Independent security researchers, Jeremy Heng (@nn\_amon)
    and Terry Chia (Ayrx), reported this vulnerability to Beyond
    Security’s SecuriTeam Secure Disclosure program. Please note that
    this interface is usually (but not exclusively) used from within
    the command-line utility program, in which case the only harm
    would be a program crash.

  - magick/constitute.c (WriteImage): Assure that the errno present
    when the blob error status first occured is reported to the user.

  - magick/blob.c (GetBlobStatus): Blob error status is now updated
    immediately upon the first error reported.
    (GetBlobFirstErrno): Returns errno value when the first blob error
    was reported.  This is useful for error reporting.

2017-10-21  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/constitute.c (WriteImage): Restore use of GetBlobStatus()
    to test if an I/O error was encountered while writing output file.
    This assures that I/O failure in writers which do not themselves
    verify writes is assured to be reported.

2017-10-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/webp.c (WriterCallback): WebP writer now detects partial
    write to output file.  Patch by Przemysław Sobala from a posting
    on Mon, 16 Oct 2017 via the graphicsmagick-help mailing list.

2017-10-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c (MontageImageCommand): Fix memory leaks in
    error return path.  Only people doing leak testing or the few who
    execute MontageImageCommand() as a function will care about this.

  - magick/studio.h (NumberOfObjectsInArray): The
    NumberOfObjectsInArray() macro is used to compute the number of
    whole objects in an array.  Instead it was rounding up, resulting
    in scrambling the heap beyond the allocation.  Fixes
    CVE-2017-13737 "There is an invalid free in the MagickFree
    function in magick/memory.c in GraphicsMagick 1.3.26 that will
    lead to a remote denial of service attack."

2017-10-09  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadOnePNGImage): Suppress "comparison between
    signed and unsigned integer expressions" warning.
  - coders/png.c (ReadJNGImage): Fix memory leak in SourceForge
    Issue #469 "use after free in ReadJNGImage".
  - coders/png.c (ReadJNGImage): Fix memory leak in SourceForge
    Issue #470 "Assert failure in writeblob".

2017-10-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - doc/options.imdoc: Fix SourceForge issue #444 "gm mogrify: Wrong
    documentation for option -output-directory".

2017-10-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/module.c (InitializeModuleSearchPath): Verify that any
    component paths specified in MAGICK\_CODER\_MODULE\_PATH and
    MAGICK\_FILTER\_MODULE\_PATH exist before adding them to search paths
    actually used, and convert to real paths if possible.  This avoids
    possible use of relative paths to load modules (a possible
    security issue) and may improve efficiency by removing
    non-existent paths.

  - coders/yuv.c (ReadYUVImage): Fix leak of scanline upon Image
    allocation failure.  Patch submitted by Petr Gajdos via email on
    Fri, 6 Oct 2017.

2017-09-13  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Attempt to fix SourceForge Issue #469 "use after
    free in ReadJNGImage".  Note that this change was found to replace
    a use after free with a memory leak so the problem is not solved
    yet.

2017-10-03  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dcm.c (DCM\_ReadNonNativeImages): Additional fix
    (improvement) for SourceForge issue #512 "NULL Pointer Dereference
    in DICOM Decoder".

2017-10-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dcm.c (ReadDCMImage): Fix SourceForge issue #512 "NULL
    Pointer Dereference in DICOM Decoder".

  - coders/pict.c (ReadPICTImage): Fix SourceForge issue #511
    "Memory Allocation error due to malformed image file".

  - coders/pnm.c (WritePNMImage): Fix SourceForge issue #503 "memory
    leak in WritePNMImage".

  - coders/png.c (ReadMNGImage): Fix SourceForge issue #501 "memory
    leak in ReadMNGImage".

  - magick/segment.c (InitializeIntervalTree): Fix SourceForge issue
    #507 "null pointer in segment.c" and issue #508 "null pointer in
    segment.c".

  - coders/topol.c (ReadTOPOLImage): Fix SourceForge issue #510
    "null pointer and meory leak in topol.c".

  - magick/widget.c (MagickXFileBrowserWidget): Fix SourceForge
    issue #506 "null pointer in widget.c".

  - coders/tiff.c (WriteTIFFImage): Fix SourceForge issue #509
    "Memory leak in tiff.c".

  - magick/module.c (FindMagickModule): Fix SourceForge issue #502
    "null pointer in module.c".

  - coders/avs.c (ReadAVSImage): Fix Coverity CID 184115 "Control
    flow issues (DEADCODE)".

2017-09-30  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/avs.c (ReadAVSImage): Fix SourceForge issue #499 "memory
    leak in avs.c".

  - coders/cmyk.c (ReadCMYKImage): Fix SourceForge issue #498
    "memory leak in cmyk.c".

  - coders/cut.c (ReadCUTImage): Fix SourceForge issue #497 "memory
    leak in cut.c".

  - coders/dpx.c (ReadDPXImage): Fix SourceForge issue #496 "memory
    leak in dpx.c".

  - coders/hdf.c (ReadHDFImage): Fix SourceForge issue #495 "memory
    leak in hdf.c".

  - coders/pcx.c (ReadPCXImage): Fix SourceForge issue #494 "memory
    leak in pcx.c".

  - coders/pcd.c (ReadPCDImage): Fix SourceForge issue #493 "memory
    leak in ReadPCDImage".

  - coders/histogram.c (WriteHISTOGRAMImage): Fix SourceForge issue
    #492 "memory leak in WriteHISTOGRAMImage".

  - coders/gif.c (WriteGIFImage): Fix SourceForge issue #491 "memory
    leak in WriteGIFImage".

  - coders/fits.c (WriteFITSImage): Fix SourceForge issue #490
    "memory leak in WriteFITSImage".

  - coders/palm.c (WritePALMImage): Fix SourceForge issue #489
    "memory leak in WritePALMImage".

  - coders/rgb.c (ReadRGBImage): Fix SourceForge issue #488 "Memory
    leak in rgb.c".

  - coders/palm.c (ReadPALMImage): Fix SourceForge issue #487 "NULL
    pointer dereference in ReadPALMImage".

  - Magick++/lib/Options.cpp (strokeDashArray): Fix SourceForge
    issue #486 "NULL pointer dereference in
    Magick::Options::strokeDashArray".

  - magick/nt\_feature.c (NTGetTypeList): Fix SourceForge issue #485
    "NULL pointer dereference in NTGetTypeList".

  - coders/sun.c (ReadSUNImage): Fix SourceForge issue #484 "Memory
    leak in sun.c".

  - coders/tim.c (ReadTIMImage): Fix SourceForge issue #483 "Memory
    leak in tim.c".

  - magick/nt\_base.c (NTRegistryKeyLookup): Fix SourceForge issue
    #482 "NULL pointer dereference in NTRegistryKeyLookup".

  - coders/viff.c (ReadVIFFImage): Fix SourceForge issue #481
    "Memory leak in viff.c".

  - magick/profile.c (SetImageProfile): Fix SourceForge issue #480
    "assertion failure in MagickMapAllocateMap".

  - coders/yuv.c (ReadYUVImage): Fix SourceForge issue #478 "Memory
    leak in yuv.c".

  - magick/map.c (MagickMapCloneMap): Fix SourceForge issue #477
    "assertion failure in MagickMapIterateNext".

  - coders/emf.c (ReadEnhMetaFile): Fix SourceForge issue #475 "NULL
    pointer dereference in ReadEnhMetaFile".

  - coders/cineon.c (ReadCINEONImage): Fix SourceForge issue #473
    "NULL pointer dereference in ReadCINEONImage"

  - coders/tiff.c (TIFFIgnoreTags): Fix SourceForge issue #476 "NULL
    Pointer in tiff.c".

2017-09-25  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/blob.c (GetConfigureBlob): Fix SourceForge issue #472
    "NULL Pointer in GetConfigureBlob".

2017-09-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/rle.c (ReadRLEImage): Fix SourceForge issue #458 "Heap
    out of bounds read in ReadRLEImage()".

2017-09-19  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/sgi.c (ReadSGIImage): Check for EOF while reading SGI
    file header.  Issue was brought to our attention by Petr Gajdos
    via email on Fri, 1 Sep 2017.

2017-09-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/tiff.c (ReadTIFFImage): Allow a single scanline, strip,
    tile, to be 1000X larger than the input file in order to not cause
    problems for extremely compressible images or tile sizes much
    larger than the pixel dimensions.

2017-09-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/symbols.h, wand/wand\_symbols.h: Update C library symbols
    which should be prefixed with 'Gm'. However, GM will not move
    Magick++ namespace because of the ImageMagick version.  Resolves
    SourceForge issue #468 "--enable-symbol-prefix does not prevent
    clashes with libMagick++ or libMagickWand?"

  - coders/png.c (DestroyJNG): DestroyJNG should be a static
    function.  Was wrongly exposed as DestroyJNGInfo in 1.3.26.  This
    is not a public function and was not intended to be part of the
    ABI.

  - coders/tiff.c (ReadTIFFImage): Limit scanline, strip, and tile
    memory allocations based on file size multiplied by a maximum
    compression ratio.  Fixes SourceForge issues #460, #461, #462,
    #463, #464 "allocation failure in ReadTIFFImage".

  - coders/pnm.c (ReadPNMImage): Require that XV 332 format have 256
    colors.  Fixes SourceForge issue #465 "NULL Pointer Dereference
    triggered by malformed file".  In our own testing the test case
    produced an assertion failure because assertions were enabled.

  - magick/colormap.c (AllocateImageColormap): Use unsigned array
    index.

2017-09-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/mat.c (ReadMATImage): Fix CVE-2016-10070, which is a heap
    overflow in the MAT reader due to an under-sized memory
    allocation.  Based on private email from Petr Gajdos on Mon, 11
    Sep 2017.

2017-09-13  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Check MemoryResource before allocating
    ping\_pixel array.

2017-09-11  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - magick/shear.c: Possible evil loop might waste CPU for long time
        without any reason.

2017-09-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Fix SourceForge issue #448 "Heap
    out of bounds read in DrawDashPolygon()".  Problem was reported by
    Kamil Frankowicz on August 28, 2017.

  - coders/uil.c (WriteUILImage): Fix crash in UIL writer when
    writing image containing transparency.  Issue was reported by
    LCatro via email on 18 Jul 2017.

  - coders/wpg.c (InsertRow): Fix crash which occurs if image is not
    PseudoClass but a PseudoColor scanline is needed.  Resolves
    SourceForge issue #449 "Null pointer dereference in InsertRow()".

  - coders/rle.c (ReadRLEImage): Impose image dimension limits
    according to Utah RLE specification. Cap number of planes handled
    internally at 4.  Remove non-standard multi-frame extension, which
    did not work anyway.

2017-09-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadJNGImage): Complete fixing CVE-2017-8350 crash
    while reading a malformed JNG file.

  - coders/{html.c, map.c, plasma.c, png.c, psd.c, rle.c, stegano.c,
    uil.c}: Downgrade claimed coder stability level for HTML, SHTML,
    MAP, FRACTAL, PLASMA, JNG, MNG, RLE, STEGANO, and UIL formats.

2017-09-08  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadJNGImage): More efforts toward fixing
    CVE-2017-8350 while reading a malformed JNG file.

2017-09-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/error.c (ThrowLoggedException): Capture the first
    exception at ErrorException level or greater, or only capture
    exception if it is more severe than an already reported exception.
    This should help lead to better error reports since the first
    error is usually the most significant.

  - coders/png.c (ReadJNGImage): Add "improper header" exception
    reporting.

2017-09-01  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadJNGImage): Efforts toward fixing CVE-2017-8350
    while reading a malformed JNG file.

2017-08-30  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/wpg.c (ReadWPGImage): Patch submitted by Petr Gajdos to
    check that .Width and .Height are greater than zero before they
    are assigned to image->columns and image->rows respectively
    (CVE-2014-9815).
    (ReadWPGImage): Do more validations on WPG\_Palette.StartIndex and
    WPG\_Palette.NumOfEntries.

2017-08-29  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Fix for SourceForge issue #440
    "use-after-free in CloseBlob (blob.c) (INCOMPLETE FIX FOR
    CVE-2017-11403)" and SourceForge issue #438 "heap use after free
    in CloseBlob".
  - coders/png.c (ReadOneJNGImage): Fix for SourceForge issue #439
    "assertion failure in magick/pixel\_cache.c"

2017-08-27  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/mpeg.c (WriteMPEGImage): Fix MPEG writer memory leak.
    Only the first image in the coalesce image list was being freed.
    Problem was reported by LCatro via email on July 15, 2017.

  - magick/attribute.c (TracePSClippingPath, TraceSVGClippingPath):
    Fix SourceForge bug #447 "Heap out of bounds read in
    ReadMSBShort()".

2017-08-26  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/xbm.c (ReadXBMImage): Fix two denial of service (DOS)
    issues in ReadXBMImage() which result in the reader not
    returning. Problem was reported via email on Wed Aug 23 2017 by
    Xiaohei and Wangchu from Alibaba Security Team.

  - coders/jnx.c (ReadJNXImage): Fix denial of service (DOS) issue
    in ReadJNXImage() whereby large amounts of CPU and memory
    resources may be consumed although the file itself does not
    support the requests.  Problem was reported via email on Wed Aug
    23 2017 by Xiaohei and Wangchu from Alibaba Security Team.

2017-08-14  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadOneMNGImage): Deal with invalid (too large)
    length of MNG chunks (bug #446).

2017-08-20  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pnm.c (ReadPNMImage): Verify that sufficient file data
    exists to support what the file header requires before allocating
    memory for it.  Fixes problem reported by Agostino Sarubbo via
    email on Wed, 12 Jul 2017 and reported yet again via SourceForge
    bug #441 "memory allocation failure in MagickRealloc".

2017-08-20  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - coders/mat.c: Fix SourceForge bug #433 "memory leak in
    ReadMATImage".  Credit for discovering and reporting the problem
    is "ADLab of Venustech".

  - coders/sun.c (ReadSUNImage): Fix failure to allocate memory due
    to inadequate file data to support claimed image width and height.
    First notified by email from Agostino Sarubbo on 14 Jul 2017 and
    then again as SourceForge bug #442 "memory allocation failure in
    magickmalloc".

2017-08-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/svg.c (GetStyleTokens): Fix SourceForge bugs 434 "heap
    buffer overflow in GetStyleTokens", 435 "null pointer
    dereference\_in\_SVGStartElement", and 436 "heap buffer overflow in
    GetStyleTokens" which all originated from a heap buffer overflow
    in GetStyleStokens(), or inconsistent initialization.  Now the
    implementation truncates parsing for poorly-formed input (to avoid
    buffer overflow) while still correctly parsing well-formed input.
    The reproducers and problem reports are attributed to "ADLab of
    Venustech".

2017-08-14  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Fixed double-free after
    reading a malformed JNG (Issue #438).

2017-08-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pcd.c (ReadPCDImage): Fix memory leak on return path due
    to corrupted header.  Patch included in email on 14 Aug 2017 by
    Petr Gajdos (ImageMagick CVE CVE-2017-8351).

2017-08-11  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/gif.c (ReadGIFImage): Assure that global colormap is
    initialized.

  - coders/pict.c (ReadPICTImage): Fix memory leaks in error return
    path.  ImageMagick CVE CVE-2017-8353.  Patch by Petr Gajdos.

2017-08-11  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - tests/rwblob.c and rwfile.c: Write the reason for FAIL in
    test-suite.log.
  - magick/image.h: Revised table of image orientations to show
    Exif ImageOrientation values (which happen to be the same as
    the enum values 1 to 8).
  - coders/png.c: ReadJNGIMage(): fix memory leak (Issue 431).

2017-08-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/mtv.c (ReadMTVImage): Fix memory leak in error return
    path upon unexpected EOF (ImageMagick CVE-2017-9142).  Problem was
    brought to our attention via email from Petr Gajdos on Wed, 9 Aug
    2017.  Also changed pixel cache access functions used to assure
    delivery of exception to the user.

2017-08-05  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - configure.ac (SETJMP\_IS\_THREAD\_SAFE): Decide if setjmp/longjmp
    are thread safe based on host OS.  Assume that these interfaces
    are thread safe by default.  Declared not to be thread safe under
    Solaris.  Declaring these interfaces to be thread safe increases
    available concurrency for coders which use setjmp/longjmp for
    error recovery (e.g. PNG and JPEG).

2017-08-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/jpeg.c (RegisterJPEGImage): Add support for the
    SETJMP\_IS\_THREAD\_SAFE preprocessor definition (already used by
    coders/png.c) to indicate if setjmp/longjmp are thread safe on
    this platform and that it is safe for multiple encoders/decoders
    to be active at one time.

2017-07-31  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/sun.c: Fix heap read overflow while indexing into
    colormap. Problem was reported via email on 17 Jul 2017 by
    Agostino Sarubbo.

2017-07-31  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadMNGImage): Stop a leak when rejecting a
    MNG image with dimensions that are too large.

2017-07-26  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/wmf.c (ReadWMFImage): Eliminate use of already freed heap
    data in error reporting path.  Problem was reported via email by
    Agostino Sarubbo on Fri, 14 Jul 2017

2017-07-25  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadMNGImage) Free chunk allocation that remains
    after attempting to read a truncated file.
  - coders/png.c: Removed some redundant checks for chunk length
    before MagickFreeMemory(chunk), which is safe to call with a
    NULL argument.
  - coders/png.c: Fixed writer bug due to missing brackets; a Log
    statement should have been inside the "i" loop but instead was
    using i++ left over from the loop.  Bug report by L. Catro.
  - coders/png.c: Reject a MNG with dimensions greater than 65k
    by 65k.
  - coders/png.c (WriteOnePNGImage): Return without crashing if
    WriteOnePNGImage is passed a NULL image. Fixes CVE-2017-11522.

2017-07-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pcl.c (WritePCLImage): Fix null pointer dereference in
    PCL writer when writing monochrome images.  Problem was reported
    by LCatro via email on July 18.

  - magick/pixel\_cache.c (PersistCache): Fix memory leak while
    writing a MPC file.  Problem was reported by LCatro via email on
    July 18.

  - coders/map.c (WriteMAPImage): Fix null pointer dereference or
    segmentation violation in the MAP writer if the input image is not
    already colormapped.  Problem was reported by LCatro via email on
    July 18.

  - coders/gray.c (WriteGRAYImage): Improve tracing and tidy up.

  - coders/rgb.c (WriteRGBImage): Fix heap overwrite in raw RGB
    writer (all output subformats) given a multiframe sequence using
    different widths.  Problem was reported by LCatro via email on
    July 18.

  - coders/cmyk.c (WriteCMYKImage): Fix heap overwrite in raw CMYK
    writer (all output subformats) given a multiframe sequence using
    different widths.  Also fix wrong output of CMYKA (and vice-versa)
    when CMYK was intended.  Problem was reported by LCatro via email
    on July 18.

  - coders/palm.c: Disable the PALM writer since the writer is a
    work in progress and still has implementation problems.  Perhaps
    no one in the world remains who cares about the undocumented PALM
    format.  Resolves heap overflow and assertion issues reported by
    LCatro via emails on July 11th, and 12th, 2017.

  - magick/colormap.c (ReplaceImageColormap): Throw an exception
    rather than assertion if the input image is not colormapped.

2017-07-13  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Implemented eXIf chunk support.

2017-07-12  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Fix typecast of left shifts (patch by Bob F)

2017-07-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/ps.c (ReadPSImage): Fix reference to constant NULL image
    argument which is dereferenced to pass an exception to
    MagickMonitorFormatted().  Problem was reported by Agostino
    Sarubbo via email on Wed, 12 Jul 2017.

2017-07-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/blob.c: Add casts to fix undefined behavior in left
    shifts.  Issue was reported by Agostino Sarubbo via email on Mon,
    10 Jul 2017.

2017-07-10  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Ignore out-of-bounds MOVE
    and CLIP object\_id's.
  - coders/png.c (ReadMNGImage): Fix apparent off-by-one error
    in MNG FRAM change\_clipping processing.
  - coders/png.c (ReadMNGImage): Fix out-of-order CloseBlob()
    and DestroyImageList() that caused a use-after-free crash.
    Fixes CVE-2017-11403.  This bug was discovered by Agostino Sarubbo.

2017-07-08  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadOneJngImage): Revised double-free fix.

2017-07-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Fix double-frees caused by
    commit on 2017-07-06.

  - coders/jpeg.c (ReadJPEGImage): Defer creating pixel cache until
    after successfully reading first scanline.  Classify some serious
    libjpeg reported "warnings" as errors and quit processing
    scanlines immediately upon first error so that corrupt JPEG does
    not consume excessive resources.  Resolves excessive resource
    consumption issue reported for two JPEG files provided via email
    by LCatro on Tue, 4 Jul 2017.

2017-07-06  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadOneJNGImage): Remove spurious '\n' from log
    statement.

2017-07-06  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Consolidate JNG cleanup into a new DestroyJNG()
    function.

2017-07-05  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: prevent a crash due to zero-length color\_image
    while reading a JNG image. (CVE-2017-11102)

2017-07-04  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Make sure is up to date.

  - www/index.rst: Update for 1.3.26 release.

  - version.sh: Update library versioning for 1.3.26 release.

  - magick/command.c (BatchCommand): Add ferror() checks around
    batch input loop.

2017-07-03  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Reject a PNG file if the file size is too small
    (less than 61 bytes).  Reject a JNG file if it is too small (less
    than 147 bytes).
  - coders/jpeg.c: Reject a JPEG file if the file size is too small
    (less than 107 bytes).

2017-07-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dpx.c (ReadDPXImage): Compute required file size and
    verify that sufficient data exists in file before allocating
    memory to decode the image data.  Resolves problem with DPX file
    with valid header (but a huge claimed image width) provided
    provided via email on Thu, 29 Jun 2017 by LCatro.  This issue has
    been assigned CVE-2017-10799.

2016-07-02  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - coders/mat.c Check whether reported object size overflows file size.

2016-07-01  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - coders/mat.c Safety check for forged and or corrupted data.
    This issue has been assigned CVE-2017-10800.

2017-07-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/tiff.c ("QuantumTransferMode"): Use a generalized method
    to enforce that buffer overflow can not happen while importing
    pixels.  Resolves problem with RGB TIFF claiming only one sample
    per pixel provided via email on Thu, 29 Jun 2017 by LCatro.  This
    issue has been assigned CVE-2017-10794.

2017-06-29  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c: Convert bare 'unsigned int' to MagickPassFail
    where suitable to make intentions clear.  Convert True/False to
    MagickTrue/MagickFalse or MagickPass/MagickFail according to
    purpose.  This is a continuation of a gradual migration and does
    not represent an API change.

2017-06-25  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Avoid NULL dereference when MAGN chunk processing
    fails (https://sourceforge.net/p/graphicsmagick/bugs/426/). Expand
    TABs.

2017-06-25  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Update NEWS with changes since the previous release.

  - www/programming.rst: Switch the Lua link to
    https://github.com/arcapos/luagraphicsmagick, which is a more
    complete and direct interface from Lua to GraphicsMagick's Wand
    API.

2017-06-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - VisualMagick/installer/gm-foo-dll.iss: Remove PerlMagick from
    the slim Inno Setup installer builder and remove mention of
    PerlMagick from the installer documentation.

  - TclMagick/generic/TclMagick.c (magickCmd): Resolve SourceForge
    patch #51 "TclMagick: memory access error; possible segfault".
    (newMagickObj): Fix formatting of pointer value so it is 64-bit
    safe.  Resolves SourceForge patch #50 "TclMagick: 64-bit
    portability issue".

  - coders/pict.c (ReadPICTImage): Avoid possible use of negative
    value when indexing array, which would cause buffer overflow.
    Resolves SourceForge issue #427 "One possible buffer overflow
    vulnerability in
    GraphicsMagick-1.3.25/coders/pict.c:ReadPICTImage()".

2017-06-22  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Stop memory leak when reading invalid JNG image.
    Fixes CVE-2017-8350.

2017-06-18  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c: Fix lcms2.h inclusion logic.

  - wand/magick\_wand.c (MagickSetImageOrientation): Eliminate use of
    snprintf, which is not supported by older Visual Studio.

2017-06-09  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Accept exIf chunks whose data segment
    erroneously begins with "Exif\0\0".

2017-06-01  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Removed experimental zxIF chunk support.  That
    proposal is dead.

2017-05-27  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - config/log.mgk: Added documentation suggested by SourceForge
    issue #419 "Consider a small patch to log.mgk".

  - www/Changes.rst: Add missing link to most recent changes.

2017-05-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - www/Magick++/Image.rst: Improve documentation for Magick++
    Image::iccColorProfile() and Image::renderingIntent().

2017-05-21  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - tiff: Update to libtiff 4.0.8.

2017-03-19  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Quieted a new Coverity complaint about a potential
    text buffer overrun.

2017-03-19  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/image.c (SetImageInfo): Ignore empty magic prefix
    specification and do not remove colon character from start of
    filename.  Resolves SourceForge bug #415 "Inconsistent Behavior w/
    input\_file Parameter".

2017-03-18  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Added new private orNT PNG chunk, to
    preserve image->orientation when it is defined and not
    the default TopLeft.
  - coders/jpeg.c: Mention image->orientation in the log when
    writing a JPEG.

2017-03-15  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (WriteOnePNGImage): Add version info about
    gm, libpng, zlib, and lcms to the PNG debug log.

2017-03-04  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c (ImportImageCommand): Fix handling of -frame
    options. Option handling was incorrect due to option checking the
    frame option after it had been freed.  Checking the frame dash
    option before freeing the argument solves the problem.  From patch
    provided by Victor Ananjevsky as SourceForge patch #49 "-frame
    doesn't work in gm import".

  - Magick++/lib/Image.cpp (attribute): Added Image attribute method
    which accepts a 'char \*' argument, and will remove the attribute
    if the value argument is NULL.  From patch provided by "Gints" as
    SourceForge patch #46 "C++ api - method to clear/remove
    attribute".

  - VisualMagick/configure/configure.cpp (InitInstance): Applied
    patch by Paul McConkey to allow the quantum command line argument
    to set the default value in the wizard drop list.  This allows
    setting the quantum depth when the /nowizard argument was
    supplied.  Resolves SourceForge patch #48 "When running from the
    command line configure.exe does not use the quantum argument".
    The provided configure.exe still needs to be rebuilt to
    incorporate this change.

  - magick/command.c (MogrifyImage): The -orient command now also
    updates the orientation in the EXIF profile, if it exists.

  - Magick++/lib/Image.cpp (orientation): Update orientation in EXIF
    profile, if it exists.

2017-03-03  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/jp2.c: Support PGX JPEG 2000 format for reading and
    writing (within the bounds of what JasPer supports).

2017-02-23  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/tiff.c (QuantumTransferMode): Fix out of bounds read when
    reading CMYKA TIFF which claims to have only 2 samples per pixel.
    Problem was reported via email on February 15, 2017 by Valon
    Chu. This issue was assigned CVE-2017-6335.

2017-01-29  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - doc/options.imdoc (-geometry): Geometry documentation changes
    suggested by Jon Wong.

2017-01-26  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Added support for a proposed new PNG chunk
    (zxIf, read-only) that is currently being discussed on the
    png-mng-misc at lists.sourceforge.net mailing list.  Enable
    exIf and zxIf with CPPFLAGS="-DexIf\_SUPPORTED -DxzIf\_SUPPORTED".
    If exIf is enabled, only the uncompressed exIF chunk will be
    written and the hex-encoded zTXt chunk containing the raw Exif
    profile won't be written.

2017-01-25  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/msl.c (MSLStartElement): Change test for NULL image
    pointer to before it is used rather than after it is used.
    Problem reported by Petr Gajdos on 2017-01-25.

2017-01-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - TclMagick/unix/m4/tcl.m4: Update tcl.m4 to TEA 3.10.  File
    supplied by Massimo Manghi.

2017-01-21  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Added support for a proposed new PNG
    chunk (exIf read-write, eXIf read-only) that is currently
    being discussed on the png-mng-misc at lists.sourceforge.net
    mailing list.

2017-01-21  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c: Added read\_user\_chunk\_callback() function
    and used it to implement a private PNG caNv (canvas) chunk
    for remembering the original dimensions and offsets when an
    image is cropped.  Previously we used the oFFs chunk for this
    purpose, but this had potential conflicts with other applications
    that also use the oFFs chunk.

2017-01-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - TclMagick/Makefile.am (AM\_DISTCHECK\_CONFIGURE\_FLAGS): Applied
    patch by Massimo Manghi to set AM\_DISTCHECK\_CONFIGURE\_FLAGS so
    that 'make distcheck' remembers configuration options, and also to
    uninstall pkgIndex.tcl.

  - magick/image.c (SetImageEx): Use PixelIterateMonoSet() for
    possibly improved efficiency.

  - magick/pixel\_iterator.c (PixelIterateMonoSet): New pixel
    iterator intended for use when initializing image pixels, without
    regard to existing values.

2017-01-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - Copyright.txt: Bump copyright years and rotate ChangeLog.


