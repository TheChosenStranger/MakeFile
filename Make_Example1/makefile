include config.mk

allObjs = $(allSrcs:.c=.o)
allDeps = $(allSrcs:.c=.d)

$(FinalTargetName) : CFLAG = 
$(allObjs): CFLAG = -c
$(allDeps): CFLAG = -MM

$(FinalTargetName) : $(allObjs) 
	$(CC) $(CFLAG) $^ -o $@ 

$(allObjs) : %.o : %.c 
	$(CC) $(CFLAG) $< -o $@ 

$(allDeps) : %.d : %.c | Dependencies
	$(CC) $(CFLAG) $< -o $@
	@cp  $@ Dependencies\

Dependencies:
	@mkdir $@

.PHONY: clean link onlyCompile depend all

clean: 
	rm -r $(FinalTargetName) $(allObjs) $(allDeps) Dependencies\

link: 
	$(CC) $(CFLAG) $(allObjs) -o $(FinalTargetName)

onlyCompile: $(allObjs)

depend: $(allDeps)

all: $(allDeps) 
	$(MAKE) $(FinalTargetName)

