AM_CXXFLAGS = $(liblo_CFLAGS) $(jack_CFLAGS) $(fftw3f_CFLAGS) -I /usr/include -I /usr/local/include -I /opt/include -I/usr/include/tcl8.5 -I/usr/local/include/tcl8.5 -I /opt/include/tcl8.5 -I ../include  -Wall -O3
LIBS += $(liblo_LIBS) $(jack_LIBS) $(fftw3f_LIBS) -L/usr/lib/tcl8.5 -L/usr/local/lib/tcl8.5 -L /opt/lib/tcl8.5 -L /usr/lib -L /opt/lib -L /usr/local/lib -ltcl8.5 -lGL -lircclient -lrt -lX11

bin_PROGRAMS = din

din_SOURCES = \
main.cc\
din.cc\
audio.cc\
range.cc\
note.cc\
play.cc\
curve.cc\
multi_curve.cc\
solver.cc\
curve_library.cc\
basic_editor.cc\
curve_editor.cc\
listeners.cc\
console.cc\
console_iterator.cc\
help.cc\
line.cc\
font.cc\
glyph.cc\
oscilloscope.cc\
delay.cc\
viewwin.cc\
mocap.cc\
beat2value.cc\
scale_info.cc\
command.cc\
scalelist.cc\
textboard.cc\
sine_mixer.cc\
levels.cc\
chrono.cc\
font_editor.cc\
phrasor.cc\
compressor.cc\
osc.cc\
globals.cc\
bot.cc\
tokenizer.cc\
morse_code.cc\
tcl_interp.cc\
ui.cc\
keyboard_keyboard.cc\
fft.cc\
widget.cc\
button.cc\
checkbutton.cc\
field.cc\
drone.cc\
fader.cc\
ticker_tape.cc\
label.cc\
filled_button.cc\
authors_note.cc
