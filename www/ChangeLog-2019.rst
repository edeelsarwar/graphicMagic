2019-12-31  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/gradient.c (ReadGRADIENTImage): QueryColorDatabase() only
    throws a warning so allow the warning to propagate to the user
    rather than failing to report a useful message at all.

2019-12-30  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/gradient.c (GradientImage): OpenMP portability requires
    that loop variable be signed.

2019-12-30  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - magick/gradient.c: Visual studio does not compile file without
    this fix.

2019-12-30  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - VisualMagick\configure\configure.cpp Add option for speed optimisation
    to achieve better performance.

2019-12-29  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/version.h.in: Bump copyright years.

  - magick/image.c (DisplayImages): Fix return status.  Was
    returning inverted return status.

  - coders/gradient.c (ReadGRADIENTImage): Support the
    "gradient:direction" definition to produce produce additional
    gradient vector directions corresponding to South, North, West,
    East, NorthWest, NorthEast, SouthWest, and SouthEast.  This
    support is similar to a useful feature added in ImageMagick
    6.9.2.5 although there is no claim that the results are identical,
    even if the resulting images appear to be visually
    indistinguishable.

  - magick/gradient.c (GradientImage): Add support for using the
    image 'gravity' attribute to produce additional gradient vector
    directions corresponding to SouthGravity (the previously-existing
    default), NorthGravity, WestGravity, EastGravity,
    NorthWestGravity, NorthEastGravity, SouthWestGravity, and
    SouthEastGravity.  Gradient images are updated to be PseudoClass
    (color-mapped), if possible.

2019-12-28  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/gradient.c (GradientImage): Output PseudoClass images if
    we can.

  - coders/pcx.c (WritePCXImage): Fix heap overflow in PCX writer
    when bytes per line value overflows its 16-bit storage unit.
    Fixes SourceForge bug #619 "heap-buffer-overflow in WritePCXImage"
    reported by Suhwan Song.

  - magick/gradient.c (GradientImage): Gradient levels were still
    not spot-on.  Now they are.  Unfortunately, this necessitated
    re-generating reference test images based on gradient since the
    gradient output has changed a little bit more than the test error
    margins allow.

2019-12-25  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Test gradient image resource limits
    using the proper API.

  - magick/resource.c (ResourceInfinity): Fix definition of
    ResourceInfinity.  Due to parenthesis in the wrong place, the
    defined value was -1 rather than the maximum range value.  The
    effect of this is that GetMagickResource() would return -1 rather
    than the maximum range value for the return type as documented.
    Regression was added on Saturday, March 09, 2019 in the 1.3.32
    release via changeset 15927:a5318823758c.

  - tests/rwfile.c (main): Allow Ghostscript supported formats to be
    a bit lossy.

  - tests/rwblob.c (main): Allow Ghostscript supported formats to be
    a bit lossy.

  - magick/gradient.c (GradientImage): Compute blending alpha with
    double precision for more precision.

2019-12-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Updates in preparation for 1.3.34 release.

2019-12-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Update with changes since the last GM release.

  - coders/png.c (png\_read\_raw\_profile): Use size\_t type to store
    profile length and 'nibbles'.  Use safer way to test for profile
    buffer overflow.
    (ReadOnePNGImage): Use size\_t type to store 'ping\_rowbytes',
    'length', and 'row\_offset'.  Check png\_pixels allocation for
    arithemetic overflow when computing the required allocation size.

  - coders/tiff.c (WriteNewsProfile): Use size\_t type to store
    profile length.

  - coders/pict.c (WritePICTImage): Avoid 'alloc-size-larger-than'
    warning from GCC when allocating row\_bytes.

2019-12-21  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - tiff/libtiff/tiffconf.h: Add standard/common libtiff 'SUPPORT'
    options which are used in full-fledged Autoconf/Cmake libtiff
    builds but were missing from the Visual C template file.  In
    particular, WebP is now supported and JBIG is somewhat supported.

  - VisualMagick/jbig/libjbig/LIBRARY.txt (EXCLUDE): Remove
    tstcodec85.c from JBIG library build.

  - VisualMagick/configure/configure.cpp: Add JBIG library to
    include path when building libraries.  Add WebP as a dependency
    when building libtiff.

2019-12-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/nt\_base.h ("C"): Assume that float versions of functions
    became available in Visual Studio 2008.

2019-12-15  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/log.c (InitializeLogInfo): Using the compiled-in
    defaults, always log to stderr by default, even under Microsoft
    Windows.  The logging output may then be diverted to
    'win32eventlog' as soon as a log.mgk file is loaded if that is
    desired.  This should not be much of a problem because loading a
    log.mgk file is the first thing that the library attempts to do.
    This change is made due to users and developers being baffled at
    not seeing any log output due to the log output going to the (very
    unfriendly) Windows application log.

  - webp: libwebp is updated to the 1.0.3 release.

2019-12-15  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - magick/nt\_base.c Fix user only installation of Ghostscript.

2019-12-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - rungm.sh.in (DIRSEP): DIRSEP should always use Unix conventions for
    Autotools-based builds.

  - magick/module.h ("C"): Eliminiate redundant and conflicting
    ListModuleInfo() prototype.

  - coders/miff.c (ReadMIFFImage): Eliminate warnings in trace
    statements.

  - coders/dib.c (DecodeImage): Eliminate warnings in trace
    statements.

  - coders/bmp.c (DecodeImage): Eliminate warnings in trace
    statements.

  - magick/studio.h (SupportMagickModules): Fix the preprocessor
    logic controlling SupportMagickModules, which became broken for
    GCC MinGW-based builds starting in the 1.3.29 release when a
    "static" module loader was implemented.  Due to an error in the
    preprocessor logic, only the "modules" based build was working for
    MinGW.  Much thanks to Giovanni Remigi for making us aware of this
    issue.

2019-12-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pict.c (WritePICTImage): Throw a writer exception if the
    PICT width limit is exceeded. Fixes SourceForge issue 617
    "heap-buffer-overflow in function EncodeImage of coders/pict.c".

2019-12-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - jbig: jbigkit is updated to 2.1 release.

  - libxml: libxml2 is updated to 2.9.10 release.

  - bzlib: bzip is updated to 1.0.8 release.

  - zlib: zlib is updated to 1.2.11 release.

  - png: libpng is updated to 1.6.37 release.

