YUI_COMPRESS_JAR = ./lib/yuicompressor-2.4.2.jar

JS_FILES = src/LICENSE src/header.js \
	src/network.js src/plus.js src/attribution.js \
	src/core.js
#   src/namespaces.js \
#	src/campaign.js \

LD_FILES = src/ubiquity-rdfa/lib/RDFGraph.js \
	src/blank_line.js \
	src/ubiquity-rdfa/lib/RDFStore.js \
	src/blank_line.js \
	src/ubiquity-rdfa/lib/RDFQuery.js \
	src/blank_line.js \
	src/ld/main.js

DEED_FILES = $(LD_FILES) \
	src/deed/main.js \
	src/deed/attribution.js \
	src/deed/queries.js

all: deed-dbg.js deed.js pddeed-dbg.js pddeed.js ld-min.js deed-sparql.js deed-sparql-min.js

ld-min.js: ld.js
	java -jar $(YUI_COMPRESS_JAR) ld.js > ld-min.js

ld.js: $(LD_FILES)
	cat $(LD_FILES) > ld.js.tmp
	cat ld.js.tmp | grep -v debugger > ld.js
	rm ld.js.tmp

deed-sparql-min.js: deed-sparql.js
	java -jar $(YUI_COMPRESS_JAR) deed-sparql.js > deed-sparql-min.js

deed-sparql.js: $(DEED_FILES)
	cat $(DEED_FILES) > deed-sparql.js.tmp
	cat deed-sparql.js.tmp | grep -v debugger > deed-sparql.js
	rm deed-sparql.js.tmp

deed-dbg.js: $(JS_FILES)
	cat $(JS_FILES) > deed-dbg.js

pddeed-dbg.js: src/pd.js
	cat src/LICENSE src/header.js src/network.js src/pd.js > pddeed-dbg.js

deed.js: deed-dbg.js
	java -jar $(YUI_COMPRESS_JAR) deed-dbg.js > deed.js

pddeed.js: deed-dbg.js
	java -jar $(YUI_COMPRESS_JAR) pddeed-dbg.js > pddeed.js

verbose: deed-dbg.js
	java -jar $(YUI_COMPRESS_JAR) -v deed-dbg.js > deed.js

clean:
	rm deed.js deed-dbg.js pddeed-dbg.js deed.js ld.js ld-min.js deed-sparql.js deed-sparql-min.js
