---
layout: page
---


<!-- title: "The Piano Path Project" -->


<!-- <video style="max-width: 100%; height: auto;" width="640" height="480" controls autoplay muted loop>
<source src="/assets/clap_toaster.mp4" type="video/mp4">
 Your browser does not support the video tag.
</video> -->

I turned my front path into a light-up keyboard:
![]()

Piano mode:
![]()

It looks pretty cool at night:
![]()

BIG Piano:
![]()

Song mode:
![]()

Daft Punk mode: (at night!!)
![]()

Open door ("welcome mode?")
![]()

Designed and built from scratch, using *mostly* recycled stuff from work. 

It took about 9 months worth of "hobby time" all-up, roughly equal parts:
- experimenting 
- iterating the chosen design
- building & waterproofing(!!) the steps
- integration (aka fixing mistakes)
- landscaping

My original budget was $250... because "*really, who can justify spending money on front path lights*". Blew RIGHT through that, of course... more than 5x. But would have been a lot more if I bought everything new!

<!-- 

This one is close to my heart (and soul)...

In 20xx a mate and I made a viral video, eventually resulting in Microsoft creating an unsuccessful XBox Kinect game based on our concept. 

The idea came from an earlier project with an XBox kinect that eventually resulted in Microsoft releasing an unsuccessful XBox Kinect game.
 -->

### How it works

Imagine a set of (waterproof) bathroom scales underneath each paver. Glue on outdoor LED strips. For the 6 steps up to the patio, add an "IR tripwire" sensor and downlights to match. Add some electronics for brains & power distribution and write some software to run it all. Then, "just add waterproofing". But actually, quadruple the amount of waterproofing you're imagining. That's about it! Easy!

For technical details, see below...


## Q&A
<!-- - Why??? 
- *How?* I built it, from scratch. The key two ingredients were trial and error. Also, recycled stuff from the bin at work, waterproofing supplies, open source SW, cheap electronics, 3D prints and landscaping supplies.
- *How long?* Around 9 months worth of "hobby time". Perhaps a quarter of it experimenting with different technologies, one quarter iterating the chosen design, one quarter building/waterproofing steps and one quarter integration and fixing issues. The biggest surprise to me was "outdoor-proofing" - making 23x2 pieces of electronics robust to complete submersion, UV and 50C temperature swings - took a LONG time. 
- *How much?* Original goal: $250, relying mostly on recycled components. Blew RIGHT through that... probably $1000. But would have been a lot more (3-5x?)if I bought everything new
 -->
**You did this from scratch? How?**<br>
I'm an engineer. Which is to say, I googled a bunch and asked a bunch of advice 

**Do you leave it on all the time?**<br>
It's often on 'silent mode' between 8.30am and 8.30pm, unless it's down for "maintenance"

**Does it use much power?**<br>
Under 10W in idle, around 1/20th of my fridge

**Can it play my fav song XYZ?**<br>
Surprisingly few songs sound ok cut up into 23 little chunks, but sure anything is possible 

**Why not use multi-colour LEDs?**<br>
It would look too garish for us - gotta draw the line somewhere :). Certainly possible though. 

**Could you have "just" used a camera and AI?**<br>
In short, no... the quality would suck. I briefly considered cameras, multi-cameras, depth-sensors, lidar... but (besides the cost) none of those would give the feeling of activating a key with your foot. Would have been fun to try though. 

**You could sell this!**<br>
Yeah nah, it's just for fun. 

**No really, I would really really really like to buy one**<br>
Sorry. I would consider it if you're willing to make a large donation to [thelifeyoucansave.org.au](http://thelifeyoucansave.org.au), pay the costs and you're very patient. 

**I live nearby, can I take video?**<br>
Sure, if you *don't post on social media at all*... this is our home!

**Can I copy?**<br>
Hell yeah! All the design files are on [github](TODO)<!--TODO-->, CC-NC-BY license. Send me a photo I'd love to see it (and post it here if you like!). Link to this page for attribution. 

---

## Technical Details

### Architecture:
![Piano Path Architecture](/assets/piano-path/architecture.png)

### Exploded view of one paver:
![Exploded view of one paver](/assets/piano-path/paver-exploded.png)

### Design Goals:
1. Steps that light up!
    - 17x pavers + 6x steps up to the front door  <span class="green-text">✓</span>
    - Young kids and adults detectable. <span class="green-text">✓</span> Stretch goal: 4kg cat  <span class="green-text">(✓)</span>
    - Lights visible during day (direct sun) and night  <span class="green-text">✓</span>
    - Can turn all lights on - to allow people to see at night  <span class="green-text">✓</span>
