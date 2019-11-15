## Process this file with automake to produce Makefile.in

dindatadir = $(datarootdir)/@PACKAGE@
dinicondir = $(datarootdir)/pixmaps
dindeskdir = $(datarootdir)/applications

dindata_DATA = \
drone.crv\
drone.ed\
waveform1.crv\
waveform1.ed\
waveform2.crv\
waveform2.ed\
waveforms.lib\
coml.crv\
comr.crv\
compressor.ed\
gater.crv\
gater-patterns.lib\
gater.ed\
fm.crv\
am.crv\
modulation.ed\
volume-l.crv\
volume-r.crv\
feedback-l.crv\
feedback-r.crv\
delay.ed\
octave-shift.crv\
octave-shift.ed\
octave-shift-patterns.lib\
dot.crv\
dash.crv\
inner.crv\
letter.crv\
word.crv\
i8n_morse_code\
morse-code.ed\
attack.crv\
decay.crv\
attack.ed\
decay.ed\
attack.lib\
decay.lib\
din_info\
globals\
ji.tuning\
pytha.tuning\
et.tuning\
shrutis.tuning\
scalelist\
sine_levels\
fft_levels\
m00\
oscilloscope\
jack_prefs\
init.tcl\
help.tcl\
save_settings.tcl\
settings.tcl\
scoper.help.tcl\
midimap.help.tcl\
droner.help.tcl\
morse-code.help.tcl\
curve-library.help.tcl\
curve-name.help.tcl\
curve-value.help.tcl\
get-selection.help.tcl\
load-patch.help.tcl\
list-patches.help.tcl\
set-curve-editor.help.tcl\
set-text-color.help.tcl\
echo.help.tcl\
add-scale.help.tcl\
remove-scale.help.tcl\
find-scale.help.tcl\
get-var.help.tcl\
set-var.help.tcl\
load-scale.help.tcl\
list-scales.help.tcl\
list-notes.help.tcl\
set-delay.help.tcl\
get-delay.help.tcl\
set-bpm.help.tcl\
reset-bpm.help.tcl\
get-bpm.help.tcl\
set-style.help.tcl\
get-style.help.tcl\
list-bpms.help.tcl\
set-beat.help.tcl\
get-beat.help.tcl\
set-scope.help.tcl\
get-scope.help.tcl\
get-drone.help.tcl\
set-font-size.help.tcl\
get-font-size.help.tcl\
set-kern.help.tcl\
note-distance.help.tcl\
get-kern.help.tcl\
notation.help.tcl\
key.help.tcl\
chord.help.tcl\
tuning.help.tcl\
bot.help.tcl\
set-drone.help.tcl\
num-octaves.help.tcl\
make-interval-note-vars.tcl\
window\
midimap.patch.tcl\
scoper.patch.tcl\
droner.patch.tcl\
start-end.patch.tcl\
start-end.help.tcl\
changer.patch.tcl\
changer.help.tcl\
2600.patch.tcl\
2600.help.tcl\
din.hlp\
curve_editor.hlp\
keyboard-keyboard.hlp\
jag.fnt\
font.ed\
velocity.crv\
velocity.ed\
velocity.lib\
dam.crv\
dfm.crv\
donate.tcl\
drone-modulation.ed\
d_min_max\
d_parameters\
d_parameter_limits\
checkdotdin.in\
tips.tcl


dindesk_DATA = din.desktop
dinicon_DATA = din.png

dinbindir = ${prefix}/bin
dinbin_DATA = checkdotdin

$(dinbin_DATA): $(dinbin_DATA).in
	sed "s|\@datarootdir\@|$(datarootdir)|" $< > $@

EXTRA_DIST = $(dindata_DATA) $(dindesk_DATA) $(dinicon_DATA) $(dinbin_DATA)

install-data-hook: ${DESTDIR}/$(prefix)/bin/checkdotdin
	chmod +x $^