2019-12-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - lcms: lcms2 is updated to 2.9 release.

  - tiff: libtiff is updated to 4.1.0 release.

2019-11-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawPatternPath): Don't leak memory if
    fill\_pattern or stroke\_pattern of cloned draw\_info are not null.
    Fixes oss-fuzz issue 18948 "graphicsmagick:coder\_MVG\_fuzzer:
    Indirect-leak in CloneImage".
    (PrimitiveInfoRealloc): Clear freshly-allocated PrimitiveInfo
    memory.

2019-11-23  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/attribute.c (GenerateEXIFAttribute): Fix oss-fuzz issue
    17986 "graphicsmagick:coder\_JPG\_fuzzer: Heap-buffer-overflow in
    GenerateEXIFAttribute".  This problem likely only happens in
    32-bit builds.

2019-11-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadMNGImage): Only magnify the image if the
    requested magnification methods are supported.

2019-11-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/compress.c (HuffmanDecodeImage): Fix signed overflow on
    range check which leads to heap overflow in 32-bit
    applications. Requires a relatively large file input compared with
    typical fuzzer files (greater than a megabyte) to trigger.
    Problem reported to the graphicsmagick-security mail address by
    Justin Tripp on 2019-11-13.
    (Ascii85Tuple): Fix thread safety issue by requiring caller to
    pass in tuple buffer as an argument and having callers allocate
    tuple buffer on the stack.

2019-11-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/bit\_stream.c: Add restrict declarations to slightly
    improve performance and decrease code size.

  - TclMagick/pkgIndex.tcl: Incorporate recommendations from third
    problem noted in SourceForge issue #420 "TclMagick issues and
    patch".  This is supposed to help support using an uninstalled
    GraphicsMagick and allow the installation path to contain a space.

  - wand/magick\_wand.c (MagickClearException): Destroy any existing
    exception info before re-initializing the exception info or else
    there will be a memory leak.

  - TclMagick/generic/libttkcommon.c (myMagickError): Clear
    exception from the Wand after it has been reported.  Addresses the
    fourth problem noted by SourceForge issue #420 "TclMagick issues
    and patch".  However, MagickClearException() already clears an
    exception in the Wand, so a new function is not needed.

  - TclMagick/unix/m4/tcl.m4: Change hard-coded INSTALL path to
    point to config/install-sh.  Re-generated/updated Autotools stuff
    by executing the genconf.sh script.  Addresses the first problem
    noted by SourceForge issue #420 "TclMagick issues and patch".

2019-11-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (SetNexus): Eliminate warning about
    possibly uninitialized variable from primordial GCC 3.4.3.

  - magick/render.c (ConvertPrimitiveToPath): Eliminate warning that
    IsClosedSubPath might be used uninitialized.

  - magick/common.h ("MAGICK\_FALLTHROUGH"): Added a
    MAGICK\_FALLTHROUGH macro to support the GCC/Clang fallthrough
    attribute when the time comes again that it would be useful.

2019-10-19  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pcx.c (ReadPCXImage): Verify that pixel region is not
    negative. Assure that opacity channel is initialized to
    opaqueOpacity.  Update DirectClass representation while
    PseudoClass representation is updated.  Improve read performance
    with uncompressed PCX.

2019-10-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/xpm.c (ReadXPMImage): Image properties are expected to
    appear within the first 512 bytes of the XPM file header.  fixes
    oss-fuzz 18267 "graphicsmagick:coder\_PICON\_fuzzer: Timeout in
    coder\_PICON\_fuzzer".

2019-10-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - configure.ac: Fix tcmalloc configuration report.

2019-10-13  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/wpg.c (ReadWPGImage): Implement subimage/subrange
    support.

  - coders/mat.c (ReadMATImage, ReadMATImageV4): Implement
    subimage/subrange support.  Should resolve oss-fuzz 14999
    "graphicsmagick/coder\_MAT\_fuzzer: Out-of-memory in
    graphicsmagick\_coder\_MAT\_fuzzer".

  - coders/tiff.c (TIFFMapBlob): Fix compile problem if
    LOG\_TIFF\_BLOB\_IO is defined.

  - coders/wpg.c (ExtractPostscript): Improve performance.  Avoid
    temporary files if possible.  Avoid additional memory allocations
    if possible.  Should address oss-fuzz issue 18173
    "graphicsmagick:enhance\_fuzzer: Timeout in enhance\_fuzzer" and
    oss-fuzz issue 17714 "graphicsmagick:coder\_WPG\_fuzzer: Timeout in
    coder\_WPG\_fuzzer".

2019-10-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pnm.c (PNMInteger): Place a generous arbitrary limit on
    the amount of PNM comment text to avoid denial of service
    opportunity.  Fixes oss-fuzz 18162 "Timeout · coder\_PNM\_fuzzer".

2019-10-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dps.c (ReadDPSImage): Fix memory leak when OpenBlob()
    reports failure.  Same as ImageMagick CVE CVE-2019-16709.

2019-09-27  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/attribute.c (GenerateEXIFAttribute): Skip
    unsupported/invalid format 0.  Fixes oss-fuzz issue 17597
    "graphicsmagick:coder\_SFW\_fuzzer: Heap-buffer-overflow in
    GenerateEXIFAttribute".

2019-09-19  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - fuzzing/oss-fuzz-build.sh: Change by Alex Gaynor so that the
    correct oss-fuzz fuzzing engine should be used.

2019-09-18  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/static.c (OpenModule): Static module loader should use
    upper-cased magick string when searching for a module alias.
    Fixes SourceForge issue #613 "static module loader is still
    case-sensitive".

2019-09-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - configure.ac: Report status of zstd (FaceBook Zstandard)
    compression in configuration summary.

2019-09-15  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (TraceArcPath): Substitute a lineto command when
    tracing arc is impossible.  Fixes oss-fuzz 10765
    "graphicsmagick/coder\_MVG\_fuzzer: Divide-by-zero in TraceArcPath".

2019-09-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (png\_read\_raw\_profile): Fix validation of raw
    profile length.  Fixes oss-fuzz 16906
    "graphicsmagick:coder\_ICO\_fuzzer: Out-of-memory in
    graphicsmagick\_coder\_ICO\_fuzzer".

  - coders/wpg.c (ReallocColormap): Avoid dereferencing a null
    pointer if image->colormap is null.  Fixes oss-fuzz 17004
    "graphicsmagick:coder\_WPG\_fuzzer: Null-dereference READ in
    ReallocColormap".

