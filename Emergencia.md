import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Vector;

public class Emergencia{
	private Vector<Paciente> pacientes = new Vector<Paciente>();
	private int cantPatients= 0;
	public void entrarPacientes(String file) throws FileNotFoundException{
		File archivo = new File(file);
		String palabra = "";
		String[] palabras;
		BufferedReader br = new BufferedReader(new FileReader(file));
	    String line = null;
        try {
			while ((line = br.readLine()) != null) {
			    palabras=line.split(",");
			    pacientes.add(new Paciente(palabras[0].replace(" ", ""), palabras[1].replace(" ", ""),palabras[2].replace(" ", "")));
			    cantPatients+=1;
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
	} 
	
	public String devolverPacientesEnOrden(){
		String pacientesEnOrden="";
		VectorHeap2 heap = new VectorHeap2 (pacientes);
		for(int i=0; i<cantPatients; i++){
			Paciente paciente = (Paciente)heap.remove();
			pacientesEnOrden=pacientesEnOrden+paciente.getNombrePaciente()+" "+","+paciente.getEnfermedad()+" "+","+paciente.getPrioridad()+"\n";
		}
		return pacientesEnOrden;
	}
}
