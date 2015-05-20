---
layout: post
title: Hackerschool, 2 weeks later
---

The first two weeks of hackerschool was way better than I expected.
Some of the highlights include learning how to use the [BeagleBoneBlack PRU][] with Dana, building a [wifi probe request sniffer]() using [libtins][], and finishing the first week of [stanford networking course CS144][].

Inspired by [Ambers post][] on trying things you are scared of, I'm going to retackle this NES sniffing project. The goal is to identify and display what cartridge is in a running NES. My plan is as follows:

  * Get the beaglebone PRU to trigger interrupts on the phase2 pin of the nes
  * Read the LSB of the data line in that interrupt
  * Write 512 bits to shared memory
  * Do this a few times
  * Find longest common substring and try to guess a 'header' to know when we should actually read

Small things that happened in the last week

  * d3.js graph to add nodes and links to visualize a mesh network
  * getting [cjdns][] up and running on OSX & a beaglebone with the help of [PSST!][], [GRRR!][], and [nyc meshnet][]

[beagleboneblack pru]: http://hipstercircuits.com/beaglebone-black-gpio-mux-for-pru-with-device-tree-overlay/
[wifi probe request sniffer]: https://github.com/jedahan/dreamcatcher
[libtins]: http://libtins.github.io
[ambers post]: http://subsymbol.org/journal/hacker-school-monday-august-4th-2014.html
[stanford networking course cs144]: http://web.stanford.edu/class/cs144/
[cjdns]: https://github.com/cjdelisle/cjdns
[psst!]: https://hotmesh.hackpad.com
[grrr!]: https://hotmesh.hackpad.com
[nyc meshnet]: http://nycmesh.net