1. Sounds 
    - Piano mode  <span class="green-text">✓</span>
    - Scales: major/minor/pentatonic  <span class="green-text">✓</span>
    - Synth patches (.sf2)  <span class="green-text">✓</span>
    - "song mode" that plays a track as you walk down the path  <span class="green-text">✓</span>
    - Low latency from keypress to hearing sound - <100ms  <span class="green-text">✓</span>  stretch: 30ms <span class="red-text">✗</span>
1. Can be safely left on all the time  <span class="green-text">✓</span>
1. The "before" and "after" photo look the same   <span class="green-text">✓</span>
    - no big boxes or lights bulging  <span class="green-text">(✓)</span>
    - Keep original pavers  <span class="green-text">✓</span>
1. Stretch goal: responsive enough to play a key twice in quick succession (eg mario has quavers at 180bpm ~= 150ms)  <span class="green-text">✓</span>
1. Recycled components (from the bin at work) as much as possible  <span class="green-text">✓</span>
1. Cheap: <s>$200-300</s> <span class="red-text">✗</span>  <s>$500</s> <span class="red-text">✗</span>  <s>$700</s> <span class="red-text">✗</span>  $1000 <span class="red-text">✗</span> 
1. Done in <s>a couple of weeks.</s><span class="red-text">✗</span>  <s>3 months.</s><span class="red-text">✗</span>  <s>Before August.</s><span class="red-text">✗</span>  <s>Before Christmas.</s><span class="red-text">✗</span> Real soon now<span class="green-text">✓</span>
1. Stretch goal: 5 year design life 



### Picking a Sensor

