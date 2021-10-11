#/* 
#* This expermental software is provided AS IS. 
#* Feel free to use/modify/distribute, 
#* If used, please retain this disclaimer and cite 
#* "GPUfs: Integrating a file system with GPUs", 
#* M Silberstein,B Ford,I Keidar,E Witchel
#* ASPLOS13, March 2013, Houston,USA
#*/

all: cp

LIBGPUFSDIR=../../libgpufs/

include $(LIBGPUFSDIR)/Makefile

cp: cp_cuda.o
	$(NVCC) --relocatable-device-code=true -o cp cp_cuda.o -I$(LIBGPUFSDIR) -I../../gpufs_con_lib.user/ $(LIBGPUFSDIR)/release/libgpufs.a

cp_cuda.o: cp.cu
	$(NVCC) -dc -I$(LIBGPUFSDIR) -I../../gpufs_con_lib.user/ cp.cu -o cp_cuda.o

PHONY:  clean

clean:
	rm -f cp *.o *.a
