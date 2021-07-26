# Practica-11
Manejo de archivos
MPOOP11

package mpoop11;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.util.StringTokenizer;
import java.util.logging.Level;
import java.util.logging.Logger;

/**
 *
 * @author Jessica
 */
public class MPOOP11 {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        System.out.println("#######Crear un archivo FILE######");
        try {
            // Los archivos son objetos, me voy a la clase File
            File archivo = new File("archivo.txt"); //tenemos que importar el archivo de  java.oi.File
            System.out.println(archivo.exists()); //pregunto si el archivo existe
            //Se creo solo un objeto, pero en mi computadora no existe un archivo llamada archivo,txt
            boolean seCreo = archivo.createNewFile();
            System.out.println(seCreo);
            System.out.println(archivo.exists());
        } catch (IOException ex) {
            Logger.getLogger(MPOOP11.class.getName()).log(Level.SEVERE, null, ex);
        }
        //Stream de salida, es decir, escribir en un archivo
        System.out.println("***********FileOutputSteam**************");
        
        FileOutputStream fos =null; //se declara y apunta a nulo, debo importar al paquete
           byte[] buffer = new byte [150];//solo es un byte, ya que se puede recibir información de lo que sea de tipo byte
           int nBytes; //contador para saber en que byte estamos
           try{
               System.out.println("Escribir el texto a guardar en el archivo");
           nBytes = System.in.read(buffer); //se guarda en buffer la información
           fos = new FileOutputStream("fos.txt");
           fos.write(buffer, 0, nBytes);  //buffer es un espacio de memoria, en el que se almacenen datos de forma temporal
           }catch(IOException ex){
        System.out.println("Error "+ex.toString());
    }finally{
           
                if(fos != null){
                    try {
                        fos.close();
                    } catch (IOException ex) {
                        Logger.getLogger(MPOOP11.class.getName()).log(Level.SEVERE, null, ex);
                    }
                }
           }
                System.out.println("***********FileInputSteam**************");
                
               FileInputStream fis = null; //tenemos que importar la clase
               String texto;
               try{
                fis = new FileInputStream("fos.txt"); // este archivo se leerá
                nBytes = fis.read(buffer,0,150);
                
                texto = new String(buffer,0,nBytes);
                System.out.println(texto);
                
            } catch (FileNotFoundException ex) {
                Logger.getLogger(MPOOP11.class.getName()).log(Level.SEVERE, null, ex);
            } catch (IOException ex) {
                Logger.getLogger(MPOOP11.class.getName()).log(Level.SEVERE, null, ex);
            } 
           
           System.out.println("**********FileWriter*********");
           BufferedReader br;
           br = new BufferedReader(new InputStreamReader(System.in));
           System.out.println("Escribir texto a guardar: ");
           try{
               texto = br.readLine();
               FileWriter fw = new FileWriter("fw.txt");
               BufferedWriter bw = new BufferedWriter(fw);
               PrintWriter salida = new PrintWriter(bw);
               salida.println(texto);
               salida.close();
               
}catch (IOException ex){
Logger.getLogger(MPOOP11.class.getName()).log(Level.SEVERE, null, ex);
} 
           System.out.println("#####FileReader#####");
           
           try{
           FileReader fr = new FileReader("fw.txt");
           br = new BufferedReader(fr);
               System.out.println("El texto contenido en el archivo es: ");
               String linea = br.readLine();
               while(linea != null){
                   System.out.println(linea);
                   linea = br.readLine();                
               }
          br.close();
           }catch (FileNotFoundException ex) {
               Logger.getLogger(MPOOP11.class.getName()).log(Level.SEVERE, null, ex);
           } catch (IOException ex) {
            Logger.getLogger(MPOOP11.class.getName()).log(Level.SEVERE, null, ex);
        }
           System.out.println("\"******* BufferedReader*******");
           try{
String textoa = "";
BufferedReader br1;
    br1 = new BufferedReader(new InputStreamReader(System.in));
System.out.println("Escribir el textodeseado");
textoa = br1.readLine();
System.out.println("El texto escrito fue:"+textoa);
}catch(IOException ioe){
System.out.println("Existe un error al leer caracteres:\n"+ioe);
}
  
    System.out.println("******* StringTokenizer*******");
String textob = "";
try{
BufferedReader br2;
br2 = new BufferedReader(new
InputStreamReader(System.in));
System.out.println("Escribir texto: ");
textob = br2.readLine();
System.out.println("\n El texto separado por espacios es:");
StringTokenizer st = new
StringTokenizer(textob);
while(st.hasMoreElements()){
System.out.println(st.nextToken());
}
}catch(Exception e){
System.out.println("\nExiste un error al leer el teclado");
e.printStackTrace();
}
System.out.println("******* Serializar*******");
new SerializeDate();
System.out.println("******* Deserializar*******");
new DeSerializeDate();
}
}




class SerializeDate

package mpoop11;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.util.Date;

/**
 *
 * @author Jessica
 */
public class SerializeDate {
    SerializeDate(){
Date d = new Date();
System.out.println(d);
try{
FileOutputStream f = new
FileOutputStream("date.ser");
ObjectOutputStream s = new
ObjectOutputStream(f);
s.writeObject(d);
s.close();
}catch(IOException ioe){
ioe.printStackTrace();
}
}

    
}


class DeSerializeDate

package mpoop11;

import java.io.FileInputStream;
import java.io.ObjectInputStream;
import java.util.Date;

/**
 *
 * @author Jessica
 */
public class DeSerializeDate {

   DeSerializeDate(){
Date d = null;
try{
FileInputStream f = new
FileInputStream("date.ser");
ObjectInputStream s = new
ObjectInputStream(f);
d = (Date) s.readObject();
s.close();
}catch(Exception e){
e.printStackTrace();
}
System.out.println("Deserialized Date objectfrom date.ser");
System.out.println("Date "+d);
}

}
