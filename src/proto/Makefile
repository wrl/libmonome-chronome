CFLAGS := -I. -I../private -I../../public $(CFLAGS)
LDFLAGS += -L.. -lmonome

.PHONY: $(PROTOCOLS)

all: $(PROTOCOLS)

clean:
	rm -f *.o *.so *.dylib *.dll

install:
	$(INSTALL) -d $(LIBDIR)/monome

	for PROTOCOL in $(PROTOCOLS); do \
		echo "  INSTALL src/proto/protocol_$$PROTOCOL.$(LIBSUFFIX) -> $(LIBDIR)/monome/protocol_$$PROTOCOL.$(LIBSUFFIX)"; \
		$(INSTALL) protocol_$$PROTOCOL.$(LIBSUFFIX) $(LIBDIR)/monome/protocol_$$PROTOCOL.$(LIBSUFFIX); \
	done

# small hack so that PROTOCOLS can be set to something like "series 40h osc"
# or just "series 40h" up at the project root
series: protocol_series.$(LIBSUFFIX)
	true
40h: protocol_40h.$(LIBSUFFIX)
	true
osc: protocol_osc.$(LIBSUFFIX)
	true
mext: protocol_mext.$(LIBSUFFIX)
	true
chronome: protocol_chronome.$(LIBSUFFIX)
	true

protocol_mext.so: mext.o
	echo "  LD      src/proto/$@"
	$(LD) -shared -Wl,-soname,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_mext.dylib: mext.o
	echo "  LD      src/proto/$@"
	$(LD) -dynamiclib -Wl,-install_name,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_mext.dll: mext.o
	echo "  LD      src/proto/$@"
	$(LD) $(LDFLAGS) $(SO_LDFLAGS) -shared -o $@ $<

protocol_chronome.so: chronome.o
	echo "  LD      src/proto/$@"
	$(LD) -shared -Wl,-soname,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_chronome.dylib: chronome.o
	echo "  LD      src/proto/$@"
	$(LD) -dynamiclib -Wl,-install_name,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_chronome.dll: chronome.o
	echo "  LD      src/proto/$@"
	$(LD) $(LDFLAGS) $(SO_LDFLAGS) -shared -o $@ $<

protocol_series.so: series.o
	echo "  LD      src/proto/$@"
	$(LD) -shared -Wl,-soname,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_series.dylib: series.o
	echo "  LD      src/proto/$@"
	$(LD) -dynamiclib -Wl,-install_name,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_series.dll: series.o
	echo "  LD      src/proto/$@"
	$(LD) $(LDFLAGS) $(SO_LDFLAGS) -shared -o $@ $<

protocol_40h.so: 40h.o
	echo "  LD      src/proto/$@"
	$(LD) -shared -Wl,-soname,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_40h.dylib: 40h.o
	echo "  LD      src/proto/$@"
	$(LD) -dynamiclib -Wl,-install_name,$@ $(LDFLAGS) $(SO_LDFLAGS) -o $@ $<

protocol_40h.dll: 40h.o
	echo "  LD      src/proto/$@"
	$(LD) $(LDFLAGS) $(SO_LDFLAGS) -shared -o $@ $<

protocol_osc.so: osc.o
	echo "  LD      src/proto/$@"
	$(LD) -shared -Wl,-soname,$@ $(LDFLAGS) $(SO_LDFLAGS) $(LO_LDFLAGS) -o $@ $<

protocol_osc.dylib: osc.o
	echo "  LD      src/proto/$@"
	$(LD) -dynamiclib -Wl,-install_name,$@ $(LDFLAGS) $(SO_LDFLAGS) $(LO_LDFLAGS) -o $@ $<

.c.o:
	echo "  CC      src/proto/$@"
	$(CC) $(LO_CFLAGS) $(CFLAGS) -c $< -o $@
