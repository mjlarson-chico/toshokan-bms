CXX = g++
CPPFLAGS = -std=c++17 -g
INCLUDEPATH = -I../
DEPDIR = deps
OBJDIR = objs
DEPFLAGS = -MT $@ -MMD -MF $(DEPDIR)/$*.Td 
#postcompiling technique grabbed from here: http://make.mad-scientist.net/papers/advanced-auto-dependency-generation/
POSTCOMPILE = mv -f $(DEPDIR)/$*.Td $(DEPDIR)/$*.d && touch $@
CPPWARNINGS = -Wall -pedantic

CPPSOURCEFILES = $(wildcard *.cpp)

# create a list of object files by substituting the .cpp in above list with .o
OBJFILES = $(CPPSOURCEFILES:%.cpp=$(OBJDIR)/%.o)

# create dependencies files. (generated with g++ -MT sourcefile -MMD -MF outputfile)
DEPFILES = $(CPPSOURCEFILES:%.cpp=$(DEPDIR)/%.d)

toshokan: $(OBJFILES)
	$(CXX) -g -o toshokan $(OBJFILES)

# pattern rule to compile .cpp files
$(OBJDIR)/%.o : %.cpp $(DEPDIR)/%.d | $(DEPDIR) $(OBJDIR)
	$(CXX) $(DEPFLAGS) $(CPPFLAGS) $(CPPWARNINGS) $(INCLUDEPATH) -o $@ -c $<
	$(POSTCOMPILE)

$(DEPDIR): ; @mkdir -p $@

$(OBJDIR): ; @mkdir -p $@

# include dependency files (.d file) generated by g++
$(DEPFILES):
include $(wildcard $(DEPFILES))

clean:
	rm -f $(OBJFILES) toshokan
	rm -rf $(DEPDIR) $(OBJDIR)
