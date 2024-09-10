PKG =  stack_data

$(PKG).gfn: $(PKG).inp $(PKG).spec $(PKG)_sample.inp $(PKG)_help.md
	gretlcli -e --makepkg $(PKG).inp

$(PKG).zip: $(PKG).gfn international_gdp.gdt
	echo makepkg $(PKG).zip | gretlcli -b -e -

# Only if the manual is a pdf file or you provide an external dataset
install: $(PKG).zip
	echo pkg install $(PKG).zip --local | gretlcli -b -e -
	cat $(PKG)_help.md | tee ../README.md

clean:
	rm -f $(PKG).zip $(PKG).gfn
