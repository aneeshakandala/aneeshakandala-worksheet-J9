## 1. What is the difference between a design pattern and a java library?
A design pattern is a concept that provides a conceptual solution to a commonly-occuring software engineering problem, whereas a java library is prewritten code that people can implement to help perform various tasks. 

## 2. Using the Singleton pattern, write code/pseudocode that ensures that only one database connection object is ever instantiated.
```
public class LargeFile {
    // This is a private member variable so that the file
    // can only be accessed through the getInstance() method.
    private static LargeFile singleton;
    private static StringBuffer fileContents;

    // Private constructor forces the class to be instantiated 
    // via the getInstance method.
    private LargeFile() {
        // private constructor
        // set up the object here
        fileContents = new StringBuffer();

        try{
            FileInputStream fstream = new FileInputStream("my_large_file.txt");
            BufferedReader br = new BufferedReader(new InputStreamReader(fstream));

            String strLine;
            while ((strLine = br.readLine()) != null)   {
                fileContents.append(strLine);
            }
            fstream.close();     
        } catch (IOException e){
            System.out.println("Sorry could not open your file.");
        }

    }

    // Method to get an instance of this class.
    public static LargeFile getInstance(){
        // Otherwise return the existing instance.
        if (singleton == null) {
            singleton = new LargeFile();
        }

        return singleton;//returning existing instance (ONE instance)
    }
}

```

## 3. Assume there is an ```Animal``` abstract parent class that has the following constructor: ```public Animal(String name, int weight```.

Using the Factory pattern, write code/pseudocode that sets up a factory for two child classes of ```Animal```: ```Bird``` and ```Mammal```. Each of these has a constructor with the same arguments as those of the parent class.

- the code for this example may look something like this, based on the lecture notes:

```
public class AnimalFactory {

    public static Animal getAnimal(String type, String name, int weight) {
        switch (type) {
            case "bird":
                return new Bird(name, weight);
            case "mammal":
                return new Mammal(name, weight);
        }
    }
}
```


## 4. Imagine we have some code for an aquarium that works nicely to schedule feeding the fish in all the tanks, and cleaning the tanks:

```
public class Aquarium {
	public void feedAll(ArrayList<Fish> tanks, int numFishInTank) {...}
	public void cleanAll(ArrayList<Fish> tanks)
}

```
This code works well with the following ```Fish``` class:

```
public class Fish{
	public void feed(String food, int weight) {...}
	public void clean(String cleaningProduct) {...}
}
```

We also, one day, inherit an animal hospital, where each patient is solo in a cage. We want to be able to use the code above to feed and clean the cages of all the animals, but our hospital has the following API for the mammals they serve:

```
public class Mammal{
	public void feed(String food, int weight, String medication) {...}
	public void clean() {...}
}
```
Use the Adapter pattern to allow us to use the ```Mammal``` class with the ```Aquarium``` class above. Each animal is housed alone in its cage during its visit. All mammals are given the same medication, namely, ```"antibiotics"```.
```

public class MammalAdapter extends Fish {
    private Mammal mammal;

    public MammalAdapter(Mammal mammal) {
        this.mammal = mammal;
    }

    @Override //do we need to override, maybe to adapt to Mammal's feed
    public void feed(String food, int weight) {
        mammal.feed(food, weight, "antibiotics");
    }

  @Override //override for the same reason?
    public void clean(String cleaningProduct) {
        mammal.clean(); 
    }
}

```
## 5. What is the benefit of the Bridge design pattern? Why use one?
The Bridge design pattern allows for separation between the implementation and the abstraction of a class, so that the two can be independent. This is useful because it makes the system you are working on easier to maintain and utilize.  



