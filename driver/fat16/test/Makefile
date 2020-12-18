CXX     := g++
LIB_DIR := ../lib
OBJ_DIR := obj
BIN_DIR := bin
MKDIR   := mkdir -p

CFLAGS := -Wall -Wextra -Werror -DNDEBUG -std=c89 -fvisibility=hidden
CXXFLAGS := -Wall -Wextra -Werror -std=c++11

all: test

TEST_SRCS := AppendSmallFileTest.cpp \
		Common.cpp \
		DeleteDirectoryTest.cpp \
		DeleteFileTest.cpp \
		FilenameTest.cpp \
		linux_hal.cpp \
		LsTest.cpp \
		main.cpp \
		MkdirTest.cpp \
		ReadEmptyFileTest.cpp \
		ReadLargeFileTest.cpp \
		ReadSmallFileTest.cpp \
		RmdirTest.cpp \
		Test.cpp \
		WriteEraseContentTest.cpp \
		WriteLargeFileTest.cpp \
		WriteSmallFileTest.cpp
TEST_OBJS := $(TEST_SRCS:%.cpp=$(OBJ_DIR)/%.o)


code:
	@ echo $(TEST_OBJS)


test: $(TEST_OBJS) $(LIB_DIR)/libfat16.a
	#$(MKDIR) $(BIN_DIR)
	$(CXX) -o $@ $^

$(OBJ_DIR)/%.o: %.cpp
	$(CXX) -c $< -o $@

clean:
	rm $(OBJ_DIR)/*
	clear

re: clean all




