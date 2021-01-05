# The online Scheme REPL is composed of the following files:
#
# - Console.js        a simple console built on top of CodeMirror
# - Interpreter.scm   the interface between the Gambit interpreter and console
# - Interpreter.js    this file is generated from Interpreter.scm by gsc
# - index.html        the main HTML file
#
# To build Interpreter.js you need the latest Gambit, which should be
# compiled like this (from an existing bootstrapped recent installation):
#
#   cd gambit
#   git pull
#   make clean
#   ./configure --enable-single-host --enable-targets=js --prefix=/usr/local/Gambit
#   make
#   make modules
#   sudo make install
#
# You also need CodeMirror.  Get and unzip codemirror-5.59.1 from:
#
#   https://codemirror.net/doc/releases.html
#
# After that, in this directory do:
#
#   make
#
# Then in a browser open index.html .

all: Interpreter.js Interpreter.min.js lib-copy

Interpreter.js: Interpreter.scm
	gsc -target js -exe -o Interpreter.js Interpreter.scm

Interpreter.min.js: Interpreter.js
	npx google-closure-compiler --js Interpreter.js --js_output_file Interpreter.min.js
	gzip -k -9 Interpreter.min.js

lib-copy:
	rm -rf lib
	cp -r `gsc -e '(display (path-expand "~~lib"))'` lib

clean:
	rm -rf Interpreter.js lib