2019-09-13  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/memory.c (MagickRealloc): Add a note that the behavior of
    this function is as described for BSD reallocf(3), which is now
    appearing in Linux's GNU libc and elsewhere.

2019-09-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - www/OpenMP.rst: Document the significant OpenMP speed-up which
    may be obtained by using an alternate memory allocation library.
    Currently 'tcmalloc', 'mtmalloc', and 'umem' are supported as
    options.

  - www/INSTALL-unix.rst: Document new --with-tcmalloc option to
    enable using Google gperftools tcmalloc library.

  - configure.ac: Add support for using Google gperftools tcmalloc
    library via the --with-tcmalloc option.

  - scripts/rst2htmldeco.py: Port to Python 3 syntax and require at
    least Python 2.6.

  - scripts/relpath.py: Port to Python 3 syntax and require
    at least Python 2.6.

  - scripts/html\_fragments.py: Port to Python 3 syntax and require
    at least Python 2.6.

  - scripts/format\_c\_api\_doc.py: Port to Python 3 syntax and require
    at least Python 2.6.

2019-08-27  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - doc/GraphicsMagick.imdoc: Document gm utility exit status codes.

2019-08-25  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (PRIMITIVE\_INFO\_POINTS\_MAX): SIZE\_MAX apparently
    rounds up by one when cast to a double on 64-bit systems.  Due to
    this, and in order to set more rational implementation limits, add
    a PRIMITIVE\_INFO\_POINTS\_MAX definition which computes and
    constrains the maximum number of PrimitiveInfo entries allowed.

2019-08-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/attribute.c (GenerateEXIFAttribute): Check that we are
    not being directed to read an IFD that we are already parsing and
    quit in order to avoid a loop.  Addresses oss-fuzz 15753
    "graphicsmagick/coder\_JPEG\_fuzzer: Timeout in
    graphicsmagick\_coder\_JPEG\_fuzzer" and 16068
    "graphicsmagick/coder\_SFW\_fuzzer: Timeout in
    graphicsmagick\_coder\_SFW\_fuzzer".

  - tests/{constitute.c, drawtest.c, rwblob.c, rwfile.c}: Eliminate
    irritating GCC 9 "\_\_builtin\_strncpy' output may be truncated"
    warnings due to copying MaxTextExtent-1 characters.  Instead
    request copying all of the characters and also assure that string
    is still null terminated.

  - doc/environment.imdoc: Update documentation pertaining to HOME
    and MAGICK\_DEBUG environment variables.

2019-08-23  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/log.c (DestroyLogInfo): Only output text to terminate an
    XML format log file if XML format is active.

2019-08-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (ExtractTokensBetweenPushPop): Previous fix for
    non-terminal loop was broken by a last-minute untested edit.
    Finally addresses oss-fuzz 15318 "graphicsmagick/coder\_MVG\_fuzzer:
    Timeout in graphicsmagick\_coder\_MVG\_fuzzer".

2019-08-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - fuzzing/utils.cc (MemoryResource): Lessen the memory limit used
    for oss-fuzz testing in order to provide more headroom and margin
    for error.

  - magick/render.c (TraceBezier): Detect arithmetic overflow and
    return errors via normal error path rather than exiting.  Fixes
    oss-fuzz 16450 "graphicsmagick:coder\_MVG\_fuzzer: Unexpected-exit
    in DefaultFatalErrorHandler".
    (PrimitiveInfoRealloc): Implement more paranoid code related to
    primitive allocation.

2019-08-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawStrokePolygon): Handle case where
    TraceStrokePolygon() returns NULL.  Addresses oss-fuzz 15516
    "graphicsmagick/coder\_MVG\_fuzzer: ASSERT: primitive\_info !=
    (PrimitiveInfo \*) NULL".
    (DrawDashPolygon): Handle case where DrawStrokePolygon() returns
    MagickFail. Also needed to address oss-fuzz 15516, since otherwise
    test-cases run for a very long time.
    (ExtractTokensBetweenPushPop): Fix non-terminal parsing loop.
    Addresses oss-fuzz 15318 "graphicsmagick/coder\_MVG\_fuzzer: Timeout
    in graphicsmagick\_coder\_MVG\_fuzzer".

2019-08-15  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/memory.h (MagickMallocAlignedArray): Add function
    attributes for added value and to quench GCC 9 warning with
    special build options enabled.

  - magick/deprecate.h (AcquireMemory): Add more function attributes
    to quench GCC 9 warning with special build options enabled.

  - magick/attribute.c (GenerateEXIFAttribute): Fix compilation
    warning in 32-bit build.

  - coders/dpx.c (AttributeToString): Eliminate annoying warnings
    from GCC 9, although the code was correct.

  - coders/msl.c (MSLStartElement): Fix defective opacity percentage
    code revealed by GCC 9 warning.

2019-08-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadMNGImage): Skip coalescing layers if there is
    only one layer.  Fixes oss-fuzz 16274
    "graphicsmagick/coder\_MNG\_fuzzer: Unexpected-exit in
    DefaultFatalErrorHandler".

2019-08-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadPNGImage): Post-processing to convert the
    image type in the PNG reader based on a specified magick prefix
    string is now disabled.  This can (and should) be done after the
    image has been returned.  Fixes oss-fuzz 16386
    "graphicsmagick:coder\_PNG8\_fuzzer: Timeout in
    graphicsmagick\_coder\_PNG8\_fuzzer".

2019-07-20  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Updates in preparation for 1.3.33 release.

2019-07-19  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Updated NEWS to reflect updates since last release.

2019-07-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (WriteOnePNGImage): Fix saving to palette when
    image has an alpha channel but no color is marked as transparent.
    Patch submitted by Przemysław Sobala via SourceForge patch #61
    "WriteOnePNGImage(): Fix saving to palette when image has an alpha
    channel but no color is marked as transparent".

  - doc/options.imdoc (characters): Fix -format documentation to
    reflect that '%r' returns the image type.  Patch submitted by
    Przemysław Sobala via SourceForge patch #60 "Fix documentation
    typo".

2019-07-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/tempfile.c (AcquireTemporaryFileDescriptor): Fix
    compilation under Cygwin.  Patch by Marco Atzeri and submitted via
    email to the graphicsmagick-help mailing list on Fri, 5 Jul 2019.

