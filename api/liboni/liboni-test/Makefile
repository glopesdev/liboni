# Examples:
# make 			// Makes all test programs
# make debug 	// Makes all test programs with debug symbols
# make profile 	// Makes all test programs and links in the gperftool's profiler

CC=cc
CFLAGS=-O3 -Wall
LDFLAGS=-loni -ldl

.PHONY: all
all: oni-repl cobs-test ## Build basic oni-repl and test functions

.PHONY: debug
debug: CFLAGS += -DDEBUG -g3 ## Build with debug symbols
debug: all

.PHONY: profile
profile: LDFLAGS += -lprofiler ## Link in the perftools profiler
profile: all

cobs-test: cobs_test.c testfunc.c ## Make COBS test program
	@echo Making $@
	$(CC) $(CFLAGS) $^ -lm $(LDFLAGS) -o $@

oni-repl: main.c ## Make simple oni-repl acquisition software
	@echo Making $@
	$(CC) $(CFLAGS) $? -lm -lpthread $(LDFLAGS) -o $@

.PHONY: clean
clean: ## Clean build artifacts
	rm ./oni-repl ./cobs-test

.PHONY: help
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'
