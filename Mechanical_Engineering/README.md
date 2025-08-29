# Mechanical Engineering Best Practices

This document describes recommended Mechanical Engineering related practices and standards for contributing to GU Robotics. The majority of this document is relevant more broadly beyond GU Robotics, and may prove useful to you academically and in industry. 


<!-- See https://markdowntohtmlgenius.com/blog/how-to-create-a-table-of-contents-in-markdown/ 
 for ways to generate a Table Of Contents. My (Lucas Johnston's) personal preference is 
  https://github.com/ajorgensen/vim-markdown-toc-->
<!-- By using this header, it adds the Table of Contents to the Table of Contents. This is funny. -->
## Table of Contents
* [Table of Contents](#table-of-contents)
* [Nomenclature](#nomenclature)
* [Design Philosophy](#design-philosophy)
* [GU Robotics Standards](#gu-robotics-standards)
  * [CAD Software](#cad-software)
  * [File Management](#file-management)
* [Drawings](#drawings)
* [Parts](#parts)
  * [Part Design through Assemblies](#part-design-through-assemblies)
  * [Design for Manufacturability](#design-for-manufacturability)
    * [Design for FDM 3D Printing](#design-for-fdm-3d-printing)
    * [Design for Machining](#design-for-machining)
    * [Design for Laser Cutting](#design-for-laser-cutting)
* [Assemblies](#assemblies)
  * [Commercial off-the-shelf (COTS) Parts](#commercial-off-the-shelf-(cots)-parts)
  * [Design for Assembly](#design-for-assembly)

## Nomenclature

Depending on your experience, this may be your first time encountering some of the vocabulary in this document. Below is a brief list of vocabulary used for reference.

- Drawing
    - an engineering document designed to either show a part (part drawing) or an assembly (assembly drawing)
    - used to communicate specifications and designs
- Assembly
    - a collection of parts  and subassemblies that come together in some way
- Specification (often abbreviated 'spec')
    - What a certain feature/design/etc must do
    - Often you'll have certain design specifications that whatever you make needs to follow
    - Being 'in spec' means a part (or assembly) is within some allowable limits and behaves like it should
    - i.e. whether a part or assembly is usable
- Nominal
    - 'named' dimensional value, not including tolerance
    - tolerance is generally applied to this
- Tolerance
    - how much a part or assembly is allowed to vary from nominal before it's out of spec
    - e.g. &pm; .010"
- Mates
    - how parts contact each other
- Allowance
    - gap between mating components, amount of 'play' components have


## Design Philosophy

A successful design is one that takes a need statement or specification, and translates that into an actionable device/system/etc that accomplishes the given goals. For this process, it's important to focus on the needs behind a design as these are how you'll evaluate your design. As part of the design process, you'll want to consider specifications, come up with a conceptual design, get it manufactured/implemented, and validate it in some way.

It is very likely that a lot of your designs do not work as you intended them to, and that's part of the learning and iteration process. This document was written to help you avoid many common design pitfalls and to hopefully help you learn from the mistakes of those who came before you.

Generally, designs work best when they're simple and modular. You should generally be thinking of how to simplify your designs whenever possible to achieve your design goals. This is done in order to reduce unnecessary waste and complexity that might slow down prototyping, assembly, inspection, repairs, etc. By considering breaking larger designs into smaller modules, it can be easier to prototype and test each individual part, as well as letting other team members focus on certain areas in parallel with your work. Depending on the design requirements, however, this may be difficult or impossible to do and might not be a priority.


CAD tools can enable you to catch potential issues with a design as soon as possible and make it easier to document and manufacture your design.


## GU Robotics Standards

To ensure consistency across the team, as well as to ensure necessary information is documented, GU Robotics has standards club members are expected to follow.

### CAD Software
**The GU Robotics team uses SOLIDWORKS for all CAD models**. Do not use other CAD software such as Onshape or Fusion 360.

SOLIDWORKS can be accessed by signing in to any of the desktop computers in Herak. If you're not enrolled in SEAS, talk with club leadership as you will need the club advisor to reach out to SEAS IT to enable you to log on to the desktops. Additionally, SEAS IT has USB drives for downloading SOLIDWORKS if you would like to work on a personal computer. You may need to delete SOLIDWORKS and install a newer version if you install locally this way, to keep your personal computer on the same version of SOLIDWORKS on the desktops in the computer labs.


### File Management

We use SharePoint (through Microsoft Teams) to store files. **You should periodically upload your work to Teams within the Mechanical Engineering channel within a descriptively named folder.** You can use the [sync](https://support.microsoft.com/en-us/office/sync-sharepoint-and-teams-files-with-your-computer-6de9ede8-5b6e-4503-80b2-6190f3354a88) option on Teams/SharePoint to automatically sync files saved locally with SharePoint files. This works for both personal computers and shared desktops.

Any time you will be walking away from a desktop in a computer lounge, you should upload your work to the Teams file structure. Those desktops occasionally have user data deleted, and sometimes someone else will be using the desktop you initially did your work on when you go back.


## Drawings

Engineering drawings are intended to communicate design information about a part, assembly, etc. to others. They're an important part of conveying a design to other engineers for review, documenting work done, and ensuring there's an accurate list of what's needed for an assembly.

Their primary purpose, however, is manufacturing. **Part drawings should be created for parts sent out to be machined**. 

 Drawings *must* include:
- A title block with the following:
    - Your name/the names of people who designed the part
    - GU Robotics included as the organization name
    - The date when the drawing was last edited
    - A note about the default unit system used
    - The total amount of sheets in this drawing document, as well as what sheet each page is
- At least one dimension to establish scale 
    - for laser cut, 3D printed, or plasma cut parts it may not be strictly necessary to include all dimensions on a drawing if they're controlled by a model instead. However, including at least one ensures models are imported at the correct scale during manufacturing

Drawings *should*:
- Be neat and legible, with dimensions and notes being organized to be as readable as possible
- Minimize the number of datums/reference features used for dimensioning
- Include at least enough orthographic views to clarify the design
    - an isometric view of the part is also strongly recommended
- Include a descriptive name for the part in the title block
- Not include redundant dimensions (except if provided as an untoleranced reference, in parenthesis, for manufacturing)
- Have dimensions applied to views that clearly show the features you want to control
- Avoid dimension lines overlapping or crossing
- Have views from a [third-angle projection](https://engineeringtechnology.org/engineering-graphics/graphical-projection-systems/parallel-projection/orthographic-projection/third-angle-projection/) instead of a first angle projection
    - the third-angle projection symbol is not necessary to include
- Include dimensions for all features
    - if part is to be 3D printed, laser cut, or plasma cut, these may be done as reference dimensions (include parenthesis around them) or basic dimensions, and may not need linear tolerancing
    - **if part is to be manually machined/manufactured, the drawing *must* include dimensions and tolerances for all features**
        - If a dimension is identified as for reference/stock and is in parenthesis, a tolerance isn't needed
- Include a revision number/letter
    - GU Robotics currently does not have a set standard for revisioning, but using numbers for prototypes/proof of concepts and letters once the design is much more established is common in industry
- Include a note about which standard to use when interperting geometric tolerances
    - there are some subtle differences between ASME Y14.5 and ISO GPS, such as whether the default condition is [Rule #1](https://www.gdandtbasics.com/gdt-rule-1/) where limits of size control form (ASME Y14.5) or [Independency](https://www.gdandtbasics.com/independency/) (ISO)
    - Drawings should use ASME Y14.5 instead of ISO GPS

**Drawings, in particular dimensioning schemes and tolerancing, are how you convey to a manufacturer the important features of your part.** For example, if you don't really care about what fillet is used on a [turned](https://en.wikipedia.org/wiki/Turning) part, you can use MAX after an upper bound on the dimension. If you're making something that mates with a bearing, tight tolerances on that feature are how you get a part that fits with a bearing with little play. **Use tight tolerances sparingly**, as they make parts much more difficult and time consuming to manufacture. Tolerances should be based off of functional requirements for a part or assembly.


## Parts

SOLIDWORKS is primarily a part-based design software, although it does have some assembly-based design features. Familiarize yourself with SOLIDWORKS to better model parts. If you're unfamiliar with SOLIDWORKS, it's often helpful to learn by doing. Additionally, you can also **ask leadership members to organize a SOLIDWORKS workshop**. Once you have a good understanding of what it is you want to make/want SOLIDWORKS to do, work backwards to figure out how to do this in SOLIDWORKS. 

**Generally, SOLIDWORKS parts start as a (2D) sketch**, and are then extruded, revolved, or have some other feature to generate a body. Chamfers and fillets can be added in either the sketch or as a part feature, with the later often being prefered as it's easier to update or change down the line. You'll want to try and work within SOLIDWORKS in ways such that it's easy to infer design intent and so that it's easy to make changes later.

**Sketches in SOLIDWORKS should always be fully defined.** SOLIDWORKS can and will shuffle around locations, sizes, and rotation if sketches aren't fully defined, and it's not always clear how sketches will update if you add new geometry or relations. You can check if a sketch is fully defined as it'll say "Fully Defined" in the bottom right corner when you're in the sketch (or "Under Defined if it isn't) Undefined geometry will also generally appear blue, while fully defined geometry will appear black. If you can't find what's undefined in a sketch, try dragging points and features around. Outside of a sketch, in the [FeatureManager Design Tree](https://help.solidworks.com/2023/english/solidworks/sldworks/c_featuremanager_design_tree.htm), a (-) will be in front of the name of your sketch if it's under defined. [Geometric relations](https://help.solidworks.com/2023/English/SolidWorks/sldworks/c_Geometric_Relations.htm) can be used to define a sketch as well as the [smart dimension](https://help.solidworks.com/2023/English/SolidWorks/sldworks/t_Dimensioning_a_2D_Sketch.htm) tool. Oftentimes, geometric are faster and more convenient to update for duplicate features (e.g. you want to make two lengths the same, or have a bolt pattern with holes that are all the same size).


Use the IPS (Inch Pound Second) unit system for parts and assemblies in SOLIDWORKS. Often, you'll encounter dimensions that are metric (e.g. wanting a clearance hole for an M3 bolt). To make it clear where these dimensions come from, you can use an equation to store this information in a dimension. For example, using "=3mm" in a dimension instead of "3mm" can make it clear where the number used comes from, and easier to change if you need to switch to a different bolt.

[Equations](https://help.solidworks.com/2023/English/SolidWorks/sldworks/HIDD_EQUATION_MANAGER.htm) can also be used to create a parametric design, where the geoemtry is controlled by a few variables. If you find yourself repeating a dimension or allowance, it's often a good idea to create a variable and use equations instead of directly dimensioning. This can be done by searching for "Manage Equations" or right clicking on the Equation section of the FeatureManager Design Tree. Note that if you delete a sketch, you'll often end up with invalid equations as the equations outlive the sketch that they were meant to be in. You can right click on Equations in the FeatureManager Design Tree, click to the left of the equation in the selection, and use the delete key to delete these equations if they're no longer needed. Using equations like this can help with prototyping as it can let you change the allowance you have based on your manufacturing method (e.g. a different allowance for 3D printing, laser cutting, and/or machining) and to quickly revise parts when you're able to test out parts. Using Equations is not necessary for GU Robotics standards, and it's your choice whether you think they'll help you with your design process.

### Part Design through Assemblies
When designing a part, it's often helpful to also include it in an assembly and switch between the part(s) you're working on and the larger assembly they're contained in. This helps you gradually add features to the part to locate it properly in the assembly, mate it with other parts, and avoid interference issues. Assemblies are often the first and easiest place to catch avoidable design issues.

SOLIDWORKS does have features to enable you to start design from an assembly using tools like [Assembly Layout Sketch](https://help.solidworks.com/2023/English/SolidWorks/sldworks/c_Assembly_Layout_Sketch.htm). This feature can be used to help you better design systems of linkages and other moving parts that interact with each other, but isn't widely used or taught much at Gonzaga. Use of this and other assembly-based design tools are a matter of personal preference.

### Design for Manufacturability

While designing a custom part, you should be thinking about how it will be manufactured or machined. The choice of manufacturing process is largely driven by the material selection and geometry of the part. Material selection should be decided based on the part's use case. Some good questions to ask yourself about material selection are included below.
- Will the part be exposed to UV for prolonged periods of time? 
- Will the part be in a corrosive, wet, dusty, etc. environment?
- How strong does this part need to be?
- Is this part subject to cyclical loading/fatigue?
- How stiff does the part need to be?
- How strong does the part need to be? 
- How light/heavy is this material?
- Do I need any optical qualities from this part (e.g. transparency, reflecting most light)?
- How much will this material cost?

Different manufacturing processes effect the kinds of tolerances and surface finishes you can have, as well as part strength. Remember, no manufacturing process is perfect and **you will never have exactly nominal dimensions**. This also means that you'll need to **consider allowance for parts that are meant to fit with each other**.

Below are some design considerations for common types of manufacturing processes used by the club. There are many more that are not listed here that are available. You should check with other club members, the MTC, and the Makerspace to familiarize yourself with manufacturing processes available to you.

#### Design for FDM 3D Printing

To begin thinking of ways to design for 3D printing, familiarize yourself with the process of FDM printing. FDM (Fused Deposition Modeling) printing works by having a nozzle extrude layers of plastic on top of each other in an additive process to produce a part.

The primary consideration for making a part printable will be print orientation to optimize for strength and dimensional accuracy. Due to how the printing process works, layers aren't adhered perfectly to each other, and prints are much weaker along layer lines. In particular, tension and shear are weak points (compression squishes the layer lines together and isn't as affected). For geometry, features parallel to the build plate tend to be more dimensionally accurate as layer sag and other behavior affects other features.

You can expect a well calibrated printer to be within &pm; 0.3 mm of nominal geometry.

3D printing excels at producing unique and complicated geometry that other manufacturing processes can struggle with. This means you can use things such as fillets very liberally when designing for 3D printing. It's a good idea to include fillets on the wall profile on each layer, as this can reduce the chance of the part warping or experiencing bed adhesion issues.

When you have a design ready to 3D print, export your SOLIDWORKS part file as *both* an STL file and a STEP file. This is because STL's are the standard file type for 3D printing and are widely supported, but STEP files are often better quality due to how SOLIDWORKS tessellates. By exporting as both, you make it as easy and universal as possible to print.
Additionally, make note of any print settings you want. If someone else is printing this, send them these setting changes, or, better yet, upload a list of them to Teams next to the saved STL and STEP files. For smaller prints in particular, print extra parts, as filament is cheap and it's easier to do than multiple reprints.

For part drawings, if the final part is intended to be 3D printed (i.e. 3D printing isn't being used just for prototyping), it's not always necessary to dimension every feature. Instead, a note can be made saying that geometry of the part is controlled by the solid model (include the SLDPRT, STL, and STEP files). Note that leaving these dimensions and callouts for features off means you're not tolerancing these features, which can introduce errors down the line.

#### Design for Machining

Familiarize yourself with various forms of machining, such as turning (lathe) and milling. The [Manufacturing Technology Center (MTC)](https://www.gonzaga.edu/school-of-engineering-applied-science/student-experiences/mtc) at Gonzaga has various practice projects intended to give you (yes, you) first hand experience with machining. Additionally, Kevin and Beau Grillo at the MTC are generally willing to look over designs and offer feedback. Daniel Clark, who works in the Makerspace, is also an experienced machinist and can be asked to look over designs. If you ask someone for design feedback, bring part drawings and enough information for them to understand what you're trying to do. Always create a part drawing for parts you machine and print out a copy to keep with the workpiece as it's being machined into your part.

If you want 'square' sides during machining, ensure your parts are physically smaller than stock material sizes. Stock materials often have rough edges and surfaces due to how they're cut by supplies. To get a nice, clean surface, outer material will have to be removed. By keeping your designs well within the size of stock material, you ensure that the smallest stock can be used to machine your part, saving money and machine time, and tool wear.

Often, you'll want to 3D print out versions of the part you intend to machine to validate your design before committing to machining many of them depending on the time it takes to machine a part and the potential waste if the machined part doesn't work.

For machining, you want to minimize the amount of setups you need for machining your part. Changing setups takes time and can introduce inaccuracies in your parts.

Parts to be machined can either be done in the MTC, or you can get a quote from local/online machining services. Keep a copy of the part drawing for your part with you when doing work in the MTC.

#### Design for Laser Cutting

We have access to a laser cutter through the Cadwell Maker Center (Makerspace) in Bollier. This is run by Daniel Clark, and is open to students and clubs.

For design, ensure the stock that you want to cut physically fits within the laser cutter and is a material that's easily cuttable. Materials like balsa wood and acrylic are great candidates for laser cutting when thin ( &lt; 0.25"). However, materials like polycarbonate can produce toxic gas as a byproduct, and scorch along the edges, and should not be laser cut (consider machining or routing instead).

Since laser cutting works best for thin materials, and most of the materials that are well suited for laser cutting are very elastic (e.g. acrylic), you should be pay special attention to deflection while designing.

Laser cutters have some kerf to them, as the laser itself has some thickness. Keep this in mind when designing and tolerancing a part. Clearance holes made 0.1 mm larger than nominal bolt size on a laser cutter reliably result in a nice clearance fit.

Export your designs as a DXF file. Be careful that you are exporting the face of the body you care about. Often times, fillets and similiar features are done as part features and not within a sketch. If you export a sketch, these features might not be included. SOLIDWORKS will show you a preview of the DXF it generates.

When making part drawings for laser cut parts, include at least general overall dimensions. This is so it can be quickly determined if the DXF is at the right scale and avoid any ambiguity about the units of the DXF file. If the final part is intended to be laser cut (i.e. laser cutting isn't being used just for prototyping), it's not always necessary to dimension every feature. Instead, a note can be made that the geometry of the part is controlled by the flat model (DXF file). Note that leaving these dimensions and callouts for features off means you're not tolerancing these features, which can introduce errors down the line. Always ensure the DXF file and the part drawing for it remain together, and make it as obvious as possible how many parts are to be cut.

## Assemblies

Assemblies are a very helpful design tool. They are often the first place you can catch design failures, such as parts that won't fit together or forgetting cutouts for a motor shaft.


### Commercial off-the-shelf (COTS) Parts 
Very frequently a significant amount of parts in your assemblies aren't parts you've designed, but generic COTS parts. **For many parts (e.g. bearings, rods, brackets) it's often better to use COTS parts if applicable instead of reinventing the wheel.** It's generally a good idea to include these in your assemblies. Doing so makes it clear to yourself and others how parts are attached and what materials are required to make the assembly. Including COTS parts also lets you validate that everything fits, that you don't have a screw head going through a block of aluminum, that your screws are long enough to properly engage with the lock nut, etc. The vast majority of the time, you do *not* have to model COTS parts, and can just download them. You can often find CAD models for parts on the manufacturers website and from industrial suppliers like [McMaster-Carr](https://www.mcmaster.com/) (for generic hardware). Sometimes, you can also find models of hardware made by others online on sites like [GrabCAD](https://grabcad.com/library/) (will need to make an account). Note that dimensions and models found online might not be accurate for the specific part you're hoping to model, especially if from a community CAD model instead of a manufacturer, so you should get in the habit of checking some dimensions to validate the model.


If you can't find a CAD model for a part, you can make your own. It's generally best to model the part as simple as possible with geometry that's at least as large as the actual component you're modeling (e.g. using a box to represent an electronic component, using a cylinder the size of the major diameter to represent external threads). Ensure that it's still obvious what you're modeling (can be done via file name). Also ensure that any relevant mating features (e.g. mounting holes) are accurately modeled.


If you have several of the same COTS parts for a feature in a SOLIDWORKS assembly (e.g. you have a screw, washer, and nut for several holes), you only need to go through the full process of mating these features once. After that, you can select all the parts, right click them, and then click [Copy with Mates](https://help.solidworks.com/2023/English/SolidWorks/sldworks/c_copying_with_mates.htm). To use this, hit next after selecting all the components you want to copy, and then select the features to be used for each mate. Be sure to hit the check mark when you're done chosing the mate features. SOLIDWORKS will keep copying if you don't select the X, so you can copy more than once.

### Design for Assembly

When adding bolts and other fasteners, remember that **someone will need to physically get the bolt and nut into place and tighten it**. This means there will need to be enough space in your assembly (at the point in time when the fasteners are installed) to manuever a bolt in place, and enough clearance to be able to fit a driver and a wrench. Often, the most convenient way of securing a bolt is to get an allen key you keep fixed in place and grab an appropriate socket wrench that's rotated to torque the nut. Sanity check that bolts are accessible for maintenance. Avoid unnecessarily blocking the heads of screws.