2019-06-23  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/attribute.c (GenerateEXIFAttribute): Added range checks
    and tracing.  Fixes oss-fuzz 14998
    "graphicsmagick/coder\_JPEG\_fuzzer: Heap-buffer-overflow in
    Read32s".  This is a tiny read overflow.

  - coders/miff.c (ReadMIFFImage): Similar fix as to mpc.c

  - coders/mpc.c (ReadMPCImage): Fix faulty signed overflow logic
    for profiles[i].length which still allowed overflow.  Fixes
    oss-fuzz issue 15190 "graphicsmagick/coder\_MPC\_fuzzer:
    Out-of-memory in graphicsmagick\_coder\_MPC\_fuzzer".

  - doc/options.imdoc: Add notes about security hazards due to
    commands which support a '@filename' syntax.

  - www/security.rst: Add notes about security hazards due to
    commands which support a '@filename' syntax.

2019-06-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Assure that 'token' is initialized.
    Fixes oss-fuzz issue 14897 "graphicsmagick/coder\_MVG\_fuzzer:
    Use-of-uninitialized-value in DrawImage".

  - magick/animate.c (MagickXAnimateImages): Fix memory leak of
    scene\_info.pixels.

  - magick/display.c (MagickXDisplayImage): Fix heap overwrite of
    windows->image.name and windows->image.icon\_name buffers.  It
    appears that the code assumed that CloneString() would always
    allocated a string at least MaxTextExtent in size. I assume that
    this issue has existed for a very long time since CloneString()
    was re-written many years ago.

  - coders/caption.c (ReadCAPTIONImage): The CAPTION reader did not
    appear to work at all any more.  Now it works again, but still not
    very well.

  - magick/command.c: Re-implement '@' file inclusion support for
    -comment, -draw, -format, and -label which was removed for the
    1.3.32 release.  Note that arguments from untrusted sources will
    still need to be sanitized to detect attempts to subvert this
    feature to access file data, but this feature has always been
    supported by GraphicsMagick and it originated early in the
    development of ImageMagick.

2019-06-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/utility.c (MagickStrlCat, MagickStrlCpy): Add debug
    checks enabled by MAGICK\_STRL\_CHECK.

  - magick/montage.c (MontageImages): Fix wrong length argument to
    strlcat() when building montage directory, which could allow heap
    overwrite.

  - coders/png.c (RegisterPNGImage): Pass correct size value to
    strlcat().  Under Apple's OS X (and possibly other targets)
    strlcat() writes bytes beyond what it needs to (but within the
    range it is allowed to) causing a crash due to the wrong limit
    value.  Fixes SourceForge issue #609 `gm identify foo.png` crashes
    on macOS (v 1.3.32).

  - www/Changes.rst: Update ChangeLog links due to new year, and
    1.3.32 release.

2019-06-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/bmp.c (WriteBMPImage): Detect arithmetic overflow of
    image\_size. Add more tracing. Reduce compilation warnings.
    (EncodeImage): Reduce compilation warnings.
    (WriteBMPImage): Assure that chromaticity uses double-precision
    for multiply before casting to unsigned integer.

  - coders/wpg.c (ReallocColormap): Reduce compilation warnings.

  - coders/braille.c (WriteBRAILLEImage): Reduce compilation
    warnings.

  - coders/dib.c (WriteDIBImage): Detect arithmetic overflow of
    image\_size. Reduce compilation warnings.
    (EncodeImage): Reduce compilation warnings.

  - coders/locale.c (WriteLOCALEImage): Reduce compilation warnings.

2019-06-15  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - Makefile.am (dist-zstd): Use the maximum possible compression
    level (22) when creating a Zstd-compressed tarball to get close to
    lzip/xz compression levels.

  - coders/tiff.c (ReadTIFFImage): Fix typo in initialization of
    'tile' pointer variable.

  - version.sh: Updates in preparation for 1.3.32 release.

2019-06-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - Makefile.am (release): Add a release target to make it easier to
    produce and sign the release files.  Add a zstd-compressed output
    tarball just because we can.

2019-06-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Fix typo when initializing
    number\_coordinates.  Somehow GCC and clang let this typo slip by.

2019-06-11  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dib.c (ReadDIBImage): Preserve PseudoClass opaque
    representation if ICO mask is opaque, otherwise return a
    DirectClass image.

2019-06-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Detect an error in TracePath() and
    quit rather than forging on.

2019-06-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Terminate drawing if
    DrawCompositeMask() reports failure.  Fixes oss-fuzz 12373
    "graphicsmagick/coder\_MVG\_fuzzer: Timeout in
    graphicsmagick\_coder\_MVG\_fuzzer".
    (TracePath): Terminate path parsing upon first parsing error.

2019-06-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/txt.c (ReadTXTImage): Use real a new-line character as
    line delimiter rather than '\n' string.

  - magick/annotate.c (AnnotateImage): No longer implicitly call
    TranslateText() since this is not suitable for most use-cases and
    causes additional performance impact.  The API user can perform
    such translations in advance on the text string using
    TranslateText() if need be.  No longer call StringToList() to
    split strings into an array of strings since this can lead to
    unexpected results, and a custom-splitter is more efficient.

2019-06-06  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawImage): Only support '@filename' syntax to
    read drawing primitive from a file if we are not already drawing.

  - magick/utility.c (TranslateTextEx): Remove support for reading
    from a file using '@filename' syntax due to security concerns.
    Problem was reported to us by "Battle Furry" via the
    GraphicsMagick security mail alias on June 6, 2019.

2019-06-03  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/utility.c (SetClientFilename): Reduce initialized data
    some more.

2019-06-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/nt\_base.c: Search for n019003l.pfb (the "Helvetica"-like
    font) rather than fonts.dir since fonts.dir is not present in all
    URW font collections.

  - NEWS.txt: Update news.

2019-06-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/logo.c: Tidy logo image definitions, and logo image
    output.

2019-05-23  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/mat.c: Make more data const.

2019-05-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/animate.c: Reduce initialized static allocations.

  - magick/display.c: Reduce initialized static allocations.

  - magick/widget.c (MagickSplitNDLTextToList): Add static
    implementation function.

2019-05-20  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/webp.c (RegisterWEBPImage): Use sprintf to format version
    since snprintf is not available in old Visual Studio.

2019-05-19  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dcm.c: Make more data const.

  - www/INSTALL-unix.rst: Add documentation for how to install URW
    fonts from various package management systems.

