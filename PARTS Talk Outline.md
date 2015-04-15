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

- Things that will go wrong:
	- Part interferences
	- wrong footprints
	- Text wrong size
	- Poor choice of via + pin size
	- Headers are backwards
	- Poor choice of parts
	- hard to assemble
	- General Assembly errors (burning parts, burning pads, losing silk)
	
- Fix labels, spacing, and text size
- Build 2:
	- One for fixing it at all costs
	- One for verifying "successful" fixes
	- I like one unbuilt board as a control
		- Useful for assembly
		- Useful for reference when making corrections. Saves trip to laptop.
		- Good for reference on re-routing later
		
- Things you'll find: 
	- May develop preference/hatred of certain footprints. 
	- May find a better process that works for you
	- It's less stressful the second time.



# Glossary: Terms you'll probably need and no one just puts in one place for you
- Trace
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
- Bus
	- Refers to a group of nets that carry a common communication signal
	- Common ones areI2C, UART, USB, Ethernet, SPI, etc.
- Annular ring
	- Extra copper around each via. 
- DRC - Design Rule Check
	- Rules entered into your design tool that ensure you don't screw up major stuff.
	- Don't catch everything
	- Don't always enforce best practices.
- DFM - Design For Manufacturing
	- Guidelines for making better boards with fewer problems. 
- Schematic
	- The symbolic connections between parts. 
	- Connects Nets, not wires
- PCB Layout / Board Layout
	- Also called "Routing"
	- The proces of running traces on your PCB file. 
	- This is setting up the physical wires
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
- Cost To Others
	- A serious thing to consider for designing open hardware
	- Forcing others to buy software to open your design can be limiting
	- However, designing fewer or inferior products due to limited tools is counterproductive 
- Feautures / Upgrade Path
	- "Free" may not mean a long-term cost of $0
		- Eagle and web-based tools are notable here.
	- A true $0 design tool may be expensive in terms of the time you use. 
	- Evaluate your needs honestly.
	- Beware the feature cap 
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
	
# A bit about Libraries
- Trust, but verify
	- Always verify every part footprint. 
	- All libraries will have an error.
		- You will find it.
		- It will be painful.
	- Other users may have designed it differently than you would like
		- For example, it may work well for high-density board layouts
		but not be good for assembling with a soldering iron. 
	- Footprints may have been for a different variant of a part. 
		- This is annoyingly common for voltage regulators and other analog circuits
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
			- Common on "Dual" or "quad" parts, such as op amps, transistors, and motor drivers. 
			- Sometimes Power and Ground nets are treated as separate parts. 

		
# Schematic Layout	
- Datasheets: A dummies guide to correctly hooking up IC
	- Often show components needed to make ICs work well or better
	- Often have variations for using them in unusual ways, or for best performance
	- Highly suggested to save them alongside your design. You'll use them a lot. 
- Name your nets
	- Names make it easy to find when doing the board layout 
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
	
- Common conventions: 	
	- Power is on the top, ground is on the bottom
	- Avoid running long lines to Power and Ground. 
		-Gets very messy that way. Use schematic symbols to connect them together
	- Typical signal flow: Input --> Component -->Output
	- Most (not all) part symbols obey this
		- The ones that don't will be caught by your meticulous checking .
	- Active Low nets should be designated as such. 
		- Usually shown by prefixing the Net name with a lowercase "n" (such as nEnable)
		- Sometimes shown as having an overline
- For your first board, add some LEDs to help
	- Add one to the regulated power source. 
	- Helpful to know that 
	- 
	
# Powering the Board
- Off-board power
	- Wall Wart
	- USB
	- Cheap and easy, but tethers your project to a  power source. 
	- Ideal for many projects.
- Batteries
	- Lipo? NiCAD? Alkaline? 
	- Voltage ranges may cause issues
	- What about charging?
		- ICs make it easy.... but don't lose scope on your project.
	- Low power design
		- Also impacts firmware. That's a whole separate issue.
- Linear Regulators
	- Simple
	- Cheap
	- Can be inefficient
	- Beware the max voltage
	- Good for starters
	- !! Watch for the voltage drop
- Switching Regulators
	- More complex
	- More components
	- More PCB area
	- Often more expensive
	- Can provide very large voltage drops with high efficiency
		- eg: Running 3.3V electronics from a 12V battery 
	- Can provide more voltage than your power source provides.
		- eg: 5V from a single 1.2V battery.
- Unregulated Battery power 
	- !! may cause serious and unexpected issues. Here Be Dragons
	- !! May drive many component choices due to battery voltage ranges
	- Good for very simple blinky circuits, particularly with LiPo batteries

# Board Layout
- Datasheets: A dummies guide to layout
- Know Thy Footprint
- 1:1 scale printout for fit testing  ?Move to prep for assembly?
- "nets"
- Design for debugging
- Ground plane or no
- Don't fear SMD (just respect it)
- Courtyards
- TRUST NO ONE. Especially you.

# About PCB Layers


# Wiring guidelines + when to care
- trace width
- Trace length
- via size
- multiple vias
- trace placement
- parasitic capacitance + inductance
- heat
- Floating pins
- High Current signals
- High speed signals
- power traces


# Bypass Caps
- own section? Part of layout? Part of schematic?


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
- Read Fab specs before, and after routing. 
- Proof gerbers


# Prepping for assembly
- Get out all your tools
- Get BOM List, make sure you have all parts
- Double check part footprints
- Plan your component order
- Large scale printout


# Smoke Test
- Before powering the board, check for errors. 
- Check continuity across anything involving power.
- Check resistance across Power and Ground. It should act as a diode, with + and - 
	having INF (or very high) one way, and something along the lines of 5-20K the other way
- If it fails these tests, STOP. 
TODO FIXME

# Questions
![My Brain is Full Can I be Excused]()


# Helpful Resources
kicad.info
SparkGap PodCast (particularly 19,20,21)
Embedded.FM podcast (easily searchable).
learn.adafruit.com
learn.sparkfun.com
