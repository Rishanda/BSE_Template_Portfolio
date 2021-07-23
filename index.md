# The Arduino Endless runner 


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Rishanda A | Uncommon prep highschool  | Engineering | Incoming Sophomore 

![Screenshot (4)](https://user-images.githubusercontent.com/86113342/125964313-cc148575-bbb6-40a7-8108-a31bc2ad6969.png)

# Code
<pre>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">Wire</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font> 
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">LiquidCrystal_I2C</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>

<font color="#434f54">&#47;&#47;LiquidCrystal_I2C lcd(0x27,20,4); &nbsp;&#47;&#47; set the LCD address to 0x27 for a 16 chars and 2 line display</font>

<font color="#5e6d03">#include</font> <font color="#005c5f">&#34;pitches.h&#34;</font>
<font color="#5e6d03">#define</font> <font color="#000000">PIN_BUTTON</font> <font color="#000000">2</font>
<font color="#5e6d03">#define</font> <font color="#000000">PIN_AUTOPLAY</font> <font color="#000000">1</font>
<font color="#5e6d03">#define</font> <font color="#000000">PIN_READWRITE</font> <font color="#000000">10</font>
<font color="#5e6d03">#define</font> <font color="#000000">PIN_CONTRAST</font> <font color="#000000">12</font>

<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_RUN1</font> <font color="#000000">1</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_RUN2</font> <font color="#000000">2</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_JUMP</font> <font color="#000000">3</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_JUMP_UPPER</font> <font color="#00979c">&#39;.&#39;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Use the &#39;.&#39; character for the head</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_JUMP_LOWER</font> <font color="#000000">4</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font> <font color="#00979c">&#39; &#39;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; User the &#39; &#39; character</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_TERRAIN_SOLID</font> <font color="#000000">5</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_TERRAIN_SOLID_RIGHT</font> <font color="#000000">6</font>
<font color="#5e6d03">#define</font> <font color="#000000">SPRITE_TERRAIN_SOLID_LEFT</font> <font color="#000000">7</font>

<font color="#5e6d03">#define</font> <font color="#000000">HERO_HORIZONTAL_POSITION</font> <font color="#000000">1</font> &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Horizontal position of hero on screen</font>

<font color="#5e6d03">#define</font> <font color="#000000">TERRAIN_WIDTH</font> <font color="#000000">16</font>
<font color="#5e6d03">#define</font> <font color="#000000">TERRAIN_EMPTY</font> <font color="#000000">0</font>
<font color="#5e6d03">#define</font> <font color="#000000">TERRAIN_LOWER_BLOCK</font> <font color="#000000">1</font>
<font color="#5e6d03">#define</font> <font color="#000000">TERRAIN_UPPER_BLOCK</font> <font color="#000000">2</font>

<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_OFF</font> <font color="#000000">0</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Hero is invisible</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_RUN_LOWER_1</font> <font color="#000000">1</font> &nbsp;<font color="#434f54">&#47;&#47; Hero is running on lower row (pose 1)</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_RUN_LOWER_2</font> <font color="#000000">2</font> &nbsp;<font color="#434f54">&#47;&#47; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(pose 2)</font>

<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_1</font> <font color="#000000">3</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Starting a jump</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_2</font> <font color="#000000">4</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Half-way up</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_3</font> <font color="#000000">5</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Jump is on upper row</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_4</font> <font color="#000000">6</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Jump is on upper row</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_5</font> <font color="#000000">7</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Jump is on upper row</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_6</font> <font color="#000000">8</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Jump is on upper row</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_7</font> <font color="#000000">9</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Half-way down</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_JUMP_8</font> <font color="#000000">10</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; About to land</font>

<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_RUN_UPPER_1</font> <font color="#000000">11</font> <font color="#434f54">&#47;&#47; Hero is running on upper row (pose 1)</font>
<font color="#5e6d03">#define</font> <font color="#000000">HERO_POSITION_RUN_UPPER_2</font> <font color="#000000">12</font> <font color="#434f54">&#47;&#47; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(pose 2)</font>

 <b><font color="#d35400">LiquidCrystal_I2C</font></b> <font color="#000000">lcd</font><font color="#000000">(</font><font color="#000000">0x27</font><font color="#434f54">,</font><font color="#000000">20</font><font color="#434f54">,</font><font color="#000000">4</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47; set the LCD address to 0x27 for a 16 chars and 2 line display</font>

<font color="#00979c">static</font> <font color="#00979c">char</font> <font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">TERRAIN_WIDTH</font> <font color="#434f54">+</font> <font color="#000000">1</font><font color="#000000">]</font><font color="#000000">;</font>
<font color="#00979c">static</font> <font color="#00979c">char</font> <font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">TERRAIN_WIDTH</font> <font color="#434f54">+</font> <font color="#000000">1</font><font color="#000000">]</font><font color="#000000">;</font>
<font color="#00979c">static</font> <font color="#00979c">bool</font> <font color="#000000">buttonPushed</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>

<font color="#00979c">void</font> <font color="#000000">initializeGraphics</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;<font color="#00979c">static</font> <font color="#00979c">byte</font> <font color="#000000">graphics</font><font color="#000000">[</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Run position 1</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01110</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11010</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B10011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Run position 2</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01110</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Jump</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01100</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11110</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01101</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B10000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Jump lower</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11110</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B01101</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B10000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Ground</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11111</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Ground right</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B00011</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Ground left</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">B11000</font><font color="#434f54">,</font>
 &nbsp;<font color="#000000">}</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">int</font> <font color="#000000">i</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47; Skip using character 0, this allows lcd.print() to be used to</font>
 &nbsp;<font color="#434f54">&#47;&#47; quickly draw multiple characters</font>
 &nbsp;<font color="#5e6d03">for</font> <font color="#000000">(</font><font color="#000000">i</font> <font color="#434f54">=</font> <font color="#000000">0</font><font color="#000000">;</font> <font color="#000000">i</font> <font color="#434f54">&lt;</font> <font color="#000000">7</font><font color="#000000">;</font> <font color="#434f54">++</font><font color="#000000">i</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">createChar</font><font color="#000000">(</font><font color="#000000">i</font> <font color="#434f54">+</font> <font color="#000000">1</font><font color="#434f54">,</font> <font color="#434f54">&amp;</font><font color="#000000">graphics</font><font color="#000000">[</font><font color="#000000">i</font> <font color="#434f54">*</font> <font color="#000000">8</font><font color="#000000">]</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#5e6d03">for</font> <font color="#000000">(</font><font color="#000000">i</font> <font color="#434f54">=</font> <font color="#000000">0</font><font color="#000000">;</font> <font color="#000000">i</font> <font color="#434f54">&lt;</font> <font color="#000000">TERRAIN_WIDTH</font><font color="#000000">;</font> <font color="#434f54">++</font><font color="#000000">i</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">i</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">i</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
<font color="#000000">}</font>

<font color="#434f54">&#47;&#47; Slide the terrain to the left in half-character increments</font>
<font color="#434f54">&#47;&#47;</font>
<font color="#00979c">void</font> <font color="#000000">advanceTerrain</font><font color="#000000">(</font><font color="#00979c">char</font><font color="#434f54">*</font> <font color="#000000">terrain</font><font color="#434f54">,</font> <font color="#00979c">byte</font> <font color="#000000">newTerrain</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;<font color="#5e6d03">for</font> <font color="#000000">(</font><font color="#00979c">int</font> <font color="#000000">i</font> <font color="#434f54">=</font> <font color="#000000">0</font><font color="#000000">;</font> <font color="#000000">i</font> <font color="#434f54">&lt;</font> <font color="#000000">TERRAIN_WIDTH</font><font color="#000000">;</font> <font color="#434f54">++</font><font color="#000000">i</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#00979c">char</font> <font color="#000000">current</font> <font color="#434f54">=</font> <font color="#000000">terrain</font><font color="#000000">[</font><font color="#000000">i</font><font color="#000000">]</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#00979c">char</font> <font color="#000000">next</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#000000">i</font> <font color="#434f54">==</font> <font color="#000000">TERRAIN_WIDTH</font><font color="#434f54">-</font><font color="#000000">1</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">newTerrain</font> <font color="#434f54">:</font> <font color="#000000">terrain</font><font color="#000000">[</font><font color="#000000">i</font><font color="#434f54">+</font><font color="#000000">1</font><font color="#000000">]</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">switch</font> <font color="#000000">(</font><font color="#000000">current</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">terrain</font><font color="#000000">[</font><font color="#000000">i</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#000000">next</font> <font color="#434f54">==</font> <font color="#000000">SPRITE_TERRAIN_SOLID</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">SPRITE_TERRAIN_SOLID_RIGHT</font> <font color="#434f54">:</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">SPRITE_TERRAIN_SOLID</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">terrain</font><font color="#000000">[</font><font color="#000000">i</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#000000">next</font> <font color="#434f54">==</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">SPRITE_TERRAIN_SOLID_LEFT</font> <font color="#434f54">:</font> <font color="#000000">SPRITE_TERRAIN_SOLID</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">SPRITE_TERRAIN_SOLID_RIGHT</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">terrain</font><font color="#000000">[</font><font color="#000000">i</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_SOLID</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">SPRITE_TERRAIN_SOLID_LEFT</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">terrain</font><font color="#000000">[</font><font color="#000000">i</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#000000">}</font>
<font color="#000000">}</font>

<font color="#00979c">bool</font> <font color="#000000">drawHero</font><font color="#000000">(</font><font color="#00979c">byte</font> <font color="#d35400">position</font><font color="#434f54">,</font> <font color="#00979c">char</font><font color="#434f54">*</font> <font color="#000000">terrainUpper</font><font color="#434f54">,</font> <font color="#00979c">char</font><font color="#434f54">*</font> <font color="#000000">terrainLower</font><font color="#434f54">,</font> <font color="#00979c">unsigned</font> <font color="#00979c">int</font> <font color="#000000">score</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<font color="#00979c">bool</font> <font color="#000000">collide</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">char</font> <font color="#000000">upperSave</font> <font color="#434f54">=</font> <font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">char</font> <font color="#000000">lowerSave</font> <font color="#434f54">=</font> <font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">byte</font> <font color="#000000">upper</font><font color="#434f54">,</font> <font color="#000000">lower</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">switch</font> <font color="#000000">(</font><font color="#d35400">position</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_OFF</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_RUN_LOWER_1</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_RUN1</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_RUN_LOWER_2</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_RUN2</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_1</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_8</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_JUMP</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_2</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_7</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_JUMP_UPPER</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_JUMP_LOWER</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_3</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_4</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_5</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_JUMP_6</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_JUMP</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_RUN_UPPER_1</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_RUN1</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">case</font> <font color="#000000">HERO_POSITION_RUN_UPPER_2</font><font color="#434f54">:</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">upper</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_RUN2</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lower</font> <font color="#434f54">=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">upper</font> <font color="#434f54">!=</font> <font color="#00979c">&#39; &#39;</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">upper</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">collide</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#000000">upperSave</font> <font color="#434f54">==</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#00979c">false</font> <font color="#434f54">:</font> <font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">lower</font> <font color="#434f54">!=</font> <font color="#00979c">&#39; &#39;</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">lower</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">collide</font> <font color="#434f54">|=</font> <font color="#000000">(</font><font color="#000000">lowerSave</font> <font color="#434f54">==</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#00979c">false</font> <font color="#434f54">:</font> <font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;
 &nbsp;<font color="#00979c">byte</font> <font color="#000000">digits</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#000000">score</font> <font color="#434f54">&gt;</font> <font color="#000000">9999</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">5</font> <font color="#434f54">:</font> <font color="#000000">(</font><font color="#000000">score</font> <font color="#434f54">&gt;</font> <font color="#000000">999</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">4</font> <font color="#434f54">:</font> <font color="#000000">(</font><font color="#000000">score</font> <font color="#434f54">&gt;</font> <font color="#000000">99</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">3</font> <font color="#434f54">:</font> <font color="#000000">(</font><font color="#000000">score</font> <font color="#434f54">&gt;</font> <font color="#000000">9</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">2</font> <font color="#434f54">:</font> <font color="#000000">1</font><font color="#000000">;</font>
 &nbsp;
 &nbsp;<font color="#434f54">&#47;&#47; Draw the scene</font>
 &nbsp;<font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">TERRAIN_WIDTH</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#00979c">&#39;\0&#39;</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">TERRAIN_WIDTH</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#00979c">&#39;\0&#39;</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">char</font> <font color="#000000">temp</font> <font color="#434f54">=</font> <font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">16</font><font color="#434f54">-</font><font color="#000000">digits</font><font color="#000000">]</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">16</font><font color="#434f54">-</font><font color="#000000">digits</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#00979c">&#39;\0&#39;</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">terrainUpper</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">16</font><font color="#434f54">-</font><font color="#000000">digits</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">temp</font><font color="#000000">;</font> &nbsp;
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font><font color="#000000">1</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">terrainLower</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">16</font> <font color="#434f54">-</font> <font color="#000000">digits</font><font color="#434f54">,</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">score</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;<font color="#000000">terrainUpper</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">upperSave</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">lowerSave</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">return</font> <font color="#000000">collide</font><font color="#000000">;</font>
<font color="#000000">}</font>

<font color="#434f54">&#47;&#47; Handle the button push as an interrupt</font>
<font color="#00979c">void</font> <font color="#000000">buttonPush</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<font color="#000000">buttonPushed</font> <font color="#434f54">=</font> <font color="#00979c">true</font><font color="#000000">;</font>
<font color="#000000">}</font>

<font color="#434f54">&#47;&#47; notes in the melody:</font>
<font color="#00979c">int</font> <font color="#000000">melody</font><font color="#000000">[</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">{</font>

 &nbsp;<font color="#000000">NOTE_C4</font><font color="#434f54">,</font> <font color="#000000">NOTE_G3</font><font color="#434f54">,</font> <font color="#000000">NOTE_G3</font><font color="#434f54">,</font> <font color="#000000">NOTE_A3</font><font color="#434f54">,</font> <font color="#000000">NOTE_G3</font><font color="#434f54">,</font> <font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">NOTE_B3</font><font color="#434f54">,</font> <font color="#000000">NOTE_C4</font>
<font color="#000000">}</font><font color="#000000">;</font>

<font color="#434f54">&#47;&#47; note durations: 4 = quarter note, 8 = eighth note, etc.:</font>
<font color="#00979c">int</font> <font color="#000000">noteDurations</font><font color="#000000">[</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">{</font>
 &nbsp;<font color="#000000">4</font><font color="#434f54">,</font> <font color="#000000">8</font><font color="#434f54">,</font> <font color="#000000">8</font><font color="#434f54">,</font> <font color="#000000">4</font><font color="#434f54">,</font> <font color="#000000">4</font><font color="#434f54">,</font> <font color="#000000">4</font><font color="#434f54">,</font> <font color="#000000">4</font><font color="#434f54">,</font> <font color="#000000">4</font>
<font color="#000000">}</font><font color="#000000">;</font>
<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;<font color="#434f54">&#47;&#47;lcd.init(); &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#47;&#47; initialize the lcd </font>
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">init</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">backlight</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_READWRITE</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_READWRITE</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_CONTRAST</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_CONTRAST</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_BUTTON</font><font color="#434f54">,</font> <font color="#00979c">INPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_BUTTON</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_AUTOPLAY</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_AUTOPLAY</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">7</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47; Digital pin 2 maps to interrupt 0</font>
 &nbsp;<font color="#d35400">attachInterrupt</font><font color="#000000">(</font><font color="#000000">0</font><font color="#95a5a6">&#47;*PIN_BUTTON*&#47;</font><font color="#434f54">,</font> <font color="#000000">buttonPush</font><font color="#434f54">,</font> <font color="#00979c">FALLING</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47; iterate over the notes of the melody:</font>

 &nbsp;<font color="#000000">initializeGraphics</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;
 &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">16</font><font color="#434f54">,</font> <font color="#000000">2</font><font color="#000000">)</font><font color="#000000">;</font>
<font color="#000000">}</font>

<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;<font color="#00979c">static</font> <font color="#00979c">byte</font> <font color="#000000">heroPos</font> <font color="#434f54">=</font> <font color="#000000">HERO_POSITION_RUN_LOWER_1</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">static</font> <font color="#00979c">byte</font> <font color="#000000">newTerrainType</font> <font color="#434f54">=</font> <font color="#000000">TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">static</font> <font color="#00979c">byte</font> <font color="#000000">newTerrainDuration</font> <font color="#434f54">=</font> <font color="#000000">1</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">static</font> <font color="#00979c">bool</font> <font color="#000000">playing</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">static</font> <font color="#00979c">bool</font> <font color="#d35400">blink</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">static</font> <font color="#00979c">unsigned</font> <font color="#00979c">int</font> <font color="#000000">distance</font> <font color="#434f54">=</font> <font color="#000000">0</font><font color="#000000">;</font>
 &nbsp;
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#434f54">!</font><font color="#000000">playing</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">drawHero</font><font color="#000000">(</font><font color="#000000">(</font><font color="#d35400">blink</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">HERO_POSITION_OFF</font> <font color="#434f54">:</font> <font color="#000000">heroPos</font><font color="#434f54">,</font> <font color="#000000">terrainUpper</font><font color="#434f54">,</font> <font color="#000000">terrainLower</font><font color="#434f54">,</font> <font color="#000000">distance</font> <font color="#434f54">&gt;&gt;</font> <font color="#000000">3</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">blink</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Press Start&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">250</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">blink</font> <font color="#434f54">=</font> <font color="#434f54">!</font><font color="#d35400">blink</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">buttonPushed</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">initializeGraphics</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">heroPos</font> <font color="#434f54">=</font> <font color="#000000">HERO_POSITION_RUN_LOWER_1</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">playing</font> <font color="#434f54">=</font> <font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">buttonPushed</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">distance</font> <font color="#434f54">=</font> <font color="#000000">0</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">return</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>

 &nbsp;<font color="#434f54">&#47;&#47; Shift the terrain to the left</font>
 &nbsp;<font color="#000000">advanceTerrain</font><font color="#000000">(</font><font color="#000000">terrainLower</font><font color="#434f54">,</font> <font color="#000000">newTerrainType</font> <font color="#434f54">==</font> <font color="#000000">TERRAIN_LOWER_BLOCK</font> <font color="#434f54">?</font> <font color="#000000">SPRITE_TERRAIN_SOLID</font> <font color="#434f54">:</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">advanceTerrain</font><font color="#000000">(</font><font color="#000000">terrainUpper</font><font color="#434f54">,</font> <font color="#000000">newTerrainType</font> <font color="#434f54">==</font> <font color="#000000">TERRAIN_UPPER_BLOCK</font> <font color="#434f54">?</font> <font color="#000000">SPRITE_TERRAIN_SOLID</font> <font color="#434f54">:</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;
 &nbsp;<font color="#434f54">&#47;&#47; Make new terrain to enter on the right</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#434f54">--</font><font color="#000000">newTerrainDuration</font> <font color="#434f54">==</font> <font color="#000000">0</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">newTerrainType</font> <font color="#434f54">==</font> <font color="#000000">TERRAIN_EMPTY</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">newTerrainType</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#d35400">random</font><font color="#000000">(</font><font color="#000000">3</font><font color="#000000">)</font> <font color="#434f54">==</font> <font color="#000000">0</font><font color="#000000">)</font> <font color="#434f54">?</font> <font color="#000000">TERRAIN_UPPER_BLOCK</font> <font color="#434f54">:</font> <font color="#000000">TERRAIN_LOWER_BLOCK</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">newTerrainDuration</font> <font color="#434f54">=</font> <font color="#000000">2</font> <font color="#434f54">+</font> <font color="#d35400">random</font><font color="#000000">(</font><font color="#000000">10</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">newTerrainType</font> <font color="#434f54">=</font> <font color="#000000">TERRAIN_EMPTY</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">newTerrainDuration</font> <font color="#434f54">=</font> <font color="#000000">10</font> <font color="#434f54">+</font> <font color="#d35400">random</font><font color="#000000">(</font><font color="#000000">10</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">buttonPushed</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">heroPos</font> <font color="#434f54">&lt;=</font> <font color="#000000">HERO_POSITION_RUN_LOWER_2</font><font color="#000000">)</font> <font color="#000000">heroPos</font> <font color="#434f54">=</font> <font color="#000000">HERO_POSITION_JUMP_1</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">buttonPushed</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font> &nbsp;

 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">drawHero</font><font color="#000000">(</font><font color="#000000">heroPos</font><font color="#434f54">,</font> <font color="#000000">terrainUpper</font><font color="#434f54">,</font> <font color="#000000">terrainLower</font><font color="#434f54">,</font> <font color="#000000">distance</font> <font color="#434f54">&gt;&gt;</font> <font color="#000000">3</font><font color="#000000">)</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">playing</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font><font color="#5e6d03">for</font> <font color="#000000">(</font><font color="#00979c">int</font> <font color="#000000">thisNote</font> <font color="#434f54">=</font> <font color="#000000">0</font><font color="#000000">;</font> <font color="#000000">thisNote</font> <font color="#434f54">&lt;</font> <font color="#000000">8</font><font color="#000000">;</font> <font color="#000000">thisNote</font><font color="#434f54">++</font><font color="#000000">)</font> <font color="#000000">{</font>

 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; to calculate the note duration, take one second divided by the note type.</font>

 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;e.g. quarter note = 1000 &#47; 4, eighth note = 1000&#47;8, etc.</font>

 &nbsp;&nbsp;&nbsp;<font color="#00979c">int</font> <font color="#000000">noteDuration</font> <font color="#434f54">=</font> <font color="#000000">1000</font> <font color="#434f54">&#47;</font> <font color="#000000">noteDurations</font><font color="#000000">[</font><font color="#000000">thisNote</font><font color="#000000">]</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<font color="#d35400">tone</font><font color="#000000">(</font><font color="#000000">8</font><font color="#434f54">,</font> <font color="#000000">melody</font><font color="#000000">[</font><font color="#000000">thisNote</font><font color="#000000">]</font><font color="#434f54">,</font> <font color="#000000">noteDuration</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; to distinguish the notes, set a minimum time between them.</font>

 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; the note&#39;s duration + 30% seems to work well:</font>

 &nbsp;&nbsp;&nbsp;<font color="#00979c">int</font> <font color="#000000">pauseBetweenNotes</font> <font color="#434f54">=</font> <font color="#000000">noteDuration</font> <font color="#434f54">*</font> <font color="#000000">1.30</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">pauseBetweenNotes</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; stop the tone playing:</font>

 &nbsp;&nbsp;&nbsp;<font color="#d35400">noTone</font><font color="#000000">(</font><font color="#000000">8</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;<font color="#000000">}</font> <font color="#434f54">&#47;&#47; The hero collided with something. Too bad.</font>
 &nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">heroPos</font> <font color="#434f54">==</font> <font color="#000000">HERO_POSITION_RUN_LOWER_2</font> <font color="#434f54">||</font> <font color="#000000">heroPos</font> <font color="#434f54">==</font> <font color="#000000">HERO_POSITION_JUMP_8</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">heroPos</font> <font color="#434f54">=</font> <font color="#000000">HERO_POSITION_RUN_LOWER_1</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">(</font><font color="#000000">heroPos</font> <font color="#434f54">&gt;=</font> <font color="#000000">HERO_POSITION_JUMP_3</font> <font color="#434f54">&amp;&amp;</font> <font color="#000000">heroPos</font> <font color="#434f54">&lt;=</font> <font color="#000000">HERO_POSITION_JUMP_5</font><font color="#000000">)</font> <font color="#434f54">&amp;&amp;</font> <font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font> <font color="#434f54">!=</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">heroPos</font> <font color="#434f54">=</font> <font color="#000000">HERO_POSITION_RUN_UPPER_1</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">heroPos</font> <font color="#434f54">&gt;=</font> <font color="#000000">HERO_POSITION_RUN_UPPER_1</font> <font color="#434f54">&amp;&amp;</font> <font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font><font color="#000000">]</font> <font color="#434f54">==</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">heroPos</font> <font color="#434f54">=</font> <font color="#000000">HERO_POSITION_JUMP_5</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">heroPos</font> <font color="#434f54">==</font> <font color="#000000">HERO_POSITION_RUN_UPPER_2</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">heroPos</font> <font color="#434f54">=</font> <font color="#000000">HERO_POSITION_RUN_UPPER_1</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">++</font><font color="#000000">heroPos</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">++</font><font color="#000000">distance</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;
 &nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_AUTOPLAY</font><font color="#434f54">,</font> <font color="#000000">terrainLower</font><font color="#000000">[</font><font color="#000000">HERO_HORIZONTAL_POSITION</font> <font color="#434f54">+</font> <font color="#000000">2</font><font color="#000000">]</font> <font color="#434f54">==</font> <font color="#000000">SPRITE_TERRAIN_EMPTY</font> <font color="#434f54">?</font> <font color="#00979c">HIGH</font> <font color="#434f54">:</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">100</font><font color="#000000">)</font><font color="#000000">;</font>
<font color="#000000">}</font>
</pre>
code pitch.h 
<pre>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B0</font> &nbsp;<font color="#000000">31</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C1</font> &nbsp;<font color="#000000">33</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS1</font> <font color="#000000">35</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D1</font> &nbsp;<font color="#000000">37</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS1</font> <font color="#000000">39</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_E1</font> &nbsp;<font color="#000000">41</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_F1</font> &nbsp;<font color="#000000">44</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_FS1</font> <font color="#000000">46</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_G1</font> &nbsp;<font color="#000000">49</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_GS1</font> <font color="#000000">52</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_A1</font> &nbsp;<font color="#000000">55</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_AS1</font> <font color="#000000">58</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B1</font> &nbsp;<font color="#000000">62</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C2</font> &nbsp;<font color="#000000">65</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS2</font> <font color="#000000">69</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D2</font> &nbsp;<font color="#000000">73</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS2</font> <font color="#000000">78</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_E2</font> &nbsp;<font color="#000000">82</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_F2</font> &nbsp;<font color="#000000">87</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_FS2</font> <font color="#000000">93</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_G2</font> &nbsp;<font color="#000000">98</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_GS2</font> <font color="#000000">104</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_A2</font> &nbsp;<font color="#000000">110</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_AS2</font> <font color="#000000">117</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B2</font> &nbsp;<font color="#000000">123</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C3</font> &nbsp;<font color="#000000">131</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS3</font> <font color="#000000">139</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D3</font> &nbsp;<font color="#000000">147</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS3</font> <font color="#000000">156</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_E3</font> &nbsp;<font color="#000000">165</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_F3</font> &nbsp;<font color="#000000">175</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_FS3</font> <font color="#000000">185</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_G3</font> &nbsp;<font color="#000000">196</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_GS3</font> <font color="#000000">208</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_A3</font> &nbsp;<font color="#000000">220</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_AS3</font> <font color="#000000">233</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B3</font> &nbsp;<font color="#000000">247</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C4</font> &nbsp;<font color="#000000">262</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS4</font> <font color="#000000">277</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D4</font> &nbsp;<font color="#000000">294</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS4</font> <font color="#000000">311</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_E4</font> &nbsp;<font color="#000000">330</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_F4</font> &nbsp;<font color="#000000">349</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_FS4</font> <font color="#000000">370</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_G4</font> &nbsp;<font color="#000000">392</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_GS4</font> <font color="#000000">415</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_A4</font> &nbsp;<font color="#000000">440</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_AS4</font> <font color="#000000">466</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B4</font> &nbsp;<font color="#000000">494</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C5</font> &nbsp;<font color="#000000">523</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS5</font> <font color="#000000">554</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D5</font> &nbsp;<font color="#000000">587</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS5</font> <font color="#000000">622</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_E5</font> &nbsp;<font color="#000000">659</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_F5</font> &nbsp;<font color="#000000">698</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_FS5</font> <font color="#000000">740</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_G5</font> &nbsp;<font color="#000000">784</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_GS5</font> <font color="#000000">831</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_A5</font> &nbsp;<font color="#000000">880</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_AS5</font> <font color="#000000">932</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B5</font> &nbsp;<font color="#000000">988</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C6</font> &nbsp;<font color="#000000">1047</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS6</font> <font color="#000000">1109</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D6</font> &nbsp;<font color="#000000">1175</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS6</font> <font color="#000000">1245</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_E6</font> &nbsp;<font color="#000000">1319</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_F6</font> &nbsp;<font color="#000000">1397</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_FS6</font> <font color="#000000">1480</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_G6</font> &nbsp;<font color="#000000">1568</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_GS6</font> <font color="#000000">1661</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_A6</font> &nbsp;<font color="#000000">1760</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_AS6</font> <font color="#000000">1865</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B6</font> &nbsp;<font color="#000000">1976</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C7</font> &nbsp;<font color="#000000">2093</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS7</font> <font color="#000000">2217</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D7</font> &nbsp;<font color="#000000">2349</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS7</font> <font color="#000000">2489</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_E7</font> &nbsp;<font color="#000000">2637</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_F7</font> &nbsp;<font color="#000000">2794</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_FS7</font> <font color="#000000">2960</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_G7</font> &nbsp;<font color="#000000">3136</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_GS7</font> <font color="#000000">3322</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_A7</font> &nbsp;<font color="#000000">3520</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_AS7</font> <font color="#000000">3729</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_B7</font> &nbsp;<font color="#000000">3951</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_C8</font> &nbsp;<font color="#000000">4186</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_CS8</font> <font color="#000000">4435</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_D8</font> &nbsp;<font color="#000000">4699</font>
<font color="#5e6d03">#define</font> <font color="#000000">NOTE_DS8</font> <font color="#000000">4978</font>

</pre>
# Third Milestone
My final milestone is to add sound to the game so everytime it jump it makes a sound making it something like Mario . 

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612573869/video_to_markdown/images/youtube--F7M7imOVGug-c05b58ac6eb4c4700831b2b3070cd403.jpg )](https://www.youtube.com/watch?v=F7M7imOVGug&feature=emb_logo "Final Milestone")

# Second Milestone
My second milestone was to turn on the blacklight with the uses of the wiring I had learnt in my first milestone. This was kind of contradicting because what I had learnt in the first milestrone was not working so had to had to change the wiring.

[![Third Milestone] [![Endless runner p2](https://res.cloudinary.com/marcomontalbano/image/upload/v1625233285/video_to_markdown/images/youtube--psbLhpZYQrA-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/psbLhpZYQrA "Endless runner p2")
# First Milestone
  

My first milestone was setting up the wires on the board and on the uno circuit. When I soldiered the jumper wires I had some diffculty getting it to work, it kept flashing.In the end I had to blacklight.

[![First Milestone][![Endless runner ](https://res.cloudinary.com/marcomontalbano/image/upload/v1624627882/video_to_markdown/images/youtube--uayA6_YEgs4-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/uayA6_YEgs4 "Endless runner ")
