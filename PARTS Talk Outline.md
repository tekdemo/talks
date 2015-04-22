# Tips, tricks and traps
- A quick guide to designing your first PCB

# intro


# The General Process
- Figure out what your board needs to do
	- Inputs
	- outputs
	- Controllers
	- Sensor Data
	- Microcontroller? Analog?
	- Just for you, or future product?
- Part Selection
	- Cost is a huge factor, but not the only one
	- More expensive parts often have greater values
	- Compare and contrast
	- Voltage Ratings
		- All parts have a maximum input voltage rating. 
		- You want the part's input voltage rating to be higher than the voltage you provide it
	- Datasheets = <3
	- Don't be afraid to get variants and breadboard them.
		- Breakout boards are a cheap and easy way to get SMD parts tested.
- Schematic / Breadboard
	- For prototype designs, it's helpful to do this together. 
- Board Layout / Routing
- Edit Schematic
	- Add missing parts
	- Replace hard-to-use or inappropriate parts
	- Adjust nets with hard-to-route wires
	- Add jumpers if needed
	- Add expansion pins
- Redo Layout and routing
- Prep for fabrication
	
# Your first board
- Will probably be wrong: Make it small and cheap.


- Things that will probably go wrong:
	- Part interferences and spacing
	- wrong footprints
	- Poor sizing of text
	- Poor choice of via + pin size
	- Headers are backwards
	- Poor choice of parts
	- hard to assemble
	- General Assembly errors (burning parts, burning pads, losing silk)

	
- How to get the most from your first board:
	- Build 2:
		- One for fixing it at all costs
		- One for verifying "successful" fixes
		- I like one unbuilt board as a control
			- Useful for assembly
			- Useful for reference when making corrections. Saves trip to laptop.
			- Good for reference on re-routing later
	- Make notes of labels, spacing, and text size that works well, and what doesnt
	- Avoid microcontrollers for now
		- Microcontrollers add a lot of other complexity
			- Need for (correct) programming headers and bootloaders
			- Functional Code 
			- Bus and IO directions need to be correct
			- You don't need all those extra errors on your first board.
		- Instead, build an Arduino Shield, Pi Hat, Beaglebone Cape, etc. 
		
- Things you'll find: 
	- May develop preference/hatred of certain footprints. 
	- May find a better process that works for you
	- It's less stressful the second time.



# Glossary: Terms you'll probably need and no one just puts in one place for you
- Trace
	- The "wire" formed by thin bits of copper on the design tool. 
- Via
	- A hole with copper plating, so it can connect the top and bottom copper layers
	- Often used for "through hole" components
- Header 
	- Typically refers to a connector for hooking up cables, wires, or other boards
	- In layout, often refers to the large vias you'll use later for such connectors
- through hole components
	- Component with long metal leads. Requires a via for connecting 
- SMD / SMT Components
	- small parts that just sit on exposed copper pads. Don't require vias for assembly. 
- Net
	- In schematics, refers to a specific signal. 
	- A single net may connect to several parts, vias, 
- Copper Pour
	- Also referred to as a "plane", often prefixed with the net name (usually "ground plane")
	- This is a large copper area created by a special design tool. 
	- Will automatically connect to nets it belongs to, and back away from connections it shouldn't.
- Bus
	- Refers to a group of nets that carry a common communication signal
	- Common ones are I2C, UART, USB, Ethernet, SPI, etc.
- Annular ring
	- Extra copper around each via. 
	- Ensures that plated holes have a solid connection to a trace when manufacturing tolerances come into play
- DRC - Design Rule Check
	- Rules entered into your design tool that ensure you don't screw up major stuff.
	- !! Don't catch everything
	- !! Don't always enforce best practices.
- DFM - Design For Manufacturing
	- Guidelines for making better boards with fewer problems. 
	- !! Usually not enforced in design tools, and must be done manually.
- Schematic
	- The symbolic connections between parts. 
	- Connects Nets and busses, not "traces". 
- PCB Layout / Board Layout
	- Also called "Routing"
	- The proces of setting up physical connections via traces on your PCB files. 
