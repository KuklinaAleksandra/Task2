# TasK2
 package project10;

import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.File;
import java.io.IOException;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.PrintWriter;
import java.util.Random;
import java.util.UUID;

public class KlassFile11 {
	private static int UTF_COUNT = 3;
	private static int DBL_COUNT = 5;
	public static void main(String[] args) throws IOException 
	{
		DataInputStream in = null;
		PrintWriter out = null;
		try {
			in = new DataInputStream(new FileInputStream(PrepareFile(GetFileByName("Task2Input.txt"))));
			out = new PrintWriter(GetFileByName("Task2Output.txt"),"cp1251");
			for (int i = 0; i < UTF_COUNT; i++) {
				String string = in.readUTF();
				if (i==1) {
					out.println(string);
				}
				System.out.println("Строка №" + i+1 + ": " + string);
			}
			for (int i = 0; i < DBL_COUNT; i++) {
				double dbl = in.readDouble();
				if (dbl > 0) {
					out.println(dbl);
				}
				System.out.println("Число №" + i+1 + ": " + dbl);
			}
		} 
		catch (Exception e) {
			System.out.println("Error: " + e.getMessage());
		}
		finally {
			in.close();
			out.flush();
			out.close();
		}
	}

	private static String DirPath = "C:\\Test\\%s";
	public static File GetFileByName(String filename) throws IOException {
		 File f1=new File(String.format(DirPath, filename));
		 f1.createNewFile();
		 return f1;
	}
	public static File PrepareFile(File file) throws IOException {
		DataOutputStream in = null;
		try {
			in = new DataOutputStream(new FileOutputStream(file));
			Random r = new Random();
			for (int i = 0; i < UTF_COUNT; i++) {
				in.writeUTF(UUID.randomUUID().toString());
			}
			for (int i = 0; i < DBL_COUNT; i++) {
				in.writeDouble(-1000 + 2000 * r.nextDouble());
			}	
		} catch (Exception e) {
			System.out.println("Error: " + e.getMessage());
		}
		finally {
			if (in != null) {
				in.close();
			}
		}	
		return file;
	}
}