I probably went though 10 different options before settling on [load cells](https://www.aliexpress.com/item/1005006593556468.html) for pavers and "IR tripwires"  for the steps. 

![Sensors](/assets/piano-path/sensors.jpg)


|Requirement | Notes |
| --- | --- |
| detect foot-step | Adults & kids. Bonus: cat |

- detect foot-lift - allows player to change note lengths. A late addition, realised during experiments. 
- multiple people playing multiple steps at once - don't force people to go one at a time
- latency <100ms 
- nothing sticking up over pavers - will get kicked & destoyed
- lots of leaves fall in autumn. Should be robust to this
- cheap - <$5 per step? Total 23 steps to detect
- no false-triggers - don't want lights randomly turning on 
- no double-triggers - don't want flicker on or weird double-notes
- IP68 rating - will be completely submerged for hours. Silt buildup over months/years
- Temperature 0°C-60°C - some pavers get direct sun on 40°C days
- works under direct sun and at night - this killed several IR reflective and lidar options
- for 6 steps up to porch: can install without pulling up the tiles
- Bonus: minimise support electronics, cabling, etc.

I tried/considered: accelerometer under paver, microphone under paver, lidar depth sensor, fancy lidar, camera, multi-camera, depth camera, IR reflective, IR with retroreflector, IR tripwire, ultrasonic distance sensor. 

**Load cells** ticked all the boxes for pavers at the expense of being fiddly to wire up 4 cells + 1 pcb for each. The result was great quality and responsive enough: 80Hz or about 6ms average latency.

The 6 steps up to the porch were different by necessity - the steps are tiled so nothing could go under. Direct sunlight is the achilles heel of many of these sensors (I learned), so I was forced to use an **IR tripwire**. The signal is modulated at 40kHz (like a TV remote) and the sensor rejects other frequencies, which is what gives it enough dynamic range to work in sunlight. It's nice and cheap but I had to wire in something on the far side of the step, which required building in a whole new siding to the steps.


### Music
**Piano mode:**
I dithered a bit about what scale to choose: all 12 notes? Just the major scale? Minor? Pentatonic?

In the end, major is a good default. Pentatonic sounds nice when there are lots of people at once - picking a nice "pluck" soundfont helped - but most people expect major and 23 notes equals 3 octaves exactly. Perhaps 12-tone chromatic could have worked if I was willing to paint the black keys, but that violates the "the before and after photo look the same" requirement.

The settings webapp can toggle preset combos of soundfont and scale. 

I'm using [pyfluidsynth](https://pypi.org/project/pyFluidSynth/) to play soundfonts, which works great. 

'Pachebel's canon mode' is also done with this mode, since song-mode doesn't allow multiple notes at once. Players start in canon, with keys picked to follow the melody not a scale. 

![]()

**Song mode:**
This mode plays arbitrary samples, not patches. So it can be any audio file, cut up into pieces. Although, it's *surprisingly* hard to find tracks that sound good cut up into 23 little tiny pieces. There are a few choices for how to cut: 

1. keep each sample a constant one/two beats long, so the player walks at steady rate - eg Imperial March
1. each sample is one note of the melody, so the player walks to rhythm of melody - eg mario
1. one key starts a "backing track" & other keys are samples that get played on top - player walks to rhythm of melody - eg Harder Better Faster Stronger

To cut up tracks into samples I used [wavesurfer.js](https://wavesurfer.xyz/) to make a simple gui `audio.html`:

<!-- TODO -->

The cut timestamps are exported to json and manually inserted into `song_catalogue.json`. 

The head app keeps the whole audio file in memory, jumping locations ("seeking", I guess) when a key is pressed. To keep latency low (especially when changing notes mid-sample), I ended up manually filling the audio buffer. [Sounddevice](https://python-sounddevice.readthedocs.io/) & [soundfile](https://python-soundfile.readthedocs.io/) made this easy. 


### Responsiveness
Making the sound/light feel responsive took effort, but thankfully didn't require pulling out all the stops. Design goals:
- low latency from foot to light
- low latency from foot to sound
- ability to repeat notes quickly

**Lights:** <br>
Sensors polled in 80Hz mode = 12.5ms period. Average latency is 12.5/2 + a little more since 6 sensors are polled in succession = <10ms. Filtering on sensor input is basic to avoid delays. Result: light feels instant to a user. 

**Sounds:** <br>
Harder. Generated by the head RPi. Achieved a good result, feels "instant". Under 100ms avg latency:
- <10ms from sensor polling (as above)
- 12ms avg from head polling the nodes (42Hz)
- 20ms(?) from audio stack in RPi OS
![]()

First attempt was 300-400ms. Used these optimisations, most effective first: 
- switched to a USB sound card not the built in RPi, which doesn't offer low latency with ALSA, at least on this OS version
- tried several sound libraries on RPi. Settled on sounddevice for playing samples and fluidsynth for playing soundfonts. Both offer low latency
- load whole audio file into memory on initialisation, samples are not loaded dynamically/separately. See `song_mode.py` and `fill_audio_buffer_callback()` in particular
- moved node 3 to a different UART so it can be simultaneously polled. Could go further and have one per node but had already hit target. 
- serial comms polling & response is a single byte either direction
- used RTS pin on UART to drive the RS485 write-enable input instead of directly writing to pin. This removes the need for any 5-10ms delays between send/receive which were previously required to account for variability in when the UART device would actually send. 
- nodes check for serial comms after each sensor, not after all 6 are read

**Repeat notes:**<br>
Goal: can play a key twice in succession, eg fast enough to play the first two notes of the mario theme: two quavers at 180bpm ~=150ms. Node states are polled at ~42Hz, or 24ms, so that's plenty fast. But it means I can't use multipoint filtering/smoothing... for example, it would have been handy to throw a 5-point median filter on the output to fix an outlier/noise issue I saw. Had to find a different solution.  

It's very satisfying to double-tap a key! 

<!-- vid?? -->

### What was hard
- Foam
- Waterproofing
- Sensor choice
- Drainage
- Cable entries


### Ideas for "Next time" - what would I do differently?

For electronics, I chose "one node per 6 steps" over a fully-distributed one-microprocessor-per-step. Hard to say if this was the right call. Making the node boxes waterproof and running trunk cabling was more effort than expected, but waterproofing 17 microprocessors and cable entries for those would have also been tough. I think it's just grass-is-greener doubt.... but at scale, distributed would indeed be the way to go. Put the load cell amp and an ESP32 in a waterproof housing with a custom PCB instead of wiring. Daisychain power and comms in waterproof glands. More design work but would be quickly amortized.

I avoided a custom PCB for the node boxes by finding pre-built modules, but would have been fun. I underestimated the time to hand-wire everything together (as usual) so it wouldn't have been too much extra effort to design a PCB to solder all the modules to. 

Waterproofing and UV-proofing took *weeks* longer than expected. Normally everything I design is used indoors! If I was willing to spend more I could have saved that effort. This alternative design would replace all the pavers with a thinner tile, enabling a new design for under-tile: a water-tight flat 'box' with transparent sides containing load cells, LEDs and maybe microprocessor. Seems like a heavy lift to make 17 of those but would likely be no more effort than I spent adhering and sealing everything. The compromise would be the price of these custom boxes and needing to replace all pavers in the yard, even the ones without sensors. 


![]()

Burying 2 nodes under pavers was a (requirements) mistake. With heavy rain, it's completely submerged for hours. Node 2's failure-by-inundation was an "early death" presumably due to build error, but with 50C temperature swings I think a leak is inevitable. Should have changed the "no visible boxes" requirement earlier - now, hidden in the grass, it'll be splashed (IPx4), not submerged (IPx8). Huge difference, much easier.  

Wired serial may have been unnecessary - took some effort to run cables and waterproof. Could have just used wifi for nodes 1 & 2 or zigbee if my fear of wifi came true. 

