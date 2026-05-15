FILES = $(wildcard *.md)
DOCXFILES = $(patsubst %.md,%.docx,$(FILES))
PDFFILES = $(patsubst %.md,%.pdf,$(FILES))

all: $(DOCXFILES) $(PDFFILES)

%.docx: %.md
	pandoc "$<" --filter pandoc-crossref --number-sections -o "$@"

%.pdf: %.md
	pandoc "$<" -s --filter pandoc-crossref --pdf-engine=lualatex -o "$*.tex"
	sed -i '/\\begin{CSLReferences}/,/\\end{CSLReferences}/d' "$*.tex"
	lualatex "$*.tex"
	rm -f "$*.tex" "$*.log" "$*.aux" "$*.out"

clean:
	rm -f *.docx *.pdf *.tex *.log *.aux *.out
