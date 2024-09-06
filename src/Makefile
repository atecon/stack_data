PKG =  stack_data

$(PKG).gfn: $(PKG).inp $(PKG).spec $(PKG)_sample.inp $(PKG)_help.md
	gretlcli --makepkg $(PKG).inp

$(PKG).zip: $(PKG).gfn international_gdp.gdt
	echo makepkg $(PKG).zip | gretlcli -b -

install: $(PKG).gfn
	echo pkg install $(PKG).gfn --local | gretlcli -b -e -
	cat $(PKG)_help.md | tee ../README.md

clean:
	rm -f $(PKG).gfn
