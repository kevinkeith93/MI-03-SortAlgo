SHELL = /bin/bash

AllDirs := $(shell ls -R | grep '^\./.*:$$' | awk '{gsub(":","");print}') .
Sources := $(foreach n,$(AllDirs) , $(wildcard $(n)/*.cpp))
Objs := $(patsubst %.cpp,%.o, $(Sources))
Deps := $(patsubst %.cpp,%.d, $(Sources))

Bin := SortAlgo

AllLibs : $(Bin)

CC = g++
CXXFLAGS = -g -O2 -fPIC -Wall
CPPFLAGS = $(foreach n,$(AllDirs) , -I$(n))

$(Bin) : $(Objs)
	g++ $(Objs) -o $@

%.d : %.cpp
	$(CC) -MT"$(<:.cpp=.o) $@" -MM $(CXXFLAGS) $(CPPFLAGS) $< > $@

sinclude $(Deps)

.PHONY : clean

clean: 
	rm -f $(Objs) $(Deps) $(StaticLib) $(DynamicLib) $(Bin)

