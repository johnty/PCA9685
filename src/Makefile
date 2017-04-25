INCLUDES := -I../../I2C/src
LIBRARIES := -L../../I2C/src 
LIBS := -lI2C
CXXFLAGS := -O3 -fPIC -g -Wall -Werror $(INCLUDES) $(LIBRARIES) $(LIBS)
CXX := g++
#CXX := arm-unknown-linux-gnueabi-g++
MAJOR := 0
MINOR := 1
NAME := PCA9685
VERSION := $(MAJOR).$(MINOR)
RM := rm -rf

TEST_LDFLAGS = -Wl,-R -Wl,../../I2C/src #mucking around with rpath settings for relative dylib paths...
TEST_LDFLAGS2 = -Wl,-R -Wl,./

all: lib test copy 
lib: lib$(NAME).so.$(VERSION) lib$(NAME).so

lib$(NAME).so: lib$(NAME).so.$(VERSION)
	ldconfig -v -n .
	ln -s lib$(NAME).so.$(MAJOR) lib$(NAME).so

lib$(NAME).so.$(VERSION): $(NAME).o
	$(CXX) -pg -shared -Wl,-soname,lib$(NAME).so.$(MAJOR) $^ -o $@

test: test_servo0.cpp
	$(CXX) -Wall $(INCLUDES) $(LIBRARIES) $(LIBS) -L./ -l$(NAME) $(TEST_LDFLAGS) $(TEST_LDFLAGS2) test_servo0.cpp -o test_servo0
 
	
clean:
	$(RM) *.o *.so*
	
copy:
ifdef DISTPATH
	cp lib$(NAME)* $(DISTPATH)
endif
