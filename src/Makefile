PKG =  stack_data

$(PKG).gfn: $(PKG).inp $(PKG).spec $(PKG)_sample.inp $(PKG)_help.md international_gdp.gdt
	gretlcli --makepkg $(PKG).inp

$(PKG).zip: $(PKG).gfn
	echo makepkg $(PKG).zip | gretlcli -b -

# Only if the manual is a pdf file or you provide an external dataset
install: $(PKG).zip
	echo pkg install $(PKG).zip --local | gretlcli -b -e -
	cat $(PKG)_help.md | tee ../README.md

clean:
	rm -f $(PKG).zip $(PKG).gfn
