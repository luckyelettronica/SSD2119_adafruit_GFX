# SSD2119 Driver for Adafruit GFX
## History
This is the result of enforced idleness during the Covid-19 lockdown. I have a 3.5" TFT display never used because I didn't know what IC it was based on no software to drive it. 
Eventually  via the site https://www.alibaba.com/product-detail/3-5-TFT-LCD-Module-Display_1976721279.html I discovered that it was an SSD2119 but that didn't help as I couldn't find an Arduino library.
Later I came upon https://github.com/TheFax/SSD2119-library which contains all the source needed to drive the TFT but it isn't really a library, rather a flat Arduino sketch.
## How I did it
### What I added
Adafuit GFX has all the drawing primitives I need so seemed the obvious partner. All one has to do is provide at least one method, drawPixel. All the rest falls into place.
While that provides basic functionality it can be painfully slow. There are other GFX methods that may be overridden for better performance. So far I have implemented drawFastHLine which also helped me to implement fillScreen, fillRect and drawRect.
### What I took away
All drawing primitives and font information. These are now provided by GFX
### What I changed
The C style code was repackaged as a C++ class.<p>
Only color mode RGB565 is supported. That is what GFX uses and what the SSD2119 provides.<p>
It is no longer necessary to specify the target architecture which is now recognised at compile time.<p>
For the Due platform extended SPI is compiled even though Arduino forums advise against it. I measured a small performance benefit.
## TBD
Implement GFX methods setRotation and drawFastVLine.<p>
This is still a work in progress and I have yet to develop better optimisation.<p>
Investigate other devices on board.
## Pin Confusion
One of the hardest problems I had was understanding the labels on the pins on the TFT board, a source of much confusion.<p>
RS   a.k.a. Register Select (Data/Command) a.k.a. DC<p>
SCL  a.k.a. SPI clock a.k.a. SCLK  NOTE: This does NOT refer to I2C SCL<p>
SDA  a.k.a  SPI Master to Slave a.k.a. MOSI  NOTE: This does NOT refer to I2C SDA<p>
I assume the pins marked SCLK, MOSI, MISO are for the other SPI devices on board, SD card, Touch Screen and DataFlash.
  
