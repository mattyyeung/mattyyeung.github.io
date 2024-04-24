---
layout: page
---


<!-- title: "My Front Path Piano" -->


I turned my front path into a light-up keyboard:
![]

It looks pretty cool at night:
![]

Piano mode:
![]

BIG Piano:
![]

Song mode:
![]

Daft Punk mode: (at night!!)
![]

Open door ("welcome mode?")
![]

## FAQs
- Why??? 
- *How?* Lots of trial and error. see below - key ingredients: trial, error, recycled stuff from the bin at work, waterproofing supplies, open source SW, cheap electronics, 3D prints,
- *How long?* Around 6 months worth of "hobby time". Perhaps a quarter of it experimenting with different technologies, one quarter iterating the chosen design, one quarter building/waterproofing steps and one quarter integration and fixing issues. The biggest surprise to me was "outdoor-proofing" - making 23x2 pieces of electronics robust to complete submersion, UV and 50C temperature swings - took a LONG time. 
- How did you learn to do all this? I'm an engineer. Which is to say, I googled a bunch of stuff and asked for a bunch of advice - *How much?* Original goal: $250, relying mostly on recycled components. Blew RIGHT through that... probably $1000. But would have been a lot more (3-5x?)if I bought everything new
- *Do you leave it on all the time?* It's often on 'silent mode' between 8.30am and 8.30pm, unless it's down for "maintenance"
- *Does it use much power?* under 10W in idle or around 1/20th of my fridge. 
- *Can it play my fav song XYZ?* Surprisingly few songs sound ok cut up into 23 little chunks, but sure! 
- *Why not use multi-colour LEDs?* RGB lights look too garish for us. Would certainly be possible though. 
- *Could you have used a camera and AI for this?* In short, no... the quality would suck. I briefly considered cameras, multi-cameras, depth-sensors, lidar... but (besides the cost) none of those would give the feeling of activating a key with your foot. Would have been fun to try though. 
- *You could sell this!* This is just for fun. 
- *No really, I would really really really like to buy one* Sorry. I would consider it if you're willing to make a large donation to thelifeyoucansave.org, pay costs and you're very patient. 
- *I live nearby, can I take video?*  Sure, if you don't post on social media... it's our home. 
- *Can I copy?* Sure! All the design files are on github, CC-BY license. Send me a photo I'd love to see it. Link to this page for attribution. 

### What was hard
- Foam
- Waterproofing
- Sensor choice
- Drainage
- Cable entries


## Technical Details

### Architecture:
![]

### Exploded view of one paver:
![]

###Design Goals:
- Steps that light up!
    - 17x pavers + 6x steps up to the front door  ✓
    - Young kids and adults detectable. Stretch goal: 4kg cat  ✓
    - Lights visible during day (direct sun) and night  ✓
    - Can turn all lights on - to allow people to see at night  ✓
- Sounds 
    - Piano mode  ✓
    - Scales: major/minor/pentatonic  ✓
    - Synth patches (.sf2)  ✓
    - "song mode" that plays a track as you walk down the path  ✓
    - Low latency from keypress to hearing sound - <100ms  ✓  stretch: 30ms   ☐ almost
- Can be safely left on all the time  ✓
- The "before" and "after" photo look the same   ✓
    - no big boxes or lights bulging  ☐ almost
    - Keep original pavers  ✓
- Warm-white lights only - colour would be fun but too garish  ✓
- Stretch goal: responsive enough to play a key twice in quick succession (eg mario has quavers at 180bpm ~= 150ms)  ✓
- Recycled components (from the bin at work) as much as possible  ✓
- Cheap - $200-300. ✗  $500. ✗  $700. ✗  $1000.  ✓
- Done in a couple of weeks. ✗  3 months. ✗  Before August. ✗   Before Christmas. ✗  Real soon now.  ✓
- Stretch goal: 5 year design life  



### Music
Piano mode:
Piano patch came from:
Mario patch came from:
I liked a different patch for the pentatonic scale:
For pachelbel's canon I used this patch: 

Song mode:
It's surprisingly hard to find tracks that sound good cut up into 23 little tiny pieces. There are a few choices for how to cut: 
- each sample is one (or two) beats long - eg Imperial March
- each sample is one note of the melody - eg mario
- one key starts a "backing track" and other keys are samples that get played on top - eg Harder Better Faster Stronger

