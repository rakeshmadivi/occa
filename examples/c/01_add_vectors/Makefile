PROJ_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

ifndef OCCA_DIR
  include $(PROJ_DIR)/../../../scripts/Makefile
else
  include ${OCCA_DIR}/scripts/Makefile
endif

#---[ COMPILATION ]-------------------------------
headers = $(wildcard $(incPath)/*.hpp) $(wildcard $(incPath)/*.tpp)
sources = $(wildcard $(srcPath)/*.cpp)

objects = $(subst $(srcPath)/,$(objPath)/,$(sources:.cpp=.o))

${PROJ_DIR}/main: $(objects) $(headers) ${PROJ_DIR}/main.c
	$(cCompiler) $(cCompilerFlags) -Wno-variadic-macros -o ${PROJ_DIR}/main $(flags) $(objects) ${PROJ_DIR}/main.c $(paths) -L${OCCA_DIR}/lib $(linkerFlags)

$(objPath)/%.o:$(srcPath)/%.cpp $(wildcard $(subst $(srcPath)/,$(incPath)/,$(<:.cpp=.hpp))) $(wildcard $(subst $(srcPath)/,$(incPath)/,$(<:.cpp=.tpp)))
	$(compiler) $(compilerFlags) -Wno-variadic-macros -o $@ $(flags) -c $(paths) $<

clean:
	rm -f $(objPath)/*;
	rm -f ${PROJ_DIR}/main
#=================================================