- IC: Integrated circuit
	- Basically, anything that goes on a board coated in black plastic. 
	- Microcontrollers, 
- Package
	- Describes the specific physical properties of an IC.
	- Usually has a "family" specifier, followed by the number of exposed pins. 
		- DIP-8 means Dual Inline Pin with 8 pins exposed. The DIP family is breadboard friendly.
		- DIP-16 conversely, has 16 pins. 
		- *Lots* of acronyms, and sometimes vendor-specific. Read the datasheet.
		- !! Many packages are very close in size, or can even be switched.
		- !! Sometimes you can change from A->B easily, but not B->A without significant effort.

# Picking a Design Tool
- Cost To You
	- Free forever? 
	- Free now, upgrade later?
- Feautures / Upgrade Path
	- "Free" may not mean a long-term cost of $0
		- Eagle and web-based tools are notable here.
	- Subscription fees may wind up being more expensive than an up-front liscence
	- A true $0 design tool may be expensive in terms of making up for it's shortcomings. 
	- Evaluate your needs honestly.
	- Beware the feature cap 
- Cost To Others
	- A serious thing to consider for designing open hardware
	- Forcing others to buy software to open your design can be limiting
	- However, designing fewer or inferior products due to limited tools is counterproductive 
- Ease of use + Learning Curve
	- Somewhat dependent on each person.
	- Some tools that make the easy stuff easy make the hard stuff nigh impossible.
	- A good community helps a lot.
- Community + Documentation
	- You will need to look up how to do something. 
	- If you can't, you want to be able to ask for help.
	- Altium wins for documentation, Eagle and KiCAD win on community.
	- Does the community you work within have a canonical standard? 
		- If so, you may weigh compatibility heavily. 

- Existing Part Libraries
	- This shortents the time between "no design" and "working board"
	- Does not eleminate the need for your own. You will need to learn to create these.
- Quirks Mode: Every design tool sucks in it's own unique way
	- Some tools will just upset you. 
	- Some tools do very well in certain areas
	- Some tools will upset you horribly only once you get used to them.
	
- Clearly Biased Suggestions
	- KiCAD: 
		- Free and open source 
		- Great Community
		- Many feautures not available in any other free design tool
		- No artificial restrictons, and can do large or multi-layer boards. 
		- !! Quirky, lots of version specific issues, 
		- Actively improving
	- Eagle: 
		- Very easy to get started with
		- Lots of easy libraries 
		- Flexible CAM and Layer setup is great for artistic work
		- Lots of open designs are built with it
		- !! Very stagnant. Almost no new feautures in the last several years, and no obvious upcoming ones
		- !! Lots of artificial restrictions on free versions

# A bit about Libraries
- Trust, but verify
	- Always verify every part footprint. 
	- All libraries will have an error.
		- You will find it.
		- It will be aggrivating.
	- Other users may have designed it differently than you would like
		- For example, it may work well for high-density board layouts
		but not be good for assembling with a soldering iron. 
	- Footprints may have been for a different variant of a part. 
		- Frusturatingly  common for voltage regulators, transistors, and other analog circuits
- Part Libraries have three different parts. 
	- Footprint (sometimes called land pattern)
		- This is the what will wind up on the PCB
		- Usually looks very generic, as footprints are fairly standardized
		- Corresponds with the "Package" of the IC going on the board.
	- Symbol 
		- This is the representation in the Schematic
		- For analog parts, usually shows the standard electrical symbol, with the pin hookups 
		- For ICs, usually a block diagram, split up, or shows multiple electrical symbols.
	- Device or Component
		- This is how the "symbol" maps to the "footprint"
		- Often have multiple variants, that map the same symbol to a variety of footprints
			- Allows you to say, swap a DIP-8 through-hole package for a TSSOP SMD one
		- !! Sometimes a single devices broken into multiple symbols
			- Common on "Dual" or "quad" parts, such as op amps, transistors, or motor drivers. 
			- Sometimes Power and Ground nets are treated as separate parts. 
- Don't worry too much about solid community libraries
	- You'll need your own in the future
	- Not much work when you get the hang of it
	- You can build them to your preferences for design, pad size/spacing, and silkscreen
	- You can (usually) trust your own library
		
