
---

# Origin — When Small Tools Begin to Reveal Structure


## 1. The Two Files That Carried Me

For more than twenty years, I have worked between two tools:  
a 2D CAD system and Excel.

Among all the files I’ve created, there are two that I’ve kept using far longer than I ever expected:

- a very simple Excel sheet
    
- an AutoCAD drawing containing block definitions
    

They live in the same folder.  
That is the entire system.

Thanks to these two files, I survived enormous drawing workloads without breaking down—physically or mentally.  
That is not an exaggeration.

This is the story of that small tool.

---

## 2. From Muscle Memory to Commands

When I joined the company, 3D CAD was not yet mainstream.  
We used a 2D system called MicroCADAM.

It took years to internalize its icons and the specialized CAD keyboard.  
Just when I finally felt fluent, we switched to AutoCAD due to vendor circumstances.

The operation model was completely different,  
and the skill set I had painstakingly built collapsed overnight.

So although AutoCAD is a GUI tool,  
I began to avoid the icons and move toward keyboard-driven work instead—  
a style based on short aliases and small, declarative actions.

Naturally, this led me to AutoCAD’s oldest and most stable API:  
the command line.

---

## 3. The Minimal Connection: From Excel to CAD

Around twenty years ago, personal blogs were still active,  
and many CAD operators shared tips online.

One day I encountered a very small “Hello World.”

In Excel, you prepare these lines:

```
_xl
h
0,5
0,-5
```

Then paste them directly into AutoCAD’s command line.

AutoCAD responds by drawing two horizontal lines:

- one through (0,5)
    
- one through (0,-5)
    

That is all.

Yet it showed me something important:  
Excel could drive CAD with almost no friction.  
A tiny bridge had appeared between the two tools.

---

## 4. The Next Step: Placing Components

If a line can be drawn,  
a component can probably be placed.

AutoCAD will insert a block if the drawing contains its definition.  
All it needs is the name and coordinates.

It feels similar to how `#include` works in a programming language.

My first attempt looked like this:

```
-insert
block_A
10,20
1
1
0
```

Just a name and a point.  
And the block appeared exactly where expected.

From there, I began building an Excel table that matched our company’s product architecture.

---

## 5. Adding a Thin Layer on Top of the Product Architecture

Fortunately, our company’s system architecture was already modular:

- one block = one component
    
- drawing numbers managed per-component
    
- wide variation handled through combinations
    

All I did in Excel was to place a thin layer on top of this existing structure.

The Excel file remains simple even today:

- Sheet 1: a small UI for selecting specifications
    
- Sheet 2 onward: lists of drawing numbers, component names, and placement points
    
- Named ranges connecting the UI to the lists
    
- A final column generating AutoCAD command strings
    

The workflow is minimal:

1. Select a specification in the UI
    
2. Copy the generated string
    
3. Paste it into AutoCAD’s command line
    

No VBA.  
No macros.

Excel generates the command text;  
I simply paste.

Of course, this does not finish the drawing.  
The tool handles only the “spine” of large families of similar orders.  
I handle the custom design work myself.

Still, this small structure has remained stable for more than fifteen years.

---

## 6. Meaning Emerges at the Boundary

Using this tool for so long, I began to notice something.

Choosing a specification in Excel,  
copying the generated text,  
pasting it into AutoCAD—

the text itself becomes a scaffold between two incompatible sandboxes.

And across that boundary, several important properties begin to appear:

- reproducibility
    
- preservation of identity
    
- declarative operations
    
- format-independent representation
    
- a clear boundary between human and machine
    
- a thin and stable API
    

I didn’t invent anything.  
What already existed in the company’s system architecture simply took on a different shape  
as it passed between Excel and AutoCAD.

Meaning did not live inside either tool.  
It appeared in the boundary between them.

---

## 7. Small Structures Endure

Sustainable engineering does not begin with a large platform.  
It begins with small structures that do not break.

A single folder,  
one Excel file,  
a few dozen blocks.

Even that is enough to support one person,  
to stabilize a workflow,  
and to give shape to structures that were hard to see before.

Meaning does not reside inside the tools.  
It emerges in the space _between_ them.
