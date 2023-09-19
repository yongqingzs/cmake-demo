# 可执行文件名
TARGET = main

# 可执行文件的路径
TARGET_DIR = bin

# gcc类型
CC = gcc

# 存放中间文件的路径
BUILD_DIR = build

#存放.c 源文件的文件夹
SRC_DIR = \
	./src \
    ./src/hadb \
    ./src/popup \
    ./src/pso \
    ./src/simulator \

# 存放头文件的文件夹
INC_DIR = \
	./include \
	./include/hadb \
	./include/popup \
	./include/pso \
	./include/simulator \


# 在头文件路径前面加入-I
INCLUDE	= $(patsubst %, -I %, $(INC_DIR))

# 得到带路径的 .c 文件
CFILES := $(foreach dir, $(SRC_DIR), $(wildcard $(dir)/*.c))

# 得到不带路径的 .c 文件
CFILENDIR := $(notdir  $(CFILES))

# 将工程中的.c 文件替换成 ./build 目录下对应的目标文件 .o
COBJS = $(patsubst %, ./$(BUILD_DIR)/%, $(patsubst %.c, %.o, $(CFILENDIR)))

# all，必须要在TARGET前面
all: $(TARGET_DIR)/$(TARGET) cleanobj

# make 自动在源文件目录下搜索 .c 文件
VPATH = $(SRC_DIR)

$(TARGET_DIR)/$(TARGET) : $(COBJS)
	$(CC) -o $@ $^ -lm

$(COBJS) : $(BUILD_DIR)/%.o : %.c
	@mkdir -p $(BUILD_DIR)
	$(CC) $(INCLUDE) -c -o $@ $< -lm

clean:
	rm -rf $(BUILD_DIR) $(TARGET_DIR)/$(TARGET)

cleanobj:
	rm -rf $(BUILD_DIR)