# Makefile for CMU-Cambridge Statistical Language Modeling toolkit.

# make            Compile executables, but leave them in current directory
# make clean      Remove all object files (*.o) 
# make spotless   Remove all object files (*.o), excutables and backup files 
# make install    Compile executables, and install them in BINDIR. Also 
#                 install SLM2.a in LIBDIR


.c.o:
	$(CC) $(CFLAGS)  -c -o $*.o $*.c


CC              = gcc

# OPT_FLAG	Make the compiler run in optimised mode if set to -O
# GDB_FLAG	If compiling under gcc then setting this flag to -ggdb will
#		allow the gdb debugger to be used
# BNDS_CHK_FLAG	Switch on bounds checking as a debugging tool
# WARNINGS_FLAG Show all warnings when compiling
# ANSI_FLAG	When compiling with cc, some implementations require this flag
#               in order to run in ANSI mode
# POSIX_FLAG    Needed when compiling under cc on HPUX machines (in CUED at 
#               least)
# BYTESWAP_FLAG Tells the compiler which byte order to use. Uncomment the 
#               line if compiling for Linux, Ultrix or any other 
#               "Little-Endian" OS. Leave commented out for SunOS, 
#               Solaris, IRIX and HPUX.
# FIX_PROT_FLAG Needed for the gcc compiler on some SunOS machines in CUED. 

OPT_FLAG	= -O
#GDB_FLAG	= -ggdb
#BNDS_CHK_FLAG	= -fbounds-checking
#WARNINGS_FLAG	= -Wall
#ANSI_FLAG	= -Aa
#POSIX_FLAG	= -D_INCLUDE_POSIX_SOURCE
BYTESWAP_FLAG	= -DSLM_SWAP_BYTES
#FIX_PROT_FLAG 	= -D__USE_FIXED_PROTOTYPES__ 

CFLAGS		= $(OPT_FLAG) $(GDB_FLAG) $(BNDS_CHK_FLAG) $(WARNINGS_FLAG) $(ANSI_FLAG) $(POSIX_FLAG) $(BYTESWAP_FLAG) $(FIX_PROT_FLAG)

LINKFLAGS       = 
# Needed for successful linking on IRIX machines in CUED
# LINKFLAGS     = -Wl -old_ld

BINDIR          = ../bin
LIBDIR          = ../lib

LIB             = SLM2.a

EXECS           = idngram2lm evallm text2wngram text2idngram binlm2arpa \
                  ngram2mgram idngram2stats wfreq2vocab text2wfreq \
                  wngram2idngram mergeidngram interpolate

PC_OBJS         = pc_libs/pc_comline.o  pc_libs/pc_message.o

RR_OBJS         = rr_libs/parse_line.o rr_libs/quit.o \
                  rr_libs/rd_wlist_arry.o rr_libs/read_voc.o \
                  rr_libs/read_wlist_si.o rr_libs/rr_calloc.o \
                  rr_libs/rr_feof.o rr_libs/rr_fexists.o \
                  rr_libs/rr_filesize.o rr_libs/rr_fopen.o rr_libs/rr_fread.o \
                  rr_libs/rr_fseek.o rr_libs/rr_fwrite.o rr_libs/rr_iopen.o \
                  rr_libs/rr_malloc.o rr_libs/rr_oopen.o rr_libs/salloc.o \
                  rr_libs/rr_malloc.o rr_libs/rr_oopen.o rr_libs/salloc.o \
                  rr_libs/sih.o

IDNGRAM2LM_OBJS = bo_ng_prob.o calc_mem_req.o compute_back_off.o \
                  compute_discount.o compute_unigram.o get_ngram.o \
                  increment_context.o lookup_index_of.o \
                  short_indices.o two_byte_alphas.o write_lms.o \
                  num_of_types.o guess_mem.o counts.o

EVALLM_OBJS     = arpa_bo_ng_prob.o bo_ng_prob.o calc_prob_of.o \
                  decode_bo_case.o gen_fb_list.o load_lm.o \
                  lookup_index_of.o parse_comline.o perplexity.o \
                  short_indices.o stats.o two_byte_alphas.o validate.o \
                  num_of_types.o counts.o

BINLM2ARPA_OBJS = load_lm.o write_lms.o short_indices.o \
                  two_byte_alphas.o num_of_types.o stats.o counts.o

OBJS            = $(IDNGRAM2LM_OBJS) $(EVALLM_OBJS) $(BINLM2ARPA_OBJS) \
                  get_ngram.o $(PC_OBJS) $(RR_OBJS)

default: $(EXECS)

$(EXECS): $(LIB)

$(LIB): $(OBJS)
	rm -f $(LIB)
	ar r $(LIB) $(OBJS)
	if [ `uname` = SunOS -o `uname` = Linux ] ; then ranlib $(LIB) ; fi

install: $(EXECS)
	for i in $(EXECS); do \
		./install-sh $$i $(BINDIR); \
	done
	./install-sh $(LIB) $(LIBDIR)

clean:
	rm -f $(OBJS)

spotless: clean
	rm -f $(EXECS) $(LIB) *~

evallm: 
	$(CC) $(CFLAGS) -o evallm evallm.c $(LIB) $(LINKFLAGS) -lm

text2wngram: 
	$(CC) $(CFLAGS) -o text2wngram text2wngram.c $(LIB) $(LINKFLAGS) -lm

text2idngram:
	$(CC) $(CFLAGS) -o text2idngram text2idngram.c $(LIB) $(LINKFLAGS) -lm

binlm2arpa:
	$(CC) $(CFLAGS) -o binlm2arpa binlm2arpa.c $(LIB) $(LINKFLAGS) -lm

ngram2mgram: 
	$(CC) $(CFLAGS) -o ngram2mgram ngram2mgram.c $(LIB) $(LINKFLAGS) -lm

idngram2stats:
	$(CC) $(CFLAGS) -o idngram2stats idngram2stats.c $(LIB) $(LINKFLAGS) -lm

wfreq2vocab:
	$(CC) $(CFLAGS) -o wfreq2vocab wfreq2vocab.c $(LIB) $(LINKFLAGS) -lm

text2wfreq:
	$(CC) $(CFLAGS) -o text2wfreq text2wfreq.c $(LIB) $(LINKFLAGS) -lm

wngram2idngram:
	$(CC) $(CFLAGS) -o wngram2idngram wngram2idngram.c $(LIB) $(LINKFLAGS) -lm

mergeidngram:
	$(CC) $(CFLAGS) -o mergeidngram mergeidngram.c $(LIB) $(LINKFLAGS) -lm

idngram2lm: 
	$(CC) $(CFLAGS) -o idngram2lm idngram2lm.c $(LIB) $(LINKFLAGS) -lm

interpolate:
	$(CC) $(CFLAGS) -o interpolate interpolate.c $(LIB) $(LINKFLAGS) -lm
