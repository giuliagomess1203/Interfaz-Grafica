# Interfaz-Grafica
package urbanroute.interfaz;
import java.awt.Color;
import java.awt.Cursor;
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.insets;
import java.awt.RenderingHints;
import javax.swing.JButton;
import javax.swing.SwingConstants;
public class BotonPlano extends JButton {
private final Color fondo;
private final Color fondoHover; 
public BotonPlano (String texto, Color fondo, Color fondoHover, Color colortexto, String ayuda) { 
super(texto);
this.fondo = fondo;
this.fondoHover = fondoHover;
setForeground(colorTexto);
setFont(Tema.FUENTE);
setToolTipText(ayuda);
setContentAreaFilled(false);
setBorderPainted(false);
setFocusPainted(false);
setOpaque(false);
setRolloverEnable(true);
setHorizontalAlignments(SwingConstants.LEFT);
setMargin(new Insets(8,14,8,14));
setCursor(Cursor.getPredefinedCursor(Cursor.HAND_CURSOR))}