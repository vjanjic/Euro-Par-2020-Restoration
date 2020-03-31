PATTERN_PLAYGROUND_DIR=../../trace-pattern-finder/PatternPlayGround
TRACER_DIR= $(PATTERN_PLAYGROUND_DIR)/Tracer/DataFlowSanitizer/Automated
MINIZINC_FINDER_DIR= $(PATTERN_PLAYGROUND_DIR)/PatternFinder/MiniZinc

# Placed here to override the recipe in $(TRACER_DIR)/Makefile.
%.dzn: %.input
	$(PROCESS_TRACE) --output-format=minizinc --match-regions-only print $< > $@

include $(TRACER_DIR)/Makefile
include ../common.mk

CXXFLAGS +=

CXXLINKFLAGS = -lm

# Internal loop IDs for trace filtering, see 'mark' enum in source code.
LOOP285= 0
LOOP290= 1
LOOP373= 2

BENCHMARK_ARGS= 1 ../input/in_4.txt prices.txt

BENCHMARK_LOOPS= 285 290 373
ALL_PREFIX= $(addprefix blackscholes.loop, $(BENCHMARK_LOOPS))

all-maps-szn: $(ALL_MAPS_SZN)
all-reductions-szn: $(ALL_REDUCTIONS_SZN)
all-trace-pdf: $(ALL_TRACE_PDF)
all-maps-pdf: $(ALL_MAPS_PDF)
all-reductions-pdf: $(ALL_REDUCTIONS_PDF)

blackscholes.loop%.bin: src/blackscholes-instrumented.c tracing.loop%.o
	$(CXX) $(CXXFLAGS) $(CXXLINKFLAGS) $^ -o $@

foo.bin: src/blackscholes-instrumented.c
	$(CXX) $(CXXFLAGS) $(CXXLINKFLAGS) $^ -o $@

