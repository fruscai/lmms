<div align="center">
	<h1>
	<img src="https://raw.githubusercontent.com/LMMS/artwork/master/Icon%20%26%20Mimetypes/lmms-64x64.svg" alt="LMMS Logo"><br>LMMS
	</h1>
	<p>Cross-platform music production software</p>
	<p>
		<a href="https://lmms.io/">Website</a>
		⦁︎
		<a href="https://github.com/LMMS/lmms/releases">Releases</a>
		⦁︎
		<a href="https://github.com/LMMS/lmms/wiki">Developer wiki</a>
		⦁︎
		<a href="https://lmms.io/documentation">User manual</a>
		⦁︎
		<a href="https://lmms.io/showcase/">Showcase</a>
		⦁︎
		<a href="https://lmms.io/lsp/">Sharing platform</a>
	</p>
	<p>
		<a href="https://github.com/LMMS/lmms/actions/workflows/build.yml"><img src="https://github.com/LMMS/lmms/actions/workflows/build.yml/badge.svg" alt="Build status"></a>
		<a href="https://lmms.io/download"><img src="https://img.shields.io/github/release/LMMS/lmms.svg?maxAge=3600" 	alt="Latest stable release"></a>
		<a href="https://github.com/LMMS/lmms/releases"><img src="https://img.shields.io/github/downloads/LMMS/lmms/total.svg?maxAge=3600" alt="Overall downloads on Github"></a>
		<a href="https://discord.gg/3sc5su7"><img src="https://img.shields.io/badge/chat-on%20discord-7289DA.svg" alt="Join the chat at Discord"></a>
		<a href="https://www.transifex.com/lmms/lmms/"><img src="https://img.shields.io/badge/localise-on_transifex-green.svg"></a>
	</p>
</div>

> ### This fork: Save with embedded samples
>
> Writes every sample a project uses into the project file itself, so it opens and plays on a
> machine that does not have the audio files. A checkbox in the Save As dialog next to the existing
> project bundle option, and a command:
>
> ```
> lmms embedsamples <in> <out>
> ```
>
> **Two branches, both buildable.**
>
> | Branch | Covers | Attributes written |
> |---|---|---|
> | `audioembed-v1` | AudioFileProcessor instruments and Sample tracks | `sampledata`, `data`, `sample_rate`, all of which stock LMMS already reads |
> | `audioembed-v2` | the above plus SlicerT, TripleOscillator user waves, and the envelope and LFO user waves | adds `userwavedata`, which stock LMMS ignores |
>
> ```
> git clone https://github.com/fruscai/lmms.git
> cd lmms
> git checkout audioembed-v1     # or audioembed-v2
> ```
>
> v2 output still opens and plays in stock LMMS 1.3. Measured against stock at the same upstream
> commit with every source file deleted: 4066144 frames at peak 32767, matching. The custom
> oscillator and LFO wave shapes are the only part stock skips.
>
> **Sample rate.** Embedded audio carries no rate of its own and the loader assumes the engine rate.
> A 48 kHz sample stored raw plays flat by 48000/44100, measured at 202 Hz against a correct 220 Hz,
> so the audio is converted first. The target is the engine rate of the machine doing the saving,
> and nothing in the file corrects it afterwards, so a project embedded on a 48 kHz engine plays
> fast on a 44.1 kHz one. The command line uses the configured rate, minimum 44100.
>
> **LMMS 1.2 cannot open anything either branch saves.** LMMS 1.3 writes `midiclip`, `mixer` and
> `mixerchannel` on every save and 1.2 has no such elements. That is unrelated to embedding. For 1.2,
> and for anything going to somebody else, use
> [LMMS-Tools-Relinker-Embedder](https://github.com/fruscai/LMMS-Tools-Relinker-Embedder), which does
> the same job from outside LMMS and fixes its target rate at 44100.
>
> Notes, decision records and the patches on their own are in
> [lmms-embed-samples](https://github.com/fruscai/lmms-embed-samples).


What is LMMS?
--------------

LMMS is an open-source cross-platform digital audio workstation designed for music production. It includes an advanced Piano Roll, Beat Sequencer, Song Editor, and Mixer for composing, arranging, and mixing music. It comes with 15+ synthesizer plugins by default, along with VST2 and SoundFont2 support.

Features
---------

* Song-Editor for arranging melodies, samples, patterns, and automation
* Pattern-Editor for creating beats and patterns
* An easy-to-use Piano-Roll for editing patterns and melodies
* A Mixer with unlimited mixer channels and arbitrary number of effects
* Many powerful instrument and effect-plugins out of the box
* Full user-defined track-based automation and computer-controlled automation sources
* Compatible with many standards such as SoundFont2, VST2 (instruments and effects), LADSPA, LV2, GUS Patches, and full MIDI support
* MIDI file importing and exporting

Building
---------

See [Compiling LMMS](https://github.com/LMMS/lmms/wiki/Compiling)

Join LMMS-development
----------------------

If you are interested in LMMS, its programming, artwork, testing, writing demo songs, (and improving this README...) or something like that, you're welcome to participate in the development of LMMS!

Information about what you can do and how can be found in the [wiki](https://github.com/LMMS/lmms/wiki).

Before coding a new big feature, please _always_ [file an issue](https://github.com/LMMS/lmms/issues/new) for your idea and suggestions about your feature and about the intended implementation on GitHub, or ask in one of the tech channels on Discord and wait for replies! Maybe there are different ideas, improvements, or hints, or maybe your feature is not welcome/needed at the moment.
