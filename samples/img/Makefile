all: fs img_cpu

CXXFLAGS=-fopenmp

LIBGPUFSDIR=../../libgpufs/

include $(LIBGPUFSDIR)/Makefile

fs: fs.o
	$(NVCC) --relocatable-device-code=true -o fs fs.o -I$(LIBGPUFSDIR) -I../../gpufs_con_lib.user/ $(LIBGPUFSDIR)/release/libgpufs.a

fs.o: fs.cu
	$(NVCC) -dc -I$(LIBGPUFSDIR) -I../../gpufs_con_lib.user/ -c $<

img_cpu: img_cpu.o
	$(CC) $(CXXFLAGS) -o $@ $<

img_cpu.o: img_cpu.cpp
	$(CC) $(CXXFLAGS) -c $<

clean:
	rm fs img_cpu  *.o
