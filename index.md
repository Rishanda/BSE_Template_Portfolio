# Project Name/Title Goes Here
The Arduino Endless runner 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Rishanda A | Uncommon prep highschool  | Engineering | Incoming Sophomore 

![Headstone Image](https://user-images.githubusercontent.com/86113342/124282836-426c6f00-db19-11eb-8c5b-2a702ca487bd.jpg)

<pre>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">LiquidCrystal</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>

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

<b><font color="#d35400">LiquidCrystal</font></b> <font color="#000000">lcd</font><font color="#000000">(</font><font color="#000000">11</font><font color="#434f54">,</font> <font color="#000000">9</font><font color="#434f54">,</font> <font color="#000000">6</font><font color="#434f54">,</font> <font color="#000000">5</font><font color="#434f54">,</font> <font color="#000000">4</font><font color="#434f54">,</font> <font color="#000000">3</font><font color="#000000">)</font><font color="#000000">;</font>
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
&#09; &nbsp;<font color="#000000">lcd</font><font color="#434f54">.</font><font color="#d35400">createChar</font><font color="#000000">(</font><font color="#000000">i</font> <font color="#434f54">+</font> <font color="#000000">1</font><font color="#434f54">,</font> <font color="#434f54">&amp;</font><font color="#000000">graphics</font><font color="#000000">[</font><font color="#000000">i</font> <font color="#434f54">*</font> <font color="#000000">8</font><font color="#000000">]</font><font color="#000000">)</font><font color="#000000">;</font>
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

<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_READWRITE</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_READWRITE</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_CONTRAST</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_CONTRAST</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_BUTTON</font><font color="#434f54">,</font> <font color="#00979c">INPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_BUTTON</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PIN_AUTOPLAY</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">PIN_AUTOPLAY</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;
 &nbsp;<font color="#434f54">&#47;&#47; Digital pin 2 maps to interrupt 0</font>
 &nbsp;<font color="#d35400">attachInterrupt</font><font color="#000000">(</font><font color="#000000">0</font><font color="#95a5a6">&#47;*PIN_BUTTON*&#47;</font><font color="#434f54">,</font> <font color="#000000">buttonPush</font><font color="#434f54">,</font> <font color="#00979c">FALLING</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;
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
 &nbsp;&nbsp;&nbsp;<font color="#000000">playing</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; The hero collided with something. Too bad.</font>
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
  
# Final Milestone
My final milestone is to add sound to the game so everytime it jump it makes a sound making it something like Mario . 

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612573869/video_to_markdown/images/youtube--F7M7imOVGug-c05b58ac6eb4c4700831b2b3070cd403.jpg )](https://www.youtube.com/watch?v=F7M7imOVGug&feature=emb_logo "Final Milestone")

# Second Milestone
My second milestone was to turn on the blacklight with the uses of the wiring I had learnt in my first milestone. This was kind of contradicting because what I had learnt in the first milestrone was not working so had to had to change the wiring.

[![Third Milestone] [![Endless runner p2](https://res.cloudinary.com/marcomontalbano/image/upload/v1625233285/video_to_markdown/images/youtube--psbLhpZYQrA-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/psbLhpZYQrA "Endless runner p2")
# First Milestone
  

My first milestone was setting up the wires on the board and on the uno circuit. When I soldiered the jumper wires I had some diffculty getting it to work, it kept flashing.In the end I had to blacklight.

[![First Milestone][![Endless runner ](https://res.cloudinary.com/marcomontalbano/image/upload/v1624627882/video_to_markdown/images/youtube--uayA6_YEgs4-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/uayA6_YEgs4 "Endless runner ")