2019-05-18  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - www/authors.rst: Add authorship attribution to Samuel Thibault
    for contributing support for the Braille image format.

  - coders/braille.c: Add support for Braille image format by Samuel
    Thibault.  Patch submitted via SourceForge patch #59 "Add braille
    image format support.

2019-05-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/tempfile.c: Make more data const.

  - magick/signature.c: Make more data const.

  - magick/quantize.c: Make more data const.

  - magick/attribute.c: Make more data const.

  - coders/png.c: Make more data const.

  - coders/mpeg.c: Make more data const.

  - coders/wmf.c: Make more data const.

  - coders/tile.c: Make more data const.

2019-05-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/enum\_strings.c: Make more data const.

2019-05-15  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/magick.c: Make more data const.

  - magick/type.c (GetTypeInfoByFamily): Make more data const.

  - magick/unix\_port.c (MagickGetMMUPageSize): Decrease initialized
    data.

  - magick/utility.c (GetPageGeometry): Make more data const.

  - coders/pdf.c (WritePDFImage): Allocate working buffer on stack
    and pass as argument to EscapeParenthesis() to eliminate a thread
    safety problem and also reduce BSS size.

  - coders/webp.c (RegisterWEBPImage): Fix compiler warning.

  - coders/jbig.c (RegisterJBIGImage): Make more data const.

  - coders/pict.c (DecodeImage): Allocate output buffer used by
    ExpandBuffer() on the stack rather than as static data private to
    ExpandBuffer().  Eliminates a thread safety problem and also
    reduces BSS size.

  - coders/webp.c (RegisterWEBPImage): Reduce BSS size.

2019-05-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/jp2.c: Make more data const.

  - coders/wmf.c: Make more data const.

  - coders/ps.c (WritePSImage): Make more data const.

  - coders/ps2.c (WritePS2Image): Make more data const.

2019-05-13  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/static.c: Revert to previous 'name' storage. Callback
    functions in structure block being properly const.

  - coders/xpm.c: Make more data const.

  - coders/pnm.c: Make more data const.

  - coders/palm.c: Make more data const.

  - coders/meta.c: Make more data const.

  - coders/dcraw.c: Make more data const.

  - magick/command.c: Fix compilation problem when HasX11 is not
    defined.

2019-05-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c: Make more data const.

2019-05-11  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/webp.c (RegisterWEBPImage): Make more data const.

  - coders/svg.c (RegisterSVGImage): Reduce BSS size.

  - coders/miff.c (RegisterMIFFImage): Fix version reporting.

  - coders/ttf.c (RegisterTTFImage): Fixed reporting of FreeType
    version.

  - coders/tiff.c (RegisterTIFFImage): Reduce BSS size.

  - coders/sfw.c (ReadSFWImage): Make SFW static data completely
    const.

  - coders/ps3.c: Make PS3 static data completely const.

  - coders/pict.c: Make PICT static data completely const.

  - magick/error.c (ThrowException, ThrowLoggedException): Handle
    the case where some passed character strings refer to existing
    exception character strings.  Fixes SourceForge issue #603
    "heap-use-after-free in function ThrowLoggedException of
    magick/error.c".
    (CatchException): Restructure so there is one return point.

  - coders/miff.c (ImportRLEPixels): Fix heap overflow caused by a
    typo in the code.  Also fix undefined behavior caused by large
    left shifts of an unsigned char.  Fixes SourceForge issue #608
    "heap-buffer-overflow in ImportRLEPixels of coders/miff.c.

2019-05-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/bmp.c (ReadBMPImage): Fix subrange/scene handling in
    'ping' mode so it is like the other formats.  Only the first frame
    was being enumerated while in 'ping' mode.

2019-05-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Update news.

  - magick/utility.c (ExpandFilenames): Only expand '@filename' to a
    list of arguments read from 'filename' if the path '@filename'
    does not exist.  This fix is made based on an email posting to the
    'graphicsmagick-help' mailing list at SourceForge by "Test User"
    on Tue, 7 May 2019.

2019-05-05  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/colorspace.c: Reorder initialization of colorspace tables
    for a possible performance improvement.

  - magick/fx.c (WaveImage): Use float for sin map.

  - configure.ac: Test for float versions of math functions.

  - magick/gem.c (GenerateDifferentialNoise): Use float versions of
    math functions when available.

2019-05-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - www/INSTALL-unix.rst: Expanded configure documentation for
    --with-modules.  Added specific configure documentation for
    --with-umem and --with-mtmalloc, which may be useful on
    Solaris-derived systems.

2019-04-23  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c (VersionCommand): Show OpenMP specification
    version corresponding to version enumeration.

  - magick/locale.c (GetLocaleMessageFromTag): Eliminate clang
    warning about comparison with a constant value.

  - magick/log.c (InitializeLogInfo): Initialize LogInfo log\_configured.

2019-04-21  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/magic.c (struct): Ajust StaticMagic definition to be more
    const-friendly.

  - magick/color\_lookup.c (struct): Adjust StaticColors definition
    to be more const-friendly.

  - magick/attribute.c: Ajust tag\_table definition to be more
    const-friendly.

  - magick/log.c: Allocate LogInfo from heap as we used to do.

  - magick/locale.c (GetLocaleMessageFromTag): Adaptations to locale
    coder output changes.

  - coders/locale.c (WriteLOCALEImage): Adjust locale coder output
    to be more const.

2019-04-20  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/color\_lookup.c: Make built-in color tables fully const.

  - magick/animate.c: Use MagickXTextViewWidgetNDL() to display help
    text.

  - magick/display.c: Use MagickXTextViewWidgetNDL() to display help
    text.

  - magick/widget.c (MagickXTextViewWidgetNDL): New private function
    to display multi-line null-delimited text in an X11 widget.

  - coders/xwd.c (ReadXWDImage): Added even more XWD header
    validation logic.  Addresses problems noted by email from Hongxu
    Chen to the graphicsmagick-security mail alias on Fri, 19 Apr 2019
    and Sat, 20 Apr 2019 and entitled "Multiple crashes (FPE and
    invalid read) when processing XWD files".

2019-04-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/xwd.c (ReadXWDImage): Added even more XWD header
    validation logic.  Addresses problems noted by email from Hongxu
    Chen to the graphicsmagick-security mail alias on Wed, 17 Apr 2019
    and entitled "Multiple crashes (FPE and invalid read) when
    processing XWD files".  Also addresses additional issues noted
    that an attacker could request to allocate an arbitrary amount of
    memory based on ncolors and the claimed header size.

