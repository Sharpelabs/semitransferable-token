PATCH         = applyHarness.patch
CONTRACTS_DIR = ../src
MUNGED_DIR    = munged

help:
	@echo "usage:"
	@echo "  make clean:  remove all generated files (those ignored by git)"
	@echo "  make munged: create $(MUNGED_DIR) directory by applying the patch file to $(CONTRACTS_DIR)"
	@echo "  make record: record a new patch file capturing the differences between $(CONTRACTS_DIR) and $(MUNGED_DIR)"

munged:  $(wildcard $(CONTRACTS_DIR)/*.sol) $(PATCH)
	@test -d ${MUNGED_DIR} && rm -rI ${MUNGED_DIR} || echo "creating ${MUNGED_DIR} from scratch..."
	cp -r $(CONTRACTS_DIR) $@
	patch -p0 -d $@ < $(PATCH)

record:
	diff -ruN $(CONTRACTS_DIR) $(MUNGED_DIR) | sed 's+\.\./src/++g' | sed 's+munged/++g' > $(PATCH)

.PHONY: help munged record
