[OpenScad](http://www.openscad.org/) ist eine Programmiersprache zum
compilieren von 3D-Objekten. Sie wird oft verwendet um
Open-Source-Hardware zu konstruieren. So sind z.B. viele Objekte auf
[Thingiverse](https://thingiverse.com) damit konstruiert. Meistens kann
über das Verändern von einigen Eingabeparametern die Konstruktion an
die eigenen Bedürfnisse angepasst werden. Thingiverse stellt sogar einen
online-customizer bereit, dem OpenSCAD-Dateien zugrunde liegen. Generell
schreibt man sein OpenSCAD Modell ähnlich wie andere Programmiersprachen
auch und compiliert es dann z.B. mit den auf der [OpenScad
Webseite](http://www.openscad.org/) verfügbaren Compilern zu einem
3D-Objekt, was man sich anschauen, drehen und verschieben kann und
anschließend in ein druckbares Format exportieren kann.

# Dokumentation und Tutorials

Eine Dokumentation der verfügbaren Funktionen gibt es
[hier](http://www.openscad.org/documentation.html). Dort finden sich
auch einige Tutorials um in die Konstruktion mit OpenSCAD einzusteigen.

In [diesem
Tutorial](http://blog.cubehero.com/2013/11/19/know-only-10-things-to-be-dangerous-in-openscad/)
wird eine Schachfigur in OpenSCAD konstruiert.

# weitere libraries installieren

Man kann sich weitere libraries installieren (z.B. zum Einfügen von
Zahnrädern, Schrauben und Muttern etc.).
[Hier](https://en.wikibooks.org/wiki/OpenSCAD_User_Manual/Libraries)
gibt es eine Installationsanleitung und eine Zusammenstellung von
Paketen.

# hilfreiche Tools

  - [OpenSCAD export aus
    Inkscape](http://www.thingiverse.com/thing:25036/#instructions)

# Tipps und Tricks:

## Hüllkurve und Animation

Eine [Hüllkurve](http://doc.cgal.org/latest/Convex_hull_2/index.html)
verbindet Kanten auf eine Weise, dass keine [konkaven
Flächen](https://de.wikipedia.org/wiki/Konvexe_und_konkave_Funktionen)
entstehen. Ein [Oloid](https://de.wikipedia.org/wiki/Oloid) ist z.B. ein
geometrischer Körper, den man sehr leicht mit dieser Technik erzeugen
kann. Das besondere an einem Oloid ist, dass es zwei Kanten und nur eine
Fläche hat und sich trotz seiner seltsamen Form über die gesamte Fläche
abrollen lässt. Zusätztlich zeigt dieses Beispiel, wie man eine
Animation in OpenSCAD erzeugt. Um die Animation zu starten wählt man im
Menü "Ansicht" den Punkt "Animation" und gibt in den sich öffnenden
Feldern z.b. FPS: 10 und Schritte: 200 ein.

` //Durchmesser Kreise (Zylinder mit h gegen Null):`
` d=50;`
` //Höhe der Zylinder sollte gegen Null gehen (darf für das Programm nicht Null sein):`
` h=0.1;`
` //Glättungsparameter für die Überfläche:`
` $fn=100;`
` `
` //Animation:`
` var=$t;`
` rotate([0,0,$t*1*360-90])`
` rotate([sin($t*360)*45+45 ]) `
`  `
` // Oloid wird mit Hüllkurve aus zwei ineinander steckenden Kreisen erzeugt:`
` hull(){`
` translate([d/4,0,0]) cylinder(d=d,h=h);`
` translate([-d/4,0,0]) rotate([90,0,0]) cylinder(d=d,h=h);`
` };`
` `
` // Boden zur Orientierung:`
` color("gray") translate([0,0,-30]) cube([200,200,10], center=true);`