2019-04-14  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/xwd.c (ReadXWDImage): Add more XWD header validation
    logic.  Addresses problems noted by email from Hongxu Chen to the
    graphicsmagick-security mail alias on Sun, 14 Apr 2019 and
    entitled "Multiple crashes (FPE and invalid read) when processing
    XWD files".

2019-04-13  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pdb.c (WritePDBImage): Assure that input scanline is
    cleared in order to cover up some decoder bug.  May fix 14215
    "graphicsmagick/coder\_PDB\_fuzzer: Use-of-uninitialized-value in
    WritePDBImage", which I have not been able to reproduce.

  - magick/render.c (DrawPrimitive): Check primitive point x/y
    values for NaN.
    (DrawImage): Fix oss-fuzz issue 14173
    "graphicsmagick/coder\_MVG\_fuzzer: Integer-overflow in DrawImage".

  - magick/pixel\_cache.c (SetNexus): Fix oss-fuzz issue 14208
    "graphicsmagick/coder\_MVG\_fuzzer: Integer-overflow in SetNexus".

2019-04-11  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/display.c: Add even more const declarations.

  - coders/mat.c (WriteMATLABImage): Add completely missing error
    handling.  Fixes SourceForge issue #604 "heap-buffer-overflow in
    function WriteMATLABImage of coders/mat.c".

2019-04-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pdb.c (WritePDBImage): Fix SourceForge issue #605
    "heap-buffer-overflow in function WritePDBImage of coders/pdb.c".

  - magick/widget.c: Add many const declarations.

  - magick/display.c: Incorporate and eliminate display.h. Add many
    const declarations.

  - magick/animate.c: Incorporate and eliminate animate.h. Add many
    const declarations.

2019-04-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/wmf.c (ReadWMFImage): Reject WMF files with an empty
    bounding box.  Fixes SourceForge issue #606 "Division by Zero in
    coders/wmf.c".

2019-04-07  Fojtik Jaroslav  <JaFojtik@seznam.cz>

  - magick/nt\_base.c Fix a problem of finding ghostscript fonts.
    Variable "font\_dir" was useless and thus removed. No need to copy
    text multiple times.  Use const char gs\_font\_dir[] instead of
    pointer.

2019-04-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/xwd.c (ReadXWDImage): Perform more header validations and
    a file size validation in order to reject files with bogus
    headers.
    (WriteXWDImage): Fix SourceForge issue #599
    "heap\_buffer\_overflow\_WRITE in function WriteXWDImage of
    coders/xwd.c".

2019-04-05  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/svg.c (SVGStartElement): Fix stack buffer overflow while
    parsing quoted font family value.  Fixes SourceForge issue #600
    "stack-buffer-overflow in function SVGStartElement of
    coders/svg.c".

  - coders/miff.c (ReadMIFFImage): Detect end of file while reading
    RLE packets.  Fixes SourceForge issue #598 "heap-buffer-overflow
    in function ReadMIFFImage of coders/miff.c".

2019-04-03  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/xwd.c (ReadXWDImage): Fix heap buffer overflow while
    reading DirectClass XWD file.  Fixes SourceForge issue #597
    "heap-buffer-overflow in function ReadXWDImage of coders/xwd.c".

2019-04-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadMNGImage): Fix small buffer overflow (one
    PixelPacket) of image colormap.  Fixes SourceForge issue #596
    "heap-buffer-overflow in function CloneImage of magick/image.c".

  - magick/colormap.c (ReallocateImageColormap): New function to
    reallocate an image colormap.

  - coders/logo.c: Make more static data const.

  - magick/module\_aliases.h: Make more static data const.

  - magick/static.c: Make more static data const.

2019-04-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/log.c (LogMagickEventList): Log elapsed time with
    microsecond precision.

2019-03-31  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/mpc.c (ReadMPCImage): Deal with a profile length of zero,
    or an irrationally large profile length.  Fixes SourceForge issue
    #601 "memory leak in function ReadMPCImage of coders/mpc.c ".

  - magick/xwindow.c (MagickXGetWindowInfo): Deal with the unlikely
    case that the memory allocation for window->segment\_info
    fails. Fixes SourceForge #595 "use allocate memory before null
    check" as pertains to magick/xwindow.c.

  - magick/segment.c (Classify): Add check for memory allocation
    failure when allocating cluster array. Fixes SourceForge #595 "use
    allocate memory before null check" as pertains to
    magick/segment.c.

  - coders/pdb.c (ReadPDBImage): Fix use of allocated memory before
    null check.  Fixes SourceForge #595 "use allocate memory before
    null check" as pertains to coders/pdb.c.

2019-03-30  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (AllocateThreadViewSet): Simplify the image
    view model by adding NexusInfo to the View structure (rather than
    referencing it via a pointer) to lessen the number of required
    per-thread allocations and to improve locality of reference.

2019-03-22  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/wpg.c (WPG1\_Palette): Change to a static declaration.

  - coders/dcm.c: dicom\_info array is now fully in the data segment.

2019-03-18  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - configure.ac: Add support for using the Solaris mtmalloc
    library.  This is primarily for testing or as an alternative to
    Solaris umem.
    Stop using posix\_memalign() until it is uniformly more mature and
    reliably quick.

2019-03-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (SetNexus): Smallest staging-area
    allocation is cache line size so declare it as such.

  - magick/fx.c: Functions in the fx module which return a new Image
    should return a null Image if an exception was thrown.  Also,
    assure that user has an opportunity to see the exception which was
    thrown.

  - magick/error.c (ThrowLoggedException): Throwing an exception is
    now thread-safe.

  - magick/pixel\_cache-private.h: Moved pixel cache private
    definitions to private header.

2019-03-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (SetNexus): Pass x, y, columns, and rows
    rather than a pointer to RectangleInfo.  This should be easier to
    inline on modern CPUs.

2019-03-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (SetNexus): Cache resource limits in
    CacheInfo rather than repeatedly calling into the resource code in
    order to lessen the overhead of performing resource limit checks
    on the pixel cache views.

  - magick/resource.c (AcquireMagickResource): Use a lock for each
    resource in order to lessen contention.  Return a maximum 64-bit
    integer value if the resource has not been limited.  Previously
    returned -1 in this case but this was not documented.

