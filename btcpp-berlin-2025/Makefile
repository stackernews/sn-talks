.PHONY: build

build:
	pandoc -t beamer -s -o slides.tex slides.md
	patch slides.tex slides.patch
	mkdir -p build
	pdflatex --output-directory=build slides.tex
	mv build/slides.pdf slides.pdf
