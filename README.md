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
public Dimension getMaximumSize(){
return new Dimension(Integer.MAX_VALUE, getPreferredSize().height);
}
protected void paintComponent(Graphics g){
Graphics2D g2 = (Graphics2D) g.create ();
g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
Color color = fondo;
if (!isEnabled()){
color = fondo.darker();
} else if (getmodel().isPressed()){
color = fondoHover.darker();
} else if (getModel().isRollover()){
color = fondoHover;
}
g2.setColor(color);
g2.fillRoundRect(0,o,getWidth(), getHeight(), 10, 10);
g2.dispose();
super.paintComponent(g);
}
}

package urbanroute.interfaz;
import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.Frame;
import javax.swing.BorderFactory;
import javax.swing.DefaultListModel;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JComponent;
import javax.swing.JDialog;
import javax.swing.JLabel;
import javax.swing.JList;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import urbanroute.estructuras.Arista;
import urbanroute.estructuras.ListaEnlazada;
import urbanroute.modelo.Estacion;
import urbanroute.modelo.Formato;
import urbanroute.modelo,RedTransporte;
public class DialogoNuevaEstacion extends JDialog{
private final RedTransporte red;
private final JTextField campold = new JTextField (14);
private final JTextField campoNombre = new JTextField (14);
private final JComboBox<string> comboLinea;
private final JComboBox<string> comboZona;
private final JSpinner spinnerCapacidad = new JSpinner (new SpinnerNumberModel(10000, 0, 1000000, 500));
private final JComboBox<estacion> comboVecina;
private final JSpinner spinnerTiempo = new JSPinner (new SpinnerNumberModel(2.0, 0.5, 999.0, 0.5));
private final DefaultListModel<string> modeloConexiones = new DefaultListModel<>();
private final JList<string> listaConexiones = new Jlist<>(modeloConexiones);
private final ListaEnlazada<arista> conexiones = new ListaEnlazada<>();
private Estacion resultado;
public DialogoNuevaEstacion(Frame padre, RedTransporte red){
super(padre, "Agregar Estacion", true);
this.red = red;
comboLinea = new JComboBox<>(red.obtenerLineas());
comboLinea.setEditable(true);
comboZona = new JComboBox<>(red.obtenerZonas());
comboZona.setEditable(true);
comboVecina = new JComboBox<>(red.obtenerEstacionesOrdenadas());
JPanel datos = Dialogos.formulario(new String]{"ID:", "Nombre:", "Linea:", "Zona:", "Capacidad:"}, new JComponent ]{campold, campoNombre, comboLinea, comboZona, spinnerCapacidad});
datos.setBorder(BorderFactory.createTitledBorder("1.Datos de la Estacion"));
JPanel conex = new JPanel(new BorderLayout(6, 6));
conex.setBorder(BorderFactory.createTitledBorder("2. Conexiones con estaciones existentes"));
JPanel fila = new JPanel(new FlowLayout(FlowLayout.LEFT, 6, 0));
fila.add(new JLabel("Estacion:"));
comboVecina.setPreferredSize(new Dimension(220, comboVecina.getPreferredSize().height));
fila.add(comboVecina);
fila.add(new JLabel("Min:"));
fila.add(spinnerTiempo);
JButton agregar = new JButton ("Añadir");
aregar.addActionListener(e-> agregarConexion());
fila.add(agregar);
JButton quitar = new JButton("Quitar seleccionada");
quitar.addActionListener(e-> quitarConexion());
listaConexiones.setVisibleRowCount(5);
conex.add(fila, borderLayout.NORTH);
conex.add(new JScrollPane(ListaConexiones), BorderLayout.CENTER);
conex.add(quitar, BorderLayout.SOUTH);
if(comboVecina.getItemCount()==0){