2019-03-07  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/import.c (ImportViewPixelArea): If range between max and
    min is less than MagickEpsilon, produce a black image rather than
    throwing an exception.

  - coders/mat.c (ReadMATImage): Fix memory leak on unexpected end
    of file.  Fixes oss-fuzz 13556 "graphicsmagick/coder\_MAT\_fuzzer:
    Direct-leak in ReadMATImage". (Credit to OSS-Fuzz)

2019-03-06  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/mat.c (ReadMATImage): Quit if image scanlines are not
    fully populated due to exception.  Fixes oss-fuzz 13530
    "graphicsmagick/coder\_MAT\_fuzzer: Use-of-uninitialized-value in
    InsertComplexFloatRow". (Credit to OSS-Fuzz)

2019-03-04  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/txt.c (ReadTXTImage): Don't start new line if x\_max <
    x\_min.  Avoids calling SetImagePixels() with a width of zero.
    Related to oss-fuzz 13521 "graphicsmagick/coder\_TEXT\_fuzzer:
    Floating-point-exception in SetNexus". (Credit to OSS-Fuzz)

  - magick/pixel\_cache.c (SetNexus): Report error for empty region
    rather than crashing due to divide by zero exception. This is a
    new bug due to yesterday's changes.  Fixes oss-fuzz 13521
    "graphicsmagick/coder\_TEXT\_fuzzer: Floating-point-exception in
    SetNexus". (Credit to OSS-Fuzz)

2019-03-03  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - design/pixel-cache.dot: Update design dot diagram to remove
    IsNexusInCore and add CompositeCacheNexus.

  - magick/pixel\_cache.c (SetNexus): Apply resource limits to pixel
    nexus allocations using the same limits (total pixels, width,
    height, memory) as applied to the whole image since some requests
    are directly influenced by the input file.  Add yet more tests for
    arithmetic overflow.  Whole source module is re-arranged so that
    static functions are in order of dependency so that forward
    prototype declarations are no longer needed.  Fixes oss-fuzz 13210
    "graphicsmagick/coder\_MVG\_fuzzer: Integer-overflow in
    SetNexus". (Credit to OSS-Fuzz)

2019-03-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (OpenCache): Use unsigned 64-bit value to
    store CacheInfo offset and length as well as for the total pixels
    calculation.  Add some more arithmetic overflow detections.

  - coders/topol.c (ReadTOPOLImage): Report a corrupt image
    exception "Unexpected end-of-file" if reader encounters end of
    file while reading header rows.  Addresses oss-fuzz 7981
    "graphicsmagick/coder\_TOPOL\_fuzzer: Use-of-uninitialized-value in
    InsertRow". (Credit to OSS-Fuzz)

  - coders/mat.c (ReadMATImage): Report a corrupt image exception
    "Unexpected end-of-file" if reader encounters end of file while
    reading scanlines.  Also added some helpful traces.  Hopefully
    addresses oss-fuzz 13445 "graphicsmagick/coder\_MAT\_fuzzer:
    Use-of-uninitialized-value in IsGrayImage". (Credit to OSS-Fuzz)

2019-02-26  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/image.h ("C"): Include as "magick/image-private.h" as the
    other headers are.
    ("C"): Include "magick/image-private.h" inside the protective
    MAGICK\_IMPLEMENTATION guard, as it should have been.  This error
    broke the oss-fuzz build.

2019-02-24  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/image-private.h (\_ImageExtra): Put ImageExtra definition
    in a private header file so that its definition may be accessed
    directly by library internals.  Add some accessor macros to
    provide access and update code to use them.

  - coders/wpg.c (ReallocColormap): Make sure that there is not a
    heap overwrite if the number of colors has been reduced.  Thanks
    to Jaroslav Fojtik for giving me a heads up about this.

2019-02-23  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/monitor.c (MagickMonitorActive): Add new private function
    to test if a progress monitor is active.  Update all progress
    monitor code in loops to use this information, while also updating
    code to hopefully address concerns expressed by Hongxu Chen about
    data races on the graphicsmagick-bugs mailing list starting on
    February 6, 2019.

2019-02-21  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/mpc.c (ReadMPCImage): Tally directory length to avoid
    death by strlen().

  - coders/miff.c (ReadMIFFImage): Tally directory length to avoid
    death by strlen().  Fixes oss-fuzz 13190
    "graphicsmagick/coder\_MIFF\_fuzzer: Timeout in
    graphicsmagick\_coder\_MIFF\_fuzzer". (Credit to OSS-Fuzz)

2019-02-17  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/svg.c (ReadSVGImage): Don't call xmlCleanupParser()
    in module code since this may cause other libxml users to fail.

  - coders/msl.c (ProcessMSLScript): Don't call xmlCleanupParser()
    in module code since this may cause other libxml users to fail.

  - magick/render.c (DrawDashPolygon): (DrawDashPolygon): Don't read
    beyond end of dash pattern array.  This is a second instance of
    issue identified by SourceForge issue #591.  Fixes oss-fuzz 13160
    "graphicsmagick/coder\_MVG\_fuzzer: Heap-buffer-overflow in
    DrawDashPolygon".  The earlier attempt to fix this problem today
    broke dash patterns entirely.  (Credit to OSS-Fuzz)

  - magick/annotate.c (RenderFreetype): Eliminate memory leak of
    GlyphInfo.image (type FT\_Glyph) while rendering some FreeType
    fonts such as the one we use now in the Magick++ test suite.

2019-02-16  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/render.c (DrawDashPolygon): Avoid reading one beyond
    length of dash pattern array, which is terminated by value 0.0.
    Fixes SourceForge issue #591 "Heap buffer overflow in
    DrawDashPolygon when parsing SVG images".
    (DrawPrimitive): Add arithmetic overflow checks when converting
    computed coordinates from 'double' to 'long'.
    (DrawImage): Don't destroy draw\_info in graphic\_context when
    draw\_info has not been allocated yet.  Problem reported via email
    by Sami Supperi on Thu, 14 Feb 2019.

  - coders/jpeg.c (ReadJPEGImage): JPEG files are observed to
    provide compression ratios as high as 2500 so allow for that.
    Also, the test for "Unreasonable dimensions" delivered yesterday
    was flawed since magick\_rows and magick\_columns are only set if a
    desired image size was provided.  Fixes SourceForge issue 592
    "Non-malicious JPEG file fails with "Unreasonable dimensions"".

  - coders/tiff.c (ReadTIFFImage): Only disassociate alpha channel
    for images where photometic is PHOTOMETRIC\_RGB. Fixes oss-fuzz
    13115 "graphicsmagick/coder\_PTIF\_fuzzer:
    Use-of-uninitialized-value in DisassociateAlphaRegion". (Credit to
    OSS-Fuzz)

