PATTERN_PLAYGROUND_DIR=../../trace-pattern-finder/PatternPlayGround
TRACER_DIR= $(PATTERN_PLAYGROUND_DIR)/Tracer/DataFlowSanitizer/Automated
MINIZINC_FINDER_DIR= $(PATTERN_PLAYGROUND_DIR)/PatternFinder/MiniZinc

# Placed here to override the recipe in $(TRACER_DIR)/Makefile.
%.dzn: %.input
	$(PROCESS_TRACE) --output-format=minizinc --match-regions-only print $< > $@

include $(TRACER_DIR)/Makefile
include ../common.mk

CXXFLAGS += -std=c++1y

CXXLINKFLAGS = -lfreeimage

# Internal loop IDs for trace filtering, see 'mark' enum in source code.
LOOP60= 0
LOOP62= 1
LOOP33= 2

BENCHMARK_ARGS=

BENCHMARK_LOOPS= 60 62 33
ALL_PREFIX= $(addprefix mandelbrot.loop, $(BENCHMARK_LOOPS))

all-maps-szn: $(ALL_MAPS_SZN)
all-reductions-szn: $(ALL_REDUCTIONS_SZN)
all-trace-pdf: $(ALL_TRACE_PDF)
all-maps-pdf: $(ALL_MAPS_PDF)
all-reductions-pdf: $(ALL_REDUCTIONS_PDF)

mandelbrot.loop%.bin: src/mandel-instrumented.cpp src/save_image.cpp src/utils.cpp tracing.loop%.o
	$(CXX) $(CXXFLAGS) $(CXXLINKFLAGS) $^ -o $@

