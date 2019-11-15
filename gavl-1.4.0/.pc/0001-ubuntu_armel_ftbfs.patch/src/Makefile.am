if HAVE_LIBPNG
png_programs = \
colorspace_test \
fill_test \
blend_test \
scaletest \
convolvetest \
deinterlacetest
else
png_programs =
endif

noinst_PROGRAMS = \
$(png_programs) \
benchmark \
colorspace_time \
deinterlace_time \
dump_frame_table \
pixelformat_penalty \
plot_scale_kernels \
scale_time \
timescale_test \
volume_test

pixelformat_penalty_SOURCES = pixelformat_penalty.c
pixelformat_penalty_LDADD = ../gavl/libgavl.la

benchmark_SOURCES = benchmark.c
benchmark_LDADD = ../gavl/libgavl.la @RT_LIBS@


volume_test_SOURCES = volume_test.c
volume_test_LDADD = ../gavl/libgavl.la

dump_frame_table_SOURCES = dump_frame_table.c
dump_frame_table_LDADD = ../gavl/libgavl.la


colorspace_test_SOURCES = colorspace_test.c
colorspace_test_LDADD = ../gavl/libgavl.la -lpng -lz

fill_test_SOURCES = fill_test.c
fill_test_LDADD = ../gavl/libgavl.la -lpng -lz

blend_test_SOURCES = blend_test.c
blend_test_LDADD = ../gavl/libgavl.la -lpng -lz

scaletest_SOURCES = scaletest.c
scaletest_LDADD = ../gavl/libgavl.la -lpng -lz

convolvetest_SOURCES = convolvetest.c pngutil.c
convolvetest_LDADD = ../gavl/libgavl.la -lpng -lz

deinterlacetest_SOURCES = deinterlacetest.c pngutil.c
deinterlacetest_LDADD = ../gavl/libgavl.la -lpng -lz


plot_scale_kernels_SOURCES = plot_scale_kernels.c
plot_scale_kernels_LDADD = ../gavl/libgavl.la

scale_time_SOURCES = scale_time.c timeutils.c
scale_time_LDADD = ../gavl/libgavl.la

deinterlace_time_SOURCES = deinterlace_time.c timeutils.c
deinterlace_time_LDADD = ../gavl/libgavl.la

colorspace_time_SOURCES = colorspace_time.c
colorspace_time_LDADD = ../gavl/libgavl.la

timescale_test_SOURCES = timescale_test.c
timescale_test_LDADD = ../gavl/libgavl.la

noinst_HEADERS = pngutil.h timeutils.h

EXTRA_DIST = \
gen_colorspace_tables.c \
gen_ssim_table.c