2019-02-15  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/jpeg.c (ReadJPEGImage): Base test for "Unreasonable
    dimensions" on original JPEG dimensions and not the scaled
    dimensions.  Fixes SourceForge issue 593 "gm convert: Insufficient
    image data in file when hinting input image".

2019-02-13  Troy Patteson  <troyp@ieee.org>

  - PerlMagick/Magick.xs (Mogrify): Add decorate argument to Annotate.

  - PerlMagick/Magick.xs (Mogrify): Remove reference to undefined
    Annotate argument.

2019-02-12  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/tiff.c (ReadTIFFImage): For planar TIFF, make sure that
    pixels are initialized in case some planes are missing.  Fixes
    oss-fuzz 13046 "graphicsmagick/coder\_PTIF\_fuzzer:
    Use-of-uninitialized-value in DisassociateAlphaRegion". (Credit to
    OSS-Fuzz)

2019-02-11  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pdf.c (WritePDFImage): Make sure to free 'xref' before
    returning.  Similar to ImageMagick CVE-2019-7397 "In ImageMagick
    before 7.0.8-25, several memory leaks exist in WritePDFImage in
    coders/pdf.c.".  Thanks to Petr Gajdos for bringing this issue to
    our attention.

2019-02-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/wpg.c (ReadWPGImage): Use a different way to reallocate
    the colormap which preserves existing content, but also updates
    image->colors and assures that added palette entries are
    initialized.

  - coders/png.c (ReadMNGImage): Bound maximum loop iterations by
    subrange as a primitive means of limiting resource consumption.
    This should finally resolve oss-fuzz 12738
    "graphicsmagick/enhance\_fuzzer: Out-of-memory in
    graphicsmagick\_enhance\_fuzzer". (Credit to OSS-Fuzz)

  - coders/tiff.c (ReadTIFFImage): Assure that opacity channel is
    initialized in the RGBAStrippedMethod case.  Convert
    'CorruptImageError' encountered while testing for more frames to
    'CorruptImageWarning' so we return the frames already read.
    Second try at fixing oss-fuzz 11896
    "graphicsmagick/coder\_PTIF\_fuzzer: Use-of-uninitialized-value in
    VerticalFilter".

  - coders/dpx.c (AttributeToString): Eliminate clang
    "-Wstring-plus-int" warning observed in oss-fuzz build.

  - coders/cineon.c (AttributeToString): Eliminate clang
    "-Wstring-plus-int" warning observed in oss-fuzz build.

2019-02-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/pict.c (DecodeImage): Avoide a one-byte over-read of
    pixels heap allocation.  The cause of the over-read is not yet
    understood.  Fixes oss-fuzz 12019
    "graphicsmagick/coder\_PICT\_fuzzer: Heap-buffer-overflow in
    ExpandBuffer". (Credit to OSS-Fuzz)

  - coders/wpg.c (ReadWPGImage): Assure that all colormap entries
    are initialized.  Fixes oss-fuzz 12614
    "graphicsmagick/enhance\_fuzzer: Use-of-uninitialized-value in
    EnhanceImage". (Credit to OSS-Fuzz)

  - coders/tiff.c (ReadTIFFImage): Make sure that image is in
    DirectClass mode and ignore any claimed colormap when the image is
    read using the RGBAStrippedMethod, RGBATiledMethod, or
    RGBAPuntMethod cases.  Fixes oss-fuzz 12195
    "graphicsmagick/coder\_PTIF\_fuzzer: Use-of-uninitialized-value in
    ExportGrayQuantumType". (Credit to OSS-Fuzz)

  - coders/miff.c (ReadMIFFImage): Improve pixel buffer calculations
    to defend against overflow.  Assure that zlib and bzlib decode the
    expected number of bytes for a pixel row.  Fixes oss-fuzz issue
    12448 "graphicsmagick/coder\_MIFF\_fuzzer:
    Use-of-uninitialized-value in RGBTransformPackets". (Credit to
    OSS-Fuzz)

2019-02-08  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (ReadMNGImage): Quit processing and report error
    upon failure to insert MNG background layer.  Fixes oss-fuzz 12738
    "graphicsmagick/enhance\_fuzzer: Out-of-memory in
    graphicsmagick\_enhance\_fuzzer". (Credit to OSS-Fuzz)

2019-02-03  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/dib.c (ReadDIBImage, WriteDIBImage): Improve buffer-size
    calculations to guard against buffer overflows.  The reader
    version was not as complete as it should have been, whereas the
    writer version did not guard against arithmetic overflow at all.

  - coders/bmp.c (ReadBMPImage, WriteBMPImage): Improve buffer-size
    calculations to guard against buffer overflows.  This is a
    follow-on fix to the previous fix submitted for SourceForge issue
    #582 "heap-buffer-overflow in ReadBMPImage of bmp.c" which is now
    also identified as CVE-2018-20185.

  - www/Hg.rst: Updates to reflect current usage and availability.

  - www/authors.rst: Promote Troy Patteson to the active contributor
    category.

2019-02-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/version.h.in: Rotate ChangeLog and update copyright
    statements for the new year.

2019-01-30  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/webp.c (WriteWEBPImage): Patch by Przemysław Sobala to
    support WebP 'use\_sharp\_yuv' option ("if needed, use sharp (and
    slow) RGB->YUV conversion") via `-define webp:use-sharp-yuv=true`.

2019-01-05  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (SetNexus): Merge IsNexusInCore()
    implementation code into SetNexus() and add check for if
    cache\_info->pixels is null.  Fixes SourceForge issue #588 "Bug in
    IsNexusInCore()".

  - configure.ac (DcrawExtraOptions): Request TIFF output from dcraw
    if build supports TIFF format in order to obtain more metadata.
    This allows obtaining some metadata from standard TIFF tags
    (e.g. camera make, model, and dcraw version), and any attached ICC
    profile, but not specifically EXIF data since we don't support
    extracting EXIF data from TIFF yet. Inspired by SourceForge issue
    589 "Identify lack of data (no Exif) in RAW formats".
