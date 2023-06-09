# Scripts
A dumping ground for misc scripts I am writing to save myself the hassle

## Redump.py
Recursively extracts Redump games into folders labelled with their name, unpacking multi-disc games into a single folder with no disc label.

For Example:
```
/ExampleDir
├── Gran Turismo 2 (USA) (Arcade Mode) (Rev 1).7z
├── Gran Turismo 2 (USA) (Simulation Mode) (Rev 2).7z
├── Klonoa - Door to Phantomile (USA).7z
├── Mega Man X6 (USA) (Rev 1).7z
└── RPGs
    ├── Chrono Cross (USA) (Disc 1).7z
    ├── Chrono Cross (USA) (Disc 2).7z
    ├── Final Fantasy IX (USA) (Disc 1) (Rev 1).7z
    ├── Final Fantasy IX (USA) (Disc 2) (Rev 1).7z
    ├── Final Fantasy IX (USA) (Disc 3) (Rev 1).7z
    └── Final Fantasy IX (USA) (Disc 4) (Rev 1).7z
```

Will Become:
```
/ExampleDir
├── Gran Turismo 2 (USA) (Arcade Mode) (Rev 1)
│   ├── Gran Turismo 2 (USA) (Arcade Mode) (Rev 1).bin
│   └── Gran Turismo 2 (USA) (Arcade Mode) (Rev 1).cue
├── Gran Turismo 2 (USA) (Arcade Mode) (Rev 1).7z
├── Gran Turismo 2 (USA) (Simulation Mode) (Rev 2)
│   ├── Gran Turismo 2 (USA) (Simulation Mode) (Rev 2).bin
│   └── Gran Turismo 2 (USA) (Simulation Mode) (Rev 2).cue
├── Gran Turismo 2 (USA) (Simulation Mode) (Rev 2).7z
├── Klonoa - Door to Phantomile (USA)
│   ├── Klonoa - Door to Phantomile (USA).bin
│   └── Klonoa - Door to Phantomile (USA).cue
├── Klonoa - Door to Phantomile (USA).7z
├── Mega Man X6 (USA) (Rev 1)
│   ├── Mega Man X6 (USA) (Rev 1).bin
│   └── Mega Man X6 (USA) (Rev 1).cue
├── Mega Man X6 (USA) (Rev 1).7z
└── RPGs
    ├── Chrono Cross (USA) 
    │   ├── Chrono Cross (USA) (Disc 1).bin
    │   ├── Chrono Cross (USA) (Disc 1).cue
    │   ├── Chrono Cross (USA) (Disc 2).bin
    │   └── Chrono Cross (USA) (Disc 2).cue
    ├── Chrono Cross (USA) (Disc 1).7z
    ├── Chrono Cross (USA) (Disc 2).7z
    ├── Final Fantasy IX (USA) (Disc 1) (Rev 1).7z
    ├── Final Fantasy IX (USA) (Disc 2) (Rev 1).7z
    ├── Final Fantasy IX (USA) (Disc 3) (Rev 1).7z
    ├── Final Fantasy IX (USA) (Disc 4) (Rev 1).7z
    └── Final Fantasy IX (USA) (Rev 1)
        ├── Final Fantasy IX (USA) (Disc 1) (Rev 1).bin
        ├── Final Fantasy IX (USA) (Disc 1) (Rev 1).cue
        ├── Final Fantasy IX (USA) (Disc 2) (Rev 1).bin
        ├── Final Fantasy IX (USA) (Disc 2) (Rev 1).cue
        ├── Final Fantasy IX (USA) (Disc 3) (Rev 1).bin
        ├── Final Fantasy IX (USA) (Disc 3) (Rev 1).cue
        ├── Final Fantasy IX (USA) (Disc 4) (Rev 1).bin
        └── Final Fantasy IX (USA) (Disc 4) (Rev 1).cue
```

### Usage
`python redump.py /path/to/root [-r]`
Use `-r` to specify recursive extraction, otherwise only files on the root directory will be managed.

### Caveats
* Dependent on `py7zr`
* I am using `os.walk()` to traverse the directories, but it will traverse through the directories that get made in the extracting process. I may or may not fix this later.

## bincue_to_chd
Take a directory of bin/cues and convert them the the MAME CHD format. If they are single-disc games, remove the containing folder as they now exist in only one file.

## Usage
`python bincue_to_chd.py /path/to/root [-r]`
Use `-r` to specify recursive traversal otherwise only files on the root directory will be managed.

### Caveats
* `chdman` must be installed. On Ubuntu/Debian, this is included in the `mame-tools` package.
* Multi-disc games are left in a containing folder, individual disc games have their folders and contents deleted after being made.
* **Be careful** when applying this to a large directory, as it **will** delete the bin/cues when it is finished compressing.
