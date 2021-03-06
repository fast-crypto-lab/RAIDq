CC=    gcc
CXX=   g++
LD=    g++

CFLAGS=  -O3 -mavx2 -std=gnu99 -Wall -Wextra
CXXFLAGS= -O3 -mavx2 -Wall -Wextra 
INCPATH= -I/usr/local/include -I/opt/local/include -I/usr/include -I../
LDFLAGS= 
LIBPATH= -L/usr/local/lib -L/opt/local/lib -L/usr/lib
LIBS=    -lm


#EXE= raid6_ssse3-test raid7_plank-test
EXE += raid_rs-test raidq-test code-benchmark-test basicop-benchmark-test code-benchmark2-test err-decoder-test err-decoder-benchmark-test
CODE_OBJ= $(wildcard ../*.o)
OBJ=
CSRC= $(wildcard *.cpp)

ifdef DEBUG
        CFLAGS+=  -D_DEBUG_
        CXXFLAGS+= -D_DEBUG_
endif

ifdef NO_SSE
	CFLAGS += -D_NO_SSE_
	CXXFLAGS += -D_NO_SSE_
endif

ifdef NUM_XMM
	CFLAGS += -D_NUM_XMM_=$(NUM_XMM)
	CXXFLAGS += -D_NUM_XMM_=$(NUM_XMM)
endif

ifdef K
	CFLAGS += -DK=$(K)
	CXXFLAGS += -DK=$(K)
endif

ifdef P
	CFLAGS += -DP=$(P)
	CXXFLAGS += -DP=$(P)
endif

ifdef AVX2
	CFLAGS += -mavx2 -D_USE_AVX2_
	CXXFLAGS += -mavx2 -D_USE_AVX2_
endif

ifdef AVX
	CFLAGS += -mavx -D_USE_AVX_
	CXXFLAGS += -mavx -D_USE_AVX_
endif

ifdef GPROF
	CFLAGS += -pg
	CXXFLAGS += -pg
	LDFLAGS += -pg
endif

all: $(EXE)

%-test: $(OBJ) %-test.o
	$(LD) $(LDFLAGS) $(LIBPATH) -o $@ $^ $(CODE_OBJ) $(LIBS)

%.o: %.c
	$(CC) $(CFLAGS) $(INCPATH) -c $<

%.o: %.cpp
	$(CXX) $(CXXFLAGS) $(INCPATH) -c $<

tests:
	cd tests; make

tables:
	cd supplement; make

clean:
	rm -f *.o *-test
