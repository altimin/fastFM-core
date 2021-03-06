P= example_als_mcmc example_sgd example_sgd_bpr
VPATH = ../
OBJECTS= example_als_mcmc.o example_sgd example_sgd_bpr
CFLAGS = `pkg-config --cflags glib-2.0` -std=c99 -g -Wall -O0 -I../include -L../bin -I../externals/CXSparse/Include
LDLIBS= -lfastfm `pkg-config --libs glib-2.0`  -L../externals/CXSparse/Lib -lcxsparse -lcblas -latlas -lm
CC=gcc

all: $(P)
	$(MAKE) -C ../ lib

#test_ffm_sgd.o: fast_fm.h

run:
	./example_sgd
	./example_sgd_bpr
	./example_als_mcmc

regression:
	./../bin/fastfm data/train_regression data/test_regression \
		--task regression   \
		--rng-seed 1234     \
		--init-var=0.11     \
		--n-iter=123        \
		--solver='mcmc'     \
		--rank 7            \
		--l2-reg=.22

classification:
	./../bin/fastfm data/train_classification data/test_classification \
		--task classification\
		--solver='als'     \
		--l2-reg-w=.11     \
		--l2-reg-V=.22


ranking:
	./../bin/fastfm data/train_ranking data/test_ranking \
		--task ranking     \
		--train-pairs  data/train_pairs \
		--solver='sgd'     \
		--init-var=0.01     \
		--n-iter=2000      \
		--rank 2           \
		--l2-reg=0.5       \
		--step-size=0.002 \
		--test-predict data/ranking_predictions


.PHONY : clean
clean : 
	rm -f $(P) $(OBJECTS)
	rm -f *.o
