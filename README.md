<div align="center">

## Blinking Text


</div>

### Description

Very cool Blinking text code. Check it out!
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Mike McNaughton](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/mike-mcnaughton.md)
**Level**          |Beginner
**User Rating**    |4.7 (14 globes from 3 users)
**Compatibility**  |Java \(JDK 1\.2\)
**Category**       |[Graphics](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics__2-75.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/mike-mcnaughton-blinking-text__2-2080/archive/master.zip)





### Source Code

```
*/
import java.awt.*;
import java.util.StringTokenizer;
/**
 * I love blinking things.
 *
 * @author Arthur van Hoff
 * @modified 04/24/96 Jim Hagen use getBackground
 * @modified 02/05/98 Mike McCloskey removed use of deprecated methods
 */
public class Blink extends java.applet.Applet implements Runnable
{
  Thread blinker = null;  // The thread that displays images
  String labelString;    // The label for the window
  int delay;        // the delay time between blinks
  public void init() {
	String blinkFrequency = getParameter("speed");
	delay = (blinkFrequency == null) ? 400 :
      (1000 / Integer.parseInt(blinkFrequency));
	labelString = getParameter("lbl");
	if (labelString == null)
      labelString = "Blink";
    Font font = new java.awt.Font("Serif", Font.PLAIN, 24);
	setFont(font);
  }
  public void paint(Graphics g) {
    int fontSize = g.getFont().getSize();
	int x = 0, y = fontSize, space;
	int red =  (int)( 50 * Math.random());
	int green = (int)( 50 * Math.random());
	int blue = (int)(256 * Math.random());
	Dimension d = getSize();
    g.setColor(Color.black);
	FontMetrics fm = g.getFontMetrics();
	space = fm.stringWidth(" ");
	for (StringTokenizer t = new StringTokenizer(labelString); t.hasMoreTokens();) {
	  String word = t.nextToken();
	  int w = fm.stringWidth(word) + space;
	  if (x + w > d.width) {
		x = 0;
		y += fontSize;
	  }
	  if (Math.random() < 0.5)
		g.setColor(new java.awt.Color((red + y*30) % 256, (green + x/3) % 256, blue));
	  else
        g.setColor(getBackground());
	  g.drawString(word, x, y);
	  x += w;
	}
  }
  public void start() {
	blinker = new Thread(this);
	blinker.start();
  }
  public void stop() {
	blinker = null;
  }
  public void run() {
    Thread me = Thread.currentThread();
	while (blinker == me) {
      try {
        Thread.currentThread().sleep(delay);
      }
      catch (InterruptedException e) {
      }
	  repaint();
	}
  }
 public String getAppletInfo() {
   return "Title: Blinker\nAuthor: Arthur van Hoff\nDisplays multicolored blinking text.";
 }
 public String[][] getParameterInfo() {
   String pinfo[][] = {
     {"speed", "string", "The blink frequency"},
     {"lbl", "string", "The text to blink."},
   };
   return pinfo;
 }
}
```

