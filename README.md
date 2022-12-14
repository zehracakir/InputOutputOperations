# InputOutputOperations
# I/O DATA STREAMS

- An input stream (Input Stream) is used to read data and an output stream (Output Stream) to write data.

```java
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!"); 
    }
}
```

- We should say that data streams in Java are divided into two main groups:
1. Byte Streams
2. Character Streams

## **Byte Stream**

- The byte stream is used to read and write single bytes (8 bits) of data. All streams that are not of image, graphic, sound and similar character type are byte streams.
- All byte stream classes derive from InputStream and OutputStream abstract classes.

## **Character Stream**

- The character stream is used to read and write a single data character. Character streams, as the name suggests, input/output data of character type. Because it uses Unicode, it adapts to the alphabets of different countries.
- All character stream classes derive from the Reader and Writer abstract classes.

## File Class

- The File class of the “Java.io” package is used to perform various operations on files and directories.

### Files and Directories

- A file is a named location that can be used to store related information.
- For example: main.java is a Java file that contains information about the Java program.
- Directories are a collection of files and subdirectories. A directory inside a directory is known as a subdirectory.
- To create a File object, we first need to import the java.io.File package.

```java
File file = new File(String pathName);
```

### File Methods

![Operations-on-File-in-Java.webp](https://github.com/zehracakir/InputOutputOperations/blob/main/Operations-on-File-in-Java.png)

✴️ File Creation:

- We can use the createNewFile() method to create a new file. The method returns true if a new file is created, false if the file already exists in the specified location.

```java
import java.io.File;
import java.io.IOException;

public class CreateFile {
    public static void main(String[] args) {
        File file=new File("zehracakir.txt");
        try {
            boolean value=file.createNewFile();
            if(value){
                System.out.println("file created");
            }else{
                System.out.println("file already exists");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}
```

✴️ File Deletion:

- We can use File class's delete() method to delete the specified file or directory.

```java
import java.io.File;

public class DeleteFile {
    public static void main(String[] args) {
        File file = new File("zehracakir.txt");
        boolean value = file.delete();
        if (value) {
            System.out.println("The File is deleted.");
        } else {
            System.out.println("The File is not deleted.");
        }
    }
}
```

✴️ Indexing

- The Java File class provides the mkdir() method to create a new directory. method backwards
1. true if new directory is created,
2. returns false if the directory already exists.

```java
import java.io.File;

public class Indexing {
    public static void main(String[] args) {
        File file = new File("zehra/cakir");
        boolean value = file.mkdir();
        if (value) {
            System.out.println("directory created");
        } else {
            System.out.println("Could not create directory");
        }

    }
}
```

✴️ List Elements in Directory

```java
import java.io.File;

public class ListElements {
    public static void main(String[] args) {
        File file=new File("zehracakir");

        String[] fList=file.list();

        for(String str:fList){
            System.out.println(str);
        }
    }
}
```

## InputStream Class

- The InputStream class is an abstract class that represents a byte stream and comes from the “Java.io” package.
- Since InputStream is an abstract class, it is not useful on its own, so subclasses of InputStream are used to read data.
- InputStream subclasses: FileInputStream, ByteArrayInputStream, ObjectInputStream

### **FileInputStream**

- The FileInputStream class of the “Java.io” package is used to read data (in bytes) from files.
- InputStream inherits the abstract class.

✔️ FileInputStream Methods:

- read(): Reads a single byte of data from the file.
- read(byte[] array): Reads data in bytes from the file and stores it in the specified array.
- available(): Returns the number of available bytes.
- skip(): We can use the skip() method to discard and skip the specified number of bytes.
- Example

```java
package fileInputStream;

import java.io.File;
import java.io.FileInputStream;

public class FileInputStreamClass {
    public static void main(String[] args) {
        try {
            //createNewFile()
            File file = new File("zehracakirr.txt");
            file.createNewFile();
            FileInputStream fileInputStream = new FileInputStream("zehracakirr.txt");

            //available()
            System.out.println("Number of available bytes: " + fileInputStream.available());

            //skip()
            fileInputStream.skip(10);

            //read()
            int i = fileInputStream.read();
            while (i > -1) {
                System.out.println(i);
                i = fileInputStream.read();
            }
            //end we are close the file
            fileInputStream.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### FileOutputStream Class

- The FileOutputStream class of the “Java.io” package can be used to write data (in bytes) to files.
- Extends the OutputStream abstract class.
- Example

```java
package fileOutputStream;

import java.io.FileNotFoundException;
import java.io.FileOutputStream;

public class FileOutputStreamClass {
    public static void main(String[] args) {
        try {
            //if boolean value=true --> writes to the end of the file
            //else boolean value=false --> overwrites the file
            //FileOutputStream fileOutputStream=new FileOutputStream("zehracakir.txt"); ---> still available
            FileOutputStream outputStream = new FileOutputStream("zehracakir.txt", true);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }

}
```

### **ByteArrayInputStream**

- The “Java.io” package's ByteArrayInputStream class can be used to read an array of input data (in bytes).
- In ByteArrayInputStream, the input stream is created using a byte array. It contains an internal array to store the data of this byte array.
- To create a byte array input stream, we must first import the java.io.ByteArrayInputStream package.
- Example

```java
package byteArrayInputStream;

import java.io.ByteArrayInputStream;

public class ByteArrayInputStreamClass {
    public static void main(String[] args) {
        byte[] array = {1, 127, 87, 52, 74, 12, 2, 18};
        try {
            //Creates a ByteArrayInputStream that reads the entire array
            ByteArrayInputStream byteArrayInputStream = new ByteArrayInputStream(array);
            int i = byteArrayInputStream.read();
            while (i > -1) {
                System.out.println(i);
                i = byteArrayInputStream.read();
            }
            System.out.println("----------------------------------------");
            byte[] array1 = {1, 127, 87, 52, 74, 12, 2, 18};
            //Creates a ByteArrayInputStream that reads part of the array
            ByteArrayInputStream byteArrayInputStream1 = new ByteArrayInputStream(array1, 2, 3);
            int a = byteArrayInputStream1.read();
            while (a > -1) {
                System.out.println(a);
                a = byteArrayInputStream1.read();
            }
            System.out.println("----------------------------------------");
            byte[] array2 = {1, 127, 87, 52, 74, 12, 2, 18};
            //Creates a ByteArrayInputStream that reads part of the array
            ByteArrayInputStream byteArrayInputStream2 = new ByteArrayInputStream(array2);
            byteArrayInputStream2.skip(3);
            int b = byteArrayInputStream2.read();
            while (b > -1) {
                System.out.println(b);
                b = byteArrayInputStream2.read();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### **ByteArrayOutputStream**

- The “Java.io” package's ByteArrayOutputStream class can be used to write an array of output data (in bytes)
- Extends the OutputStream abstract class.
- ByteArrayOutputStream has an internal byte array to store data.
- Example



```java
package byteArrayOutputStream;

import java.io.ByteArrayOutputStream;

public class ByteArrayOutputStreamClass {
    public static void main(String[] args) {

        String data = "Patika ile Java Öğreniyorum";

        try {
            //Creates a ByteArrayOutputStream of default size
            ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
            byte[] array = data.getBytes();
            outputStream.write(array);

            String streamData = outputStream.toString();
            System.out.println("Output Stream : " + streamData);

            outputStream.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### **Serialization**

- We have the problem of not knowing the type information of the values when we generate an object of any class, write it to a file and read it again from the file. This is exactly where the Java Serialization API comes to our aid.
- Thanks to the Java Serialization API, we can store an exact copy of an object outside of the Java platform. With this mechanism, we can then pull the object from the stored location and continue to use it with the same state and properties. This whole system is called Object Serialization.
- All that needs to be done to serialize objects is to specify at the beginning of the class declaration that our object to be serialized is serializable, thanks to the tagging interface.
- To serialize objects, the Java platform provides 2 base classes. With these two classes, called ObjectInputStream and ObjectOutputStream, we can serialize any class that implements the Serializable interface. The first of these two classes, ObjectInputStream, implements the ObjectInput interface and is used to read the serialized object back from the stream. The other class named ObjectInputStream implements the ObjectOutput interface and is used to print any object to the stream.
- Example

```java
import java.io.Serializable;

public class Car implements Serializable {
    
    private String brand;
    private String model;

    Car(String brand, String model) {
        this.brand = brand;
        this.model = model;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public String getModel() {
        return model;
    }

    public void setModel(String model) {
        this.model = model;
    }
}
```

### **ObjectOutputStream**

- The ObjectOutputStream class of the “Java.io” package can be used to write objects that can be read by the ObjectInputStream. Extends the OutputStream abstract class.
- Basically, ObjectOutputStream encodes Java objects using the class name and object values and creates the corresponding streams. This process is known as serialization.
- Converted streams can be stored in files and transferred between networks.
- Note: The ObjectOutputStream class only writes objects that implement the Serializable interface. This is because objects need to be serialized as they are written to the stream.
- To create an object output stream, we must first import the java.io.ObjectOutputStream package.
- Example

```java
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;

public class SerialTest {
    public static void main(String[] args) {

        try {
            Car car = new Car("Hyundai", "Getz");
            FileOutputStream file = new FileOutputStream("output.txt");
            ObjectOutputStream write = new ObjectOutputStream(file);
            write.writeObject(car);
            write.close();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### **ObjectInputStream**

- The ObjectInputStream class of the “Java.io” package can be used to read objects previously written by ObjectOutputStream.
- Extends the InputStream abstract class.
- Example

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

public class SerialTest {
    public static void main(String[] args) {

        try {
            Car car = new Car("Hyundai", "Getz");
            FileOutputStream file = new FileOutputStream("output.txt");
            ObjectOutputStream write = new ObjectOutputStream(file);
            write.writeObject(car);

            FileInputStream fileIn = new FileInputStream("output.txt");
            ObjectInputStream read = new ObjectInputStream(fileIn);

            // Reads the objects
            Car newCar = (Car) read.readObject();

            System.out.println("Car Brand : " + newCar.getBrand());
            System.out.println("Car Model: " + newCar.getModel());

            read.close();
            write.close();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

## **BufferedInputStream**

- The “Java.io” package's BufferedInputStream class is used with other input streams to read data (in bytes) more efficiently. Extends the InputStream abstract class.
- BufferedInputStream maintains an internal buffer of 8192 bytes. During the read operation in the BufferedInputStream, a stack of bytes is read from the disk and stored in the internal buffer. Also, bytes are read individually from the internal buffer. This reduces the number of communications with the disk. This is why reading bytes using BufferedInputStream is faster.
- Example

```java
package bufferedInputStream;

import java.io.BufferedInputStream;
import java.io.FileInputStream;

public class BufferedInputStreamClass {
    public static void main(String[] args) {
        try {
            FileInputStream file = new FileInputStream("zehracakir.txt");
            BufferedInputStream bufferedInputStreamClass = new BufferedInputStream(file);
            int i = bufferedInputStreamClass.read();

            while (i != -1) {
                System.out.print((char) i);

                i = bufferedInputStreamClass.read();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## **BufferedOutputStream**

- The “Java.io” package's BufferedOutputStream class is used with other output streams to write data (in bytes) more efficiently. Extends the OutputStream abstract class.
- BufferedOutputStream maintains an internal buffer of 8192 bytes. During the write operation, bytes are written to the internal buffer instead of the disk. After the buffer is filled or the stream is turned off, the entire buffer is written to disk. This reduces the number of communications with the disk. This is why writing bytes using BufferedOutputStream is faster.
- Example

```java
import java.io.BufferedOutputStream;
import java.io.FileOutputStream;

public class PatikaDev {
    public static void main(String[] args) {

        String data = "Patika Dev Java102";

        try {
            // FileOutputStream
            FileOutputStream file = new FileOutputStream("output.txt");

            // BufferedOutputStream
            BufferedOutputStream output = new BufferedOutputStream(file);

            byte[] array = data.getBytes();

            output.write(array);
            output.close();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

## PrintStream

- The PrintStream class of the “Java.io” package can be used to write output data in a widely readable format (text) rather than bytes.
- Extends the abstract OutputStream class.
- Unlike other output streams, PrintStream converts primitive data (integer, character) to text rather than bytes. It then writes this formatted data to the output stream
- Also, the PrintStream class does not throw any input/output exceptions. Instead, we need to use the checkError() method to find any errors in it.
- Example

```java
import java.io.PrintStream;

class Main {
    public static void main(String[] args) {

        String data = "Hello World.";

        try {
            PrintStream output = new PrintStream("output.txt");

            output.print(data);
            output.close();
        }
        catch(Exception e) {
            e.getStackTrace();
        }
    }
}
```

### **InputStreamReader Class**

- The InputStreamReader class of the “Java.io” package can be used to convert data in bytes to data in characters. Extends the abstract Reader class.
- The InputStreamReader class works with other input streams (Input Streams). Also known as a bridge between byte streams and character streams. This is because the InputStreamReader reads the bytes from the input stream as characters.
- For example, some characters required 2 bytes to be stored in storage. To read this type of data we can use the InputStreamReader class which reads the 2 bytes together and converts them to the corresponding character.
- Example

```java
import java.io.InputStreamReader;
import java.io.FileInputStream;

public class PatikaDev {
    public static void main(String[] args) {

        char[] array = new char[100];

        try {
            // FileInputStream
            FileInputStream file = new FileInputStream("input.txt");

            // InputStreamReader
            InputStreamReader input = new InputStreamReader(file);

            int data = input.read();
            while (data != -1) {
                System.out.print((char) data);
                data = input.read();
            }
            
            input.close();
        } catch (Exception e) {
            e.getStackTrace();
        }

    }
}
```

## **Writer Sınıfı**

- The Writer class of the “Java.io” package is an abstract superclass that represents a stream of characters.
- Writer is not useful on its own because it is an abstract class. However, its subclasses can be used to write data.

### OutputStreamWriter

- The OutputStreamWriter class of the “Java.io” package can be used to convert character-format data to byte-format data. Extends the Writer abstract class.
- The OutputStreamWriter class works with other output streams. Also known as a bridge between byte streams and character streams. This is because OutputStreamWriter converts its characters to bytes.
- For example, storing some characters in storage requires 2 bytes. To write this type of data, we can use the OutputStreamWriter class, which converts the character to its corresponding bytes and stores the bytes together.
- Example

```java
import java.io.FileOutputStream;
import java.io.OutputStreamWriter;
import java.nio.charset.StandardCharsets;

public class PatikaDev {
    public static void main(String[] args) {

        try {
            FileOutputStream file = new FileOutputStream("output.txt");

            OutputStreamWriter output1 = new OutputStreamWriter(file);

            OutputStreamWriter output2 = new OutputStreamWriter(file, StandardCharsets.UTF_8);
						
						//The getEncoding() method can be used to get the encoding type used to write data to the output stream
            System.out.println("Character encoding of output1: " + output1.getEncoding());
            System.out.println("Character encoding of output2: " + output2.getEncoding());

            output1.close();
            output2.close();
        }

        catch(Exception e) {
            e.getStackTrace();
        }
    }
}
```

## **FileReader**

- The FileReader class of the “Java.io” package can be used to read data (as characters) from files. Extends the InputStreamReader class.
- Example

```java
import java.io.FileReader;

public class PatikaDev {
    public static void main(String[] args) {
        try {
            FileReader input = new FileReader("input.txt");

            int data = input.read();
            while (data != -1) {
                System.out.print((char) data);
                data = input.read();
            }

            input.close();
        } catch (Exception e) {
            e.getStackTrace();
        }
    }
}
```

## **FileWriter**

- The FileWriter class of the “Java.io” package can be used to write data (as characters) to files. Extends the OutputStreamWriter class.
- Example

```java
import java.io.FileWriter;

public class PatikaDev {
    public static void main(String[] args) {
        String data = "Patika Java102 Dersleri";

        try {
            FileWriter output = new FileWriter("output.txt");
            output.write(data);

            output.close();
        } catch (Exception e) {
            e.getStackTrace();
        }
    }
}
```

## **BufferedReader**

- The “Java.io” package's BufferedReader class can be used with other readers to read data (as characters) more efficiently. Extends the abstract Reader class.
- BufferedReader maintains an internal buffer of 8192 characters. During the read operation in BufferedReader, a chunk of characters are read from the disk and stored in the internal buffer, and the characters are read individually from the internal buffer. This reduces the number of communications with the disk. This is why it is faster to read characters using the BufferedReader.
- Example

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class PatikaDev {
    public static void main(String[] args) {

        try {
            FileReader file = new FileReader("input.txt");
            BufferedReader input = new BufferedReader(file);

            String line;
            while ((line = input.readLine()) != null) {
                System.out.println(line);
            }

            input.close();
        } catch (Exception e) {
            e.getStackTrace();
        }
    }
}
```

## **BufferedWriter**

- The “Java.io” package's BufferedWriter class can be used with other writers to write data (as characters) more efficiently. Extends the Writer abstract class.
- Example

```java
import java.io.BufferedWriter;
import java.io.FileWriter;

public class PatikaDev {
    public static void main(String[] args) {
        String data = "Java 102 PatikaDev zehracakir";

        try {
            FileWriter file = new FileWriter("output.txt");

            BufferedWriter output = new BufferedWriter(file);

            output.write(data);

            output.close();
        } catch (Exception e) {
            e.getStackTrace();
        }
    }
}
```

## **PrintWriter**

- The PrintWriter class of the “Java.io” package can be used to write output data in a widely readable format (text). Extends the Writer abstract class.
- Unlike other Writer classes, PrintWriter converts primitive data (int, float, char, etc.) to text format. It then transfers this formatted data to Writer.
- Also, the PrintWriter class does not throw any input/output exceptions. Instead, we need to use the checkError() method to find any errors in it.
- Example

```java
import java.io.PrintWriter;

public class PatikaDev {
    public static void main(String[] args) {
        String data = "Java 102 PAtikaDev zehrackr.";
        try {
            PrintWriter output = new PrintWriter("output.txt");
            output.print(data);
            output.close();
        } catch (Exception e) {
            e.getStackTrace();
        }
    }
}
```