# Schematic Layout	
- Datasheets: A dummies guide to correctly hooking up an IC
	- Often show components needed to make ICs work well or better
	- Often have variations for using them in unusual ways, or for best performance
	- Highly suggested to save them alongside your design. You'll use them a lot. 
- Name your nets
	- Names make it easy to find when doing the board layout 
	- Helps prevent connection layers
	- Allows you to place visually significant name tags
	
- Don't worry about connecting the nets with solid lines.
	- Use names and flags to isolate sub-sections of your board
	- This is a good place to add basic notes about your design decisions
		- You already have it open and are looking at datasheets. 
		- Is this circuit built in an unusual fashion? Explain what it does. 
		- Did you spend forever dedicing which part to use? Explain why this one was used
		- Good filler for documenting later. 
- !! Remember: Library symbol != IC pin layout != datasheet pin ordering 
	- Sometimes they royally screw this up, and make it confusing. Redraw it if you have to.
		
- Pin Swapping / Gate Swap
	- Lets you move a net from one pin to another. 
	- Assumes that the library component supports it. 
		- Often faster and easier to simply delete a wire and re-route it manually.
- Common conventions: 	
	- Power flows from top to the bottom of the schematic:
	- Signals flow from the left to the right:
		- Not always possible, but generally followed
	- Avoid running long lines to Power and Ground. 
		-Gets very messy that way. Use schematic symbols to connect them together
	- Most (not all) part symbols obey this
		- The ones that don't will be caught by your meticulous checking .
	- Active Low nets should be designated as such. 
		- Usually shown by prefixing the Net name with a lowercase "n" (such as nEnable)
		- Sometimes shown as having an overline
	- For confusing input or output only ports, add INPUT or OUTPUT to the net name. 
		- Common for UARTS: `TX_OUTPUT` is much less confusing than `TX`. Who's TX is it?
- Add some LEDs to provide status LEDs
	- Add one to the regulated power source
	- A micro-controller controlled LED will provide a status indicator that your code is working
	
		
# Powering the Board
- Off-board power
	- Wall Wart
	- USB
	- Cheap and easy, but tethers your project to a  power source. 
	- Ideal for a large variety of projects.
- Batteries
	- Lipo? NiCAD? Alkaline? 
	- Voltage ranges may cause issues if you're not careful
	- What about charging?
		- ICs make it easy.... but don't lose scope on your project.
		- Using external chargers are kind of annoying.
		- !! Charging incorrectly can be a fire hazard
		- !! Over-discharging can cause battery failure.
	- Low power design
		- Also impacts code and firmware. That's a whole separate issue.
- Linear Regulators
	- Simple
	- Cheap
	- Can be inefficient
	- Beware the max voltage
	- Good for starters
	- !! Watch for the voltage drop. Especially problematic on batteries
	- !! Generate a lot of heat for large voltage drops
- Switching Regulators
	- More complex
	- More components
	- More PCB area
	- Often more expensive than linear
	- Can provide very large voltage drops with high efficiency
		- eg: Running 3.3V electronics from a 12V battery 
	- Can provide more voltage than your power source provides.
		- eg: 5V from a single 1.2V battery.
- Unregulated Battery power 
	- !! may cause serious and unexpected issues. Here Be Dragons
	- !! May drive many component choices due to battery voltage ranges
	- Good for very simple blinky circuits, particularly with LiPo batteries
	- Older ICs and many analog ICs have no problem with a wide voltage range
		- However, you might get erratic results at some point.
- Circuit Protection 
	- Definitely good idea when moving past initial prototypes
	- Reverse Polarity protection can be as simple as a single N-Mosfet
	- Overcurrent/short protection is only a bit more complex
	- Overvoltage is great when handling unknown scenarios
	- Can buy protection ICs to do all of this in a single part.
	
# Board Layout
- Design Rules
	- The critical specs:
		- Minimum Drill size
		- Annular Ring
		- Trace Spacing
		- Trace Width
	- The Less critical ones:
		- Mask Expansion/Retraction: The fab can over/under expose areas around other pads. 
		- Minimum soldermask web: Determines how wide any particular bit of soldermask can be 
		
- Datasheets: A dummies guide to layout
	- Always has package information and footprint pitches
	- For complex chips, sometimes include suggested circuitry alongside footprint
	- Very helpful for high-power or analog parts.
	- Often has suggested routing patterns, and usually includes routing of suggested components.
- Know Thy Footprint
	- Verify each footprint you haven't personally used. 
	- Once you have named nets on the schematic and are looking at a pcb footprint, this is easy
- "nets"
	- Net rules and DRC rules: Can help you catch errors in advance
	- Great for power traces, and helping visual identification of power traces
- Design for debugging
	- Add test points
- Ground paths
	- Electroncs run in a loop. Try to figure out the "loop" when supplying power from one component to another.
	- For good ground paths, anytime one component powers another, simply run both power and ground at the same time. 
	- Some circuits require good grounding power paths (such as switching regulators and analog parts). 
	- Most circuits are tolerant of poor grounding, until you do it very wrong.

- Bus routing
	- Route all bus wires at the same time, to make sure they're kept about the same length. 
	- Double check who is transmitting, and who is recieving. 
	- Net names help a lot for getting this correct
	- Add a "swizzle" part that makes it easier to correct when you screw it up. 
		- Some parts make it very unclear how to do it right, so you WILL get this wrong eventually.
		- ![A good smd swizzle][] 
- Layout Decisions:
	- Thermals
		- Makes soldering easier on ground connections
		- Improves reflow by preventing part movement
		- !! Can hurt current rating on high-power boards (sorta)
	- Tenting
		- Often looks better
		- Helps with reflow and hand soldering
		- Can improve board density
		- !! Makes patching errors more difficult
	- Ground plane or no
		- Don't put a ground plane near any radios (wifi, bluetooth). 
		- Often make routing easier
		- !! Can make you very sloppy about ground paths. 
	- Hot Components
		- Voltage regulators
		- Motor Drivers
		- Mosfets
		
- Group Components to form logical blocks
	- Each block has it's own inputs and outputs
	- Build blocks first, then worry about space constraint and board size. 
- Don't fear SMD (just respect it)
	- Courtyards / keep outs zones
	- Orientation matters when hand-soldering
	- Placing components really close together will make it hard to assemble. 
- SMD Components on one or both sides?
	- Assembly is much easier with only one side
	- for 2 sided, mostly stuck with hand-soldering at least some parts.
- TRUST NO ONE. Especially you.
	- Make sure to verify things.
- Autorouters
	- Fast, simple way to make a very terrible board
	- Tends to produce non-ideal layouts, noisy signals, and difficult to correct boards
	- Knowing how to configure net rules makes it less terrible
		- But, requires lots of design tool knowledge and initial setup.
	- For your first few boards, avoid autorouting. 
	- Once you know what a board should look like, Autorouters can help speed up the easy parts.
	
