## Nomad (GameTek) file format research

### 3D models (.BIN)

The three sections of the .BIN files are:

* Polygon count (one 16-bit word)
* Polygon definitions, each one containing:
    * Coordinates of a point to define a normal vector (three signed 16-bit words)
    * Two words who purpose is currently unknown
    * Vertex count
    * IDs of vertices
* Vertex definitions (three signed 16-bit words for each)

#### Example: MISSILE3.BIN

```
0C 00 - polygon count

polygons:
normal coords?                      vertices  color?  vertex IDs
01 00  02 00  FE FF   FF FF  17 00  03        05      00 00  01 00  02 00
FF FF  00 00  06 00   FF FF  31 00  04        05      03 00  04 00  05 00  06 00
01 00  00 00  FE FF   FF FF  4B 00  04        05      07 00  00 00  02 00  08 00
FF FF  FA FF  06 00   FF FF  63 00  03        05      06 00  05 00  09 00
01 00  FE FF  FE FF   FF FF  7B 00  03        05      09 00  07 00  08 00
FF FF  06 00  06 00   FF FF  93 00  03        05      04 00  03 00  01 00
01 00  02 00  02 00   FF FF  AB 00  03        05      00 00  04 00  01 00
FF FF  FA FF  FA FF   FF FF  C3 00  03        05      06 00  09 00  08 00
01 00  FE FF  02 00   FF FF  DB 00  03        05      05 00  07 00  09 00
FF FF  00 00  FA FF   FF FF  F5 00  04        05      03 00  02 00  08 00  06 00
01 00  00 00  02 00   FF FF  0F 01  04        05      05 00  04 00  00 00  07 00
FF FF  06 00  FA FF   FF FF  FF FF  03        05      01 00  03 00  02 00

0A 00 - vertex count
14 00  05 00  00 00     20, 5, 0
0A 00  0A 00  00 00     10,10, 0
0A 00  05 00  FB FF     10, 5, -5
EC FF  05 00  00 00     -4, 5, 0
0A 00  05 00  05 00     10, 5, 5
0A 00  FB FF  05 00     10,-5, 5
EC FF  FB FF  00 00     -4,-5, 0
14 00  FB FF  00 00     20,-5, 0
0A 00  FB FF  FB FF     10,-5,-5
0A 00  F6 FF  00 00     10,-10,0
```

Color group is given as a 0-based index into an array of eight base colors. Each group contains eight tints/shades of the base, used by the 3D engine to draw highlights and shadows on the 3D objects as they move through space. The 64 total colors used for rendering 3D objects are loaded from SHIP.PAL into the VGA at starting at palette index 0xC0.

| Group index | Color   |
|-------------|---------|
| 0           | Dk gray |
| 1           | Blue    |
| 2           | Green   |
| 3           | Cyan    |
| 4           | Red     |
| 5           | Magenta |
| 6           | Yellow  |
| 7           | Lt gray |
