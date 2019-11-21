---
title: 用Make 编译Python项目
tags:
  - linux
  - make
  - python
url: 534.html
id: 534
categories:
  - linux server
  - Python
date: 2013-03-07 13:59:49
---

python编译后性能并不会提升，但是1来可以减少文件量，2来可以对明文的代码封装，还是挺好的。 makefile #编译后文件的去处 BINDIR := ../bin #源代码所在目录 BASEDIR := ../src #编译参数 可选 DBGFLAGS ?= -O ifeq ($(findstring -O,$(DBGFLAGS)),-O) COM := .pyo else COM := .pyc endif define dirflow FILES := $(wildcard $(1)*) DIRS := $$(foreach e, $$(FILES), $$(if $$(wildcard $$(e)/*), $$(eval DIRS := $$(DIRS) $$(e)))) FILES := $$(filter-out $$(DIRS),$$(FILES)) ALLFILES := $$(ALLFILES) $$(FILES) $$(foreach e,$$(DIRS),$$(eval $$(call dirflow,$$(e)/))) endef $(eval $(call dirflow ,$(BASEDIR))) sources := $(filter %.py,$(ALLFILES)) clean\_com := $(patsubst %.py, \_clean_%.py, $(sources)) MKDIR := mkdir -p TEST  := test -d RM    := rm -rf .PHONY : all all:$(sources) %.py:bin\_dir @echo Go into $(dir $@) $(shell $(TEST) $(subst $(BASEDIR),$(BINDIR),$(dir $@)) || $(MKDIR) $(subst $(BASEDIR),$(BINDIR),$(dir $@))) python $(DBGFLAGS) -m py\_compile $@ mv $(patsubst %.py, %$(COM), $@) $(subst $(BASEDIR),$(BINDIR),$(dir $@)) @echo Compile $@ done. bin\_dir: $(shell $(TEST) $(BINDIR) || $(MKDIR) $(BINDIR)) .PHONY: clean clean: $(clean\_com) $(RM) $(BINDIR) $(clean\_com):bin\_dir $(RM)$(patsubst \_clean\_%.py, %$(COM), $@)