To cut up a music track into 23 samples I used wavesurfer.js to make a simple gui `audio.html`:

The cut timestamps are exported to json and manually inserted into `song_catalogue.json`. The head app keeps the whole audio file in memory and just jumps to the right location when a key is pressed


#### Responsiveness
Making the sound/light feel responsive took effort, but thankfully didn't require pulling out all the stops. Design goals:
- low latency from foot to light
- low latency from foot to sound
- ability to repeat notes quickly

Lights: sensors polled in 80Hz mode = 12.5ms period. Average latency is 12.5/2 + a little more since 6 sensors are polled in succession = <10ms. Filtering on sensor input is basic to avoid delays. Result: light feels instant to a user. 

Sounds: Harder. Generated by the head RPi. Achieved a good result, feels "instant". Under 100ms avg latency:
- <10ms from sensor polling (as above)
- 12ms avg from head polling the nodes (42Hz)
- 20ms(?) from audio stack in RPi OS
![]

First attempt was 300-400ms. Used these optimisations, most effective first: 
- switched to a USB sound card not the built in RPi, which doesn't offer low latency with ALSA, at least on this OS version
- tried several sound libraries on RPi. Settled on sounddevice for playing samples and fluidsynth for playing soundfonts. Both offer low latency
- load whole audio file into memory on initialisation, samples are not loaded dynamically/separately. See `song_mode.py` and `fill_audio_buffer_callback()` in particular
- moved node 3 to a different UART so it can be simultaneously polled. Could go further and have one per node but had already hit target. 
- serial comms polling & response is a single byte either direction
- used RTS pin on UART to drive the RS485 write-enable input instead of directly writing to pin. This removes the need for any 5-10ms delays between send/receive which were previously required to account for variability in when the UART device would actually send. 
- nodes check for serial comms after each sensor, not after all 6 are read

Repeat notes:
Goal: can play a key twice in succession, eg fast enough to play the mario theme: 180bpm, the first two notes of the fanfare are repeated quavers, or ~150ms. Node states are polled at ~42Hz, or 24ms, so that's plenty. But it means I can't use eg a 5-point median filter on sensor inputs to fix an outlier/noise issue I saw - had to find a different solution. It's very satisfying to "double tap" a key! 



### Fails:


### Ideas for "Next time" - what would I do differently?

Waterproofing and UV-proofing took *weeks* longer than I expected. Normally everything I design is used indoors! If I was willing to spend more I could replace all the pavers with a thinner tile, enabling a new design for under-tile: a water-tight flat 'box' with transparent sides containing load cells, LEDs and maybe microprocessor. Seems like a heavy lift to make 17 of those but would likely be no more effort than I spent adhering and sealing everything. The compromise would be price these custom boxes and needing to replace all pavers in the yard, even the ones without sensors. 

Hard to say whether "one node per 6 steps" was a net benefit over a fully-distributed one-microprocessor-per-step. I think it's just grass-is-greener. Making the node boxes waterproof and running trunk cabling was more effort than expected, but waterproofing 17 microprocessors and cable entries for those would have also been tough. Though at scale, distributed would be the way to go. Put the load cell amp and an ESP32 in a waterproof housing with a custom PCB instead of wiring. Daisychain power and comms in waterproof glands. More design work but would be quickly amortized.

I avoided a custom PCB for the node boxes by finding pre-built modules, but would have been fun. I underestimated the time to hand-wire everything together (as usual) so it wouldn't have been too much extra effort to design a PCB to solder all the modules to. 

![]

Burying 2 nodes under pavers was a (requirements) mistake. With heavy rain, it's completely submerged for hours. Node 2's failure-by-inundation was an "early death" presumably due to build error, but with 50C temperature swings I think a leak is inevitable. Should have changed the "no visible boxes" requirement earlier - now, hidden in the grass, it'll be splashed (IPx4), not submerged (IPx8). Huge difference, much easier.  

Wired serial may have been unnecessary - took some effort to run cables and waterproof. Could have just used wifi for nodes 1 & 2 or zigbee if my fear of wifi came true. 

