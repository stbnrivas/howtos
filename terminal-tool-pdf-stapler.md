# pdf-stapler


```bash
pdf-stapler <mode> <page range> output.pdf
```

previous step: convert any amount of png to pdf

```bash
for i in $(seq -w 1 042);do convert $i.png $i.pdf; done
```

## mode: [cat|del|split|zip|info]

Select the given pages/ranges from input files.     No range means all pages.
cat/sel: <inputfile> [<pagerange>] ... (output needed) 

Select all but the given pages/ranges from input files.
del: <inputfile> [<pagerange>[<rotation>]] ... (output needed)

Create one file per page in input pdf files (no output needed)
burst/split: <inputfile> ... (no output needed)

Merge/Collate the given input files interleaved.
zip: <inputfile> [<pagerange>[<rotation>]] ... (output needed)
    
Display PDF metadata
info: <inputfile> ... (no output needed)
    
## page range 

n - single numbers mean single pages (e.g., 15)
n-m - page ranges include the entire specified range (e.g. 1-6)
m-n - negative ranges sort pages backwards (e.g., 6-3)

### Extended page range options:

R +90º
L -90º
D +180º


1-15R	rotate 1-15 page 90 degree
1-15L
1-15D

```bash
for i in $(seq -w 1 042);do echo $i.pdf; done

pdf-stapler cat  001.pdf 002.pdf 003.pdf 004.pdf 005.pdf 006.pdf 007.pdf 008.pdf 009.pdf 010.pdf 011.pdf 012.pdf 013.pdf 014.pdf 015.pdf 016.pdf 017.pdf 018.pdf 019.pdf 020.pdf 021.pdf 022.pdf 023.pdf 024.pdf 025.pdf 026.pdf 027.pdf 028.pdf 029.pdf 030.pdf 031.pdf 032.pdf 033.pdf 034.pdf 035.pdf 036.pdf 037.pdf 038.pdf 039.pdf 040.pdf 041.pdf output.pdf
```