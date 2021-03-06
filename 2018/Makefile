ifeq (,$(OUT))
$(error you must define OUT)
endif

TMP = .tmp

HTML_NAMES = $(addsuffix .html, \
	contact index registration schedule/index speakers/index thankyou venue)

TALK_BASENAMES = \
alexandrescu \
bright \
odersky \
cesi \
cojocaru \
davis \
degenhardt \
dilly \
engelen \
funkwerk \
hackathon1 \
hackathon2 \
jercaianu \
kroeplin \
le \
leroy \
lightning \
marques \
nacke \
nitu \
olshansky \
panel \
rohe \
schveighoffer \
shemesh \
staniloiu \
watson \
weka \
zvibel \

$(addprefix $(OUT)/, includes/%): includes/%
	cp $^ $@

TO_COPY = \
	images/ $(wildcard images/*.png images/*.svg images/*.jpg) \
	includes/ $(wildcard includes/*) \

TALK_NAMES = $(addprefix talks/, $(addsuffix .html, ${TALK_BASENAMES}))

SPEAKER_BITS = $(addprefix $(TMP)/speakers/, $(addsuffix .gen.ddoc, ${TALK_BASENAMES}))

SCHEDULE_BITS = $(addprefix $(TMP)/schedule/, $(addsuffix .gen.ddoc, ${TALK_BASENAMES}))

ALL_RELATIVE_PATHS = $(HTML_NAMES) $(TALK_NAMES) $(TO_COPY)

SITE_FILES = $(addprefix $(OUT)/, $(ALL_RELATIVE_PATHS))

# Rules

all : $(SITE_FILES)

clean :
	rm -rf $(OUT) $(TMP)

# Patterns

$(OUT)/talks/%.html : macros.ddoc talks/macros.ddoc talks/%.dd
	$(DMD) -c -o- -Df$@ $^

$(TMP)/speakers/%.gen.ddoc : macros.ddoc speakers/fragment.ddoc talks/%.dd
	$(DMD) -c -o- -Df$@ $^

$(OUT)/speakers/index.html : macros.ddoc ${SPEAKER_BITS} speakers/index.dd
	$(DMD) -c -o- -Df$@ $^

$(OUT)/schedule/index.html : macros.ddoc ${SCHEDULE_BITS} \
		schedule/index.dd
	$(DMD) -c -o- -Df$@ $^

$(TMP)/schedule/%.gen.ddoc : macros.ddoc talks/macros.ddoc schedule/fragment.ddoc talks/%.dd
	$(DMD) -c -o- -Df$@ $^

$(OUT)/%.html : macros.ddoc %.dd
	$(DMD) -c -o- -Df$@ $^

$(OUT)/%.pdf : %.pdf
	cp $^ $@

$(OUT)/%.pptx : %.pptx
	cp $^ $@

$(OUT)/%.ppt : %.ppt
	cp $^ $@

$(OUT)/%.odp : %.odp
	cp $^ $@

$(OUT)/%.zip : %.zip
	cp $^ $@

$(OUT)/%.png : %.png
	cp $^ $@

$(OUT)/%.svg : %.svg
	cp $^ $@

$(OUT)/%.jpg : %.jpg
	cp $^ $@

$(OUT)/%.d : %.d
	cp $^ $@

$(OUT)/%.css : %.css
	cp $^ $@

$(OUT)/%/ : %/
	mkdir -p $@