- Sparkfun's locking headers. 
	- Absolutely fantastic. 
	- Hold headers perfectly while trying to solder them
	- Exist in Sparkfun's Eagle libraries (Connectors > M0# >M0#-LOCK)
	- Need to lay out your own in other design tools
	- [Details about it here](https://www.sparkfun.com/tutorials/114)

# Bypass Caps
- Very important to functionality of circuits
	- Helps prevent noise travelling between two different components
	- Magic sprinkles of the circuit world
	
- Every IC should have it's own bypass cap

- Anything is better than nothing
	- If in doubt, put a 0.1uF cap on it. 
	- In an ideal world, figure out what frequencies your board will use, and use a cap to block it
		- Becomes more critical when desigining RF components in a design 
	- !! Adding 2 identical capacitors doesn't work as you'd think. If you want to add 2, make them different values (eg, 0.1uF and 470nF)
		- (TODO: find a good link explaining this)
		
- Schematic best practices
	- Place them with each IC or component block that it belongs to
		- This reminds you that it's part of the IC when doing routing
	- !! Resist the temptation to add a "bypass capacitor" section of your schematic. You'll forget what parts need what.

	- Suggestion: Give bypass caps unique names
		- This helps differentiate them from othercapacitors that will wind up in the design
		- I tend to use `B` or `CBP` instead of the more common C prefix for capacitors
		- If possible, suffix the name with a block/IC descriptor (such as CBP_M1 for Motor Driver 1)
- PCB Routing
	- Bypass cap must be between the IC and the power/ground connections
	- Minimize trace length between power and ground connection
	- Try to reduce vias between IC and bypass cap
	- Provide a clean connection to ground
	

# About PCB Layers
- Not all layers in your design tool are used for fabrication
	- Unused layers are GREAT for adding additional details and notes about your board
	- Also great for making assembly notes, such as huge values right on the board layout
	- Sometimes tweaking the CAM setting can add a non-printing layer to other layers
	
- Some layers in the design tool affect multiple layers on manufacturing files:
	- Via Drill/Pad layers will show up on both top and bottom of the board
	- Stop mask layers will cause nearby silkscreen to be removed
	- Restrict or Keepout layers will remove copper pours
	
- Some layers have special, fab-dependent meanings
	- Common for indicating where your board edge should be, or declaring milling paths and slots. 
	- Check with your fab if things seem like they're not working right
	
# Wiring guidelines + when to care
- Some guidelines only apply when working on specific signal types. Here's a quick guide for when you 
	need to take explicit care for laying out your traces
- Note: I am not a professional layout guy. Datasheets will help, and experience is invaluable.



|                                            |  General     |  Precision   | High Speed Signals| High current | High Voltage  |
|                                            |      Analog* |      Analog* |   ( >1MHz)        |  >1A or so   |   >48V or AC  |
|--------------------------------------------|--------------|--------------|-------------------|--------------|---------------|
| trace width (beyond fab spec)              |              |         Y    |    Y              |    Y         |      Y        |
| trace spacing (beyond fab spec)            |              |         Y    |                   |              |      Y        |
| Trace length                               |       Y      |         Y    |    Y              |    Y         |               |
| via size                                   |              |         Y    |    Y              |    Y         |      Y        |
| multiple vias                              |              |         Y    |    Y              |    Y         |               |
| trace placement / adjacent signals         |       Y      |         Y    |    Y              |              |               |
| parasitic capacitance + inductance         |              |         Y    |    Y              |              |               |
| heat                                       |              |         Y    |                   |    Y         |      Y        |
| Solid ground connections (ground loop path)|      Y       |         Y    |    Y              |    Y         |      Y        |
 
- Communication busses each have their own unique requirements. Those vary wildly based on speed and signal type.
	- All busses
		- Read part datasheets: They'll explain a lot of what you need to worry about
		- Double check the connections. The connections will vary wildly, and nomenclature is often confusing.
	- Low speed: 
		- Common for SPI, I2C, UARTS, PWM, and some proprietary ones (such as WS2811/Neopixels)
		- Generally forgiving, as long as you try to follow a guide
	- High Speed: 
		- Common for USB, SPI, Network, DRAM, SRAM, and video outputs
		- Will cause you grief if given any chance. Prioritize them above other parts of your circuit, and read some white papers
	- Differential pairs
		- Pretty forgiving if you ensure the net lengths are identical
	- Other: 
		-Read whitepapers on the protocol, which will highlight what you need to care about. 
		- Most have routing guides
		
- Precision analog:
	- refers to needing accurate voltage readings in the 1-10mV range, that's not affected by other parts of the circuit
	- Most hobby-level analog is fine if your voltage swings around in a ~100mV range, and doesn't require as much care
- High Speed:
	- Common for clock inputs to microcontrollers.
	- Often refers to RF or single-ended timing-based signals
	- Never refers to PWM: PWM is meant to generate an average value, so if it's imprecise it's fine.
                                                                    


# Prepping for fabrication
- Run DRC
- Check Traces
- Check Pinouts (again)
- Check BOM Availability
- Date, version, and name on board
- Mechanical concerns
	- Mounting Holes
	- Enclosures
	- Do parts fit?
- 1:1 scale printout
	- If something looks too small, pick a different package
	- If things loook too close or hard to assemble, fix it.
	- Feel free to jab through-hole components directly into it. Good for determining hole sizes

# Version Control
- Back up everything: design files, gerbers, drill file, assembly, etc. 
- You'll need to reference the existing files
- Maybe in 6 months you need to fix it.
- Different ways: Some are better than others.
	- Manual Version Numbers (eg: Board V1.brd, Board V2.brd)
		- Great for small projects, no software required
		- Easy to forget.
		- Handy for opening old and new versions to compare differences
	- Dropbox: 
		- Good safe-keeping. 
		- Not Good versioning (30 days, hard to find specific ones)
		- Works well with manual versioning
	- Github App for Windows/Mac
		- Git is awesome for versioning
		- Official apps are very easy to use
		- Makes sure all files are saved at the same time.
		- Makes it difficult to get versions out of sync, especially when including code
		- Works well with Dropbox and manual versioning. 
		- !! Publishing repos makes it public. 
		- Can do "local only" git repos for versioning. 
# Manufacturing
- When in doubt: Ask.
- Read Fab specs before and after routing. 
- Proof gerbers
	- Drill files are especially problematic
	- !! Internal copper layers have "polarity": Make sure you provide something your fab expects
- Fabrication is non-ideal. 
	- Even the best fabs have tolerances. 
	- Always expect to get a board with the worst possible tolerance
	- Design tools are exact, and very poor at representing fab tolerances
	

# Prepping for assembly
- Get out all your tools
	- Always
		- Solering iron
		- Solder 
		- Solder braid
	- For SMD stuff
		- good, fine point tweezers. 
			- ~4 bucks at Walgreens or other farmacy.
			- Stainless steel won't stick to solder.
		- Acetone + Isopropyl Alcohol
			- Acetone Removes flux from tools and the pcb. 
			- Can also be picked up from Walgreens. 
			- Acetone is usually sold as nail polish remover

- Get BOM List, make sure you have all parts, and the correct size/package
- Double check part footprints
	- If you screwed it up, order a new part, or plan how to fix it
- Plan your component order
	- Boards are easier to put together if you have a plan. 
	- Inside out or left-to-right is usually a good plan. 
- Large scale printout
	- Helps with not getting stuck reading tiny text. 
- Stencils for reflow?


# Assembling the boards
- Skillet / Hot Plate reflow
- Hand Soldering as needed
- Proper technique
	- 2 second per joint (approximately)
	- Let things cool for multiple repeated joints.
	- Flux is your friend
- Low-volume assembly outsourcing
	- Macrofab, Small Batch, etc



# Smoke Test
- Before powering the board, check for errors. 
- Check continuity across anything involving power.
- Check resistance across Power and Ground. It should act as a diode, with + and - 
	having INF (or very high) one way, and something along the lines of 5-20K the other way
- If it fails these tests, STOP. 
	- Double check connections, and try again. 
- Verify power rails are at expected levels
	- If high, likely a voltage regulation issue
	- If low, likely a mild short. Turn it off until you can figure out the issue
	
- If 5V is acceptable, power it with a USB power hub first
	- USB automatically fails on over-current or under-voltage
	- Will help prevent damage to your board
	- If you added a power LED, you'll see it not light up to indicate a failure.
	- !! Don't supply both USB and wall power at the same time, unless you know what you're doing. Can harm your computer.
	- !! Most computer ports supply much more power than the USB spec suggests they should
		- Helps with charging phones
		- Bad for testing circuits
		- USB Hubs, on the other hand, are pretty reliably 500mA or less; and won't damage things before you catch it
		

# Questions
![My Brain is Full Can I be Excused]()


# Helpful Resources
kicad.info
SparkGap PodCast (particularly 19,20,21, 30, which relate to pcb design)
Embedded.FM podcast (easily searchable. Not a lot on PCB designs, but a lot on electronics and programming).
learn.adafruit.com
learn.sparkfun.com





# random includes
“A learning experience is one of those things that says, 'You know that thing you just did? Don't do that.” 
