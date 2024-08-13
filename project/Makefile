#Targets
#compile our source file into object file
#Variables in Make file

#CC: Programs for compiling c programs; default gcc
#CXX: Programs for compiling C++ programs; default g++
#CFLAGS: Extra flags to give to the C complier
#CXXFLAGS: EXtra Flags to give to the C++ Compiler
#CPPFLAGS: EXtra Flags to give to the C preprocessor 
#LDFLAGS: Extra Flag to give to the linker

CC = gcc 
CFLAGS = -Wall -Wextra
LDFLAGS = -lmath

INCLUDE_DIR = include
SOURCE_DIR = src
BUILD_DIR = build

EXECUTABLE_NAME = helloworld

CPPFLAGS = -I $(INCLUDE_DIR)

COMPILER_CALL = $(CC) $(CFLAGS) $(CPPFLAGS)


CSOURCE_FILES = $(wildcard $(SOURCE_DIR)/*.c)
COBJECTS_FILES = $(patsubst $(SOURCE_DIR)/%.c,$(BUILD_DIR)/%.o, $(CSOURCE_FILES))

all: create link

create:
	mkdir -p $(BUILD_DIR)

link: create $(COBJECTS_FILES)
	echo $(CSOURCE_FILES)
	echo $(COBJECTS_FILES)
	$(COMPILER_CALL) $(COBJECTS_FILES) -o $(BUILD_DIR)/$(EXECUTABLE_NAME)

execute:
	./$(BUILD_DIR)/$(EXECUTABLE_NAME)
clean:
	rm -rf $(BUILD_DIR)
	rm -rf $(BUILD_DIR)/*.o
	rm -rf $(BUILD_DIR)/$(EXECUTABLE_NAME)


#to complie more source files at a time
##Patterns
$(BUILD_DIR)/%.o: $(SOURCE_DIR)/%.c
	$(COMPILER_CALL) -c $< -o $@
