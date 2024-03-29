######################################################################
# Recipes.
######################################################################
include Makefile.default
include Makefile.var
include Makefile.fun

#
# Phony 
# ----------------------------- #
# ----------------------------- #
.PHONY: all clean cleanall debug help

#
# Recipes
#

# TODO there is another use case here
# Where the user might want to make multiple
# programs in one folder.
# Current implementation requires each prog
# has it's own folder.
all: $(objs)
>   @echo Making Main
>   $(f_check_subdirs_for_libs)
>   $(verbose)$(compile)

$(objs): $(srcs) $(incs)
>   $(verbose)$(compiler) $(CCFLAGS) $(include_dirs) -c $(realpath $<) -o $@


# TODO there is another use case here
# Where the user might want to make multiple
# libraries in one folder.
# Current implementation requires each library
# has it's own folder.
shared: $(objs)
>   @echo Making Shared lib
>   $(f_check_subdirs_for_libs)
>   $(verbose)$(compile_shared_lib)

clean:
>   $(f_clean_main)

cleanall: 
>   $(if $(findstring yes,$(recursive)),$(clean_subdirectories),)
>   $(f_clean_main)

debug: CPPFLAGS += -g 
debug: all 

debug-shared: CPPFLAGS += -g
debug-shared: shared

help:
>   @$(MAKE) --print-data-base --question all | \
	grep -v -e '^no-such-target' -e '^makefile' |       \
    awk '/^[^.%][-A-Za-z0-9_]*:/                        \
          { print substr($$1, 1, length($$1)-1) }' |      \
    sort 

# Alternatively:
# awk '/^[^.%][-A-Za-z0-9_]*:/ { print }' |      \

print-%: ; @echo $* = $($*)

print-all: ;
>    @echo ------------------------------ General
>    @echo SHELL                = $(SHELL)
>    @echo name                 = $(name) 
>    @echo ------------------------------------------ Shared library
>    @echo shl_name           = $(shl_name) 
>    @echo shl_version        = $(shl_version)
>    @echo shl_release_number = $(shl_release_number) 
>    @echo shl_minor_number   = $(shl_minor_number)
>    @echo shl_linker_name    = $(shl_linker_name)
>    @echo shl_soname         = $(shl_soname)
>    @echo shl_fullname       = $(shl_fullname)

>    @echo ------------------------------------------ Directories  
>    @echo subdirs              = $(subdirs) 
>    @echo CURR_DIR             = $($CURR_DIR)
>    @echo include_dirs = $(include_dirs) 
>    @echo library_dirs = $(library_dirs)
>    @echo libraries    = $(libraries)

>    @echo ---------------------------- Compiler 
>    @echo CC                   = $(CC) 
>    @echo CXX                  = $(CXX) 
>    @echo compiler             = $(compiler)

>    @echo ---------------------------- Flags
>    @echo shared               = $(shared)
>    @echo CFLAGS               = $(CFLAGS)
>    @echo CPPFLAGS             = $(CPPFLAGS)
>    @echo LDFLAGS              = $(LDFLAGS)

>    @echo ---------------------------- Sources 
>    @echo c_srcs       = $(c_srcs)
>    @echo c_srcs       = $(c_srcs)
>    @echo cxx_srcs     = $(cxx_srcs)
>    @echo ---------------------------- Objects 
>    @echo cxx_objs     = $(cxx_objs)
>    @echo c_objs       = $(c_objs)
>    @echo ---------------------------- Headers 
>    @echo h            = $(h)
>    @echo hpp          = $(hpp)
>    @echo cap_h        = $(cap_h)
