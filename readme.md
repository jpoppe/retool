# Retool
Strips [Redump](http://redump.org/) dats to only include English titles from
all regions, with no dupes. US titles are preferenced. This is not an
official Redump project.

## Installation
_Retool_ requires [Python 3](https://www.python.org/) with `pip`.

You'll need to install dependencies with `pip` before using _Retool_. To do so,
open Terminal, Command Prompt, or whatever the CLI is on your system, and type:

```python
pip install bs4
pip install lxml
```

## Usage
`python retool.py -i input.dat -o output.dat <options>`

## Options
* `-a` Remove applications
* `-d` Remove demos and coverdiscs
* `-e` Remove educational
* `-m` Remove multimedia
* `-p` Remove betas and prototypes
* `-ra` Split into regions, all languages (not checked for dupes)
* `-re` Split into regions, English only

## How it works
The input dat is split into regions, then each region is processed in a
specific order. Each region cannot include titles that are in the regions
that precede it. The USA version of a title is considered canonical.

Regions are parsed in the following order:

1. USA
2. World
3. UK
4. Canada
5. Australia
6. New Zealand
7. Ireland
8. Brazil
9. Latin America
10. Europe
11. Asia
12. Scandinavia
13. Japan
14. Austria
15. Belgium
16. China
17. Croatia
18. Denmark
19. Finland
20. France
21. Germany
22. Greece
23. India
24. Israel
25. Italy
26. Korea
27. Netherlands
28. Norway
29. Poland
30. Portugal
31. Russia
32. South Africa
33. Spain
34. Sweden
35. Switzerland
36. Taiwan
37. No region

As the program progresses through the regions, `_regional_renames.py` is
referenced to check if any titles in the current region are the same as
another region's title, but with a different name. For example, apart from the
name, **_Dancing Stage Unleashed 3 (Europe)_** and
**_Dance Dance Revolution Ultramix 3 (USA)_** are the same title, and so
**_Dancing Stage Unleashed 3 (Europe)_** would not be included.

## Known limitations
Be aware of the following limitations when using _Retool_. These may or may not be addressed in the future.

#### Doesn't remove older versions of titles
For example, **_Halo - Combat Evolved (USA)_**,
**_Halo - Combat Evolved (USA) (Rev 1)_** and
**_Halo - Combat Evolved (USA) (Rev 2)_** will all be included.

#### Doesn't remove single titles in favor of compilation titles
For example, **_Assassin's Creed - Ezio Trilogy_** does not supersede
**_Assassin's Creed II_**, **_Assassin's Creed - Brotherhood_**, and
**_Assassin's Creed - Revelations_**.

#### Doesn't remove different language versions from the same region
For example, **_Suffering, The - Ties That Bind (Europe) (En,Es,It)_** and
**_Suffering, The - Ties That Bind (Europe) (En,Fr)_**.

#### Can't preference a non-US title over a US title, when the non-US title is arguably superior
For example, **_Fahrenheit (Europe) (En,Fr,De,Es,It)_** versus **_Indigo Prophecy (USA)_**,
where the latter is censored.

#### Can only follow Redump language tags for non-English countries
If Redump missed tagging titles from regions where English isn't their first language (for example, Japan),
those titles won't be included.

#### Will remove titles that have the same name in different regions, even if those titles have different content
For example, versions of singing titles that have additional local tracks.