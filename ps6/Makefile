#Phonies, making sure that Make does not mistake any file with below
#command names for something else than what the commands intend
.PHONY: all
.PHONY: run
.PHONY: clean
.PHONY: install

target:=raycast

all: cpu gpu gpu_shared gpu_texture gpu_combined

get_result:
	scp gpu:~/tdt4200/ps6/$(target)_out.bmp ./

get_lab_result:
	scp gpu-lab:~/tdt4200/ps6/raycast_$(target)_out.bmp ./

memcheck: $(target)
	cuda-memcheck optirun ./run_$(target) --no-xorg --no-failsafe

run: $(target)
	./run_$(target)

raycast: bmp.c clutil.c raycast.c
	gcc -std=c99 bmp.c clutil.c raycast.c -o run_raycast \
	-lOpenCL -lm -Wextra -Wall -pedantic -g -O3

clean:
	rm -f run_* *.o
