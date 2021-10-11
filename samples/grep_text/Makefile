#/* 
#* This expermental software is provided AS IS. 
#* Feel free to use/modify/distribute, 
#* If used, please retain this disclaimer and cite 
#* "GPUfs: Integrating a file system with GPUs", 
#* M Silberstein,B Ford,I Keidar,E Witchel
#* ASPLOS13, March 2013, Houston,USA
#*/

all: fs_gpu fs_gpu_nofs grep_text_cpu

CXXFLAGS=-fopenmp
grep_text_cpu.o: grep_text_cpu.cpp 

grep_text_cpu: grep_text_cpu.o
	$(CXX) -o grep_text_cpu grep_text_cpu.o -O2 -fopenmp 


LIBGPUFSDIR=../../libgpufs/

include $(LIBGPUFSDIR)/Makefile

fs_gpu: grep_text_gpu.o
	$(NVCC) --relocatable-device-code=true -o fs_gpu fs.cu -I$(LIBGPUFSDIR) -I../../gpufs_con_lib.user/ $(LIBGPUFSDIR)/release/libgpufs.a

fs_gpu_nofs: grep_text_gpu_nofs.o
	$(NVCC) --relocatable-device-code=true -o fs_gpu_nofs fs.cu -I$(LIBGPUFSDIR) -I../../gpufs_con_lib.user/ $(LIBGPUFSDIR)/release/libgpufs.a

grep_text_gpu.o: grep_text_gpu.cu
	$(NVCC) -dc grep_text_gpu.cu -I$(LIBGPUFSDIR)

grep_text_gpu_nofs.o: grep_text_gpu_nofs.cu
	$(NVCC) -dc grep_text_gpu_nofs.cu -I$(LIBGPUFSDIR)

clean: 
	rm *.o fs_gpu fs_gpu_nofs grep_text_cpu



