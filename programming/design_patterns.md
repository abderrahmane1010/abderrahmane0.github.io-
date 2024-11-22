# Les patrons de conceptions - design patterns :

Les **patrons de conception** (design patterns) sont des solutions classiques à des problèmes récurrents de la conception de logiciels. Chaque patron est une sorte de plan ou de schéma que vous pouvez personnaliser afin de résoudre un problème récurrent dans votre code.

Les patrons de conception diffèrent par leur complexité, leur niveau de détails et l’échelle à laquelle ils peuvent être mis en œuvre. Ils sont rangés dans trois catégories selon leur intention.

- Les **Patrons de création** fournissent des mécanismes de création d’objets, ce qui augmente la flexibilité et la réutilisation du code.
- Les **Patrons structurels** expliquent comment assembler des objets et des classes en de plus grandes structures, tout en les  gardant flexibles et efficaces.
- Les **Patrons comportementaux** mettent en place une communication efficace et répartissent les responsabilités entre les objets.

## Patron de création : 

### Simple Factory

Le **Simple Factory** est un pattern de création qui fournit une méthode pour créer des objets sans exposer la logique d'instanciation au client. Il centralise la création d'objets dans une seule classe ou fonction, souvent appelée "Factory".

#### **Principe**

1. Une classe "Factory" est responsable de la création des instances d'autres classes.
2. Le client utilise la Factory pour obtenir des objets au lieu d'utiliser directement le mot-clé `new` ou les constructeurs.
3. Cela permet d'encapsuler la logique de création et de simplifier le code client.

```java
// Interface de base
interface Shape {
    void draw();
}

// Implémentations concrètes
class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing a Circle.");
    }
}

class Rectangle implements Shape {
    public void draw() {
        System.out.println("Drawing a Rectangle.");
    }
}

// Classe Factory
class ShapeFactory {
    public static Shape createShape(String type) {
        if (type.equalsIgnoreCase("circle")) {
            return new Circle();
        } else if (type.equalsIgnoreCase("rectangle")) {
            return new Rectangle();
        }
        return null;
    }
}

// Classe principale
public class Main {
    public static void main(String[] args) {
        Shape circle = ShapeFactory.createShape("circle");
        circle.draw();

        Shape rectangle = ShapeFactory.createShape("rectangle");
        rectangle.draw();
    }
}

```

### Factory Method

Le **Factory Method** est un pattern de création qui repose sur des sous-classes pour instancier des objets spécifiques. Contrairement au Simple Factory, il utilise une classe abstraite ou une interface avec une méthode de création polymorphique que chaque sous-classe doit implémenter.

#### **Principe**

1. Une **classe abstraite** ou une **interface** déclare une méthode de création abstraite.
2. Les **sous-classes concrètes** implémentent cette méthode pour créer des objets spécifiques.
3. Le client utilise la classe abstraite pour travailler avec les objets, sans connaître leurs implémentations spécifiques.

```java
// Interface de base
interface Shape {
    void draw();
}
class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing a Circle.");
    }
}
class Rectangle implements Shape {
    public void draw() {
        System.out.println("Drawing a Rectangle.");
    }
}

// Créateur abstrait
abstract class ShapeCreator {
    // Factory Method
    protected abstract Shape createShape();

    // Méthode commune
    public void drawShape() {
        Shape shape = createShape(); // Appelle le Factory Method
        shape.draw();
    }
}

// Créateurs concrets
class CircleCreator extends ShapeCreator {
    @Override
    protected Shape createShape() {
        return new Circle();
    }
}

class RectangleCreator extends ShapeCreator {
    @Override
    protected Shape createShape() {
        return new Rectangle();
    }
}

// Classe principale
public class Main {
    public static void main(String[] args) {
        ShapeCreator creator;

        // Décision dynamique
        String type = "circle"; // Changez en "rectangle" pour tester
        if (type.equalsIgnoreCase("circle")) {
            creator = new CircleCreator();
        } else {
            creator = new RectangleCreator();
        }

        creator.drawShape();
    }
}
```

<img src="/home/abder/Desktop/notes_/programming/factorymethod.png" alt="20" style="zoom:80%;" />

### Différence entre simple factory et method factory : 

#### **Simple Factory**

- La logique de création des objets est centralisée dans une seule classe (ou méthode statique).
- Le client ne sait rien des implémentations spécifiques, mais **toute la logique de création est contenue dans un seul endroit**, ce qui peut devenir complexe si le nombre d'objets augmente.

**Exemple clé** : Une classe `ShapeFactory` contient une méthode statique `createShape(String type)` qui décide quel objet créer.

#### **Factory Method**

- La création des objets est déléguée à des **sous-classes** spécifiques via une méthode abstraite.
- Cela permet de découpler la logique de création et facilite l'extension (ajout de nouvelles formes) en créant simplement une nouvelle sous-classe du créateur.

### Abstract Factory

L'**Abstract Factory** est un design pattern de création qui permet de produire des familles d'objets liés ou dépendants **sans spécifier leurs classes concrètes**. Contrairement au **Factory Method**, ce pattern gère plusieurs produits en même temps et garantit leur cohérence.

#### **Principe**

1. Une interface ou une classe abstraite définit plusieurs méthodes pour créer différents types de produits.
2. Les **implémentations concrètes** produisent des ensembles spécifiques d'objets compatibles.
3. Le client utilise uniquement l'interface abstraite et ne connaît pas les classes concrètes.

```java
// Produit de base 1 : Forme 2D
interface Shape2D {
    void draw();
}

// Produits concrets 2D
class Circle2D implements Shape2D {
    public void draw() {
        System.out.println("Drawing a 2D Circle.");
    }
}

class Rectangle2D implements Shape2D {
    public void draw() {
        System.out.println("Drawing a 2D Rectangle.");
    }
}

// Produit de base 2 : Forme 3D
interface Shape3D {
    void draw();
}

// Produits concrets 3D
class Circle3D implements Shape3D {
    public void draw() {
        System.out.println("Drawing a 3D Circle.");
    }
}

class Rectangle3D implements Shape3D {
    public void draw() {
        System.out.println("Drawing a 3D Rectangle.");
    }
}

// Abstract Factory : Interface pour créer des formes 2D et 3D
interface ShapeFactory {
    Shape2D create2DShape();
    Shape3D create3DShape();
}

// Factories concrètes
class CircleFactory implements ShapeFactory {
    public Shape2D create2DShape() {
        return new Circle2D();
    }

    public Shape3D create3DShape() {
        return new Circle3D();
    }
}

class RectangleFactory implements ShapeFactory {
    public Shape2D create2DShape() {
        return new Rectangle2D();
    }

    public Shape3D create3DShape() {
        return new Rectangle3D();
    }
}

// Classe principale
public class Main {
    public static void main(String[] args) {
        ShapeFactory factory;

        // Décision dynamique
        String type = "circle"; // Changez en "rectangle" pour tester
        if (type.equalsIgnoreCase("circle")) {
            factory = new CircleFactory();
        } else {
            factory = new RectangleFactory();
        }

        // Création d'un ensemble compatible
        Shape2D shape2D = factory.create2DShape();
        Shape3D shape3D = factory.create3DShape();

        shape2D.draw();
        shape3D.draw();
    }
}
```

<img src="/home/abder/Desktop/notes_/programming/abstractfactory.png" alt="20" style="zoom:80%;" />

### **Différence entre Factory Method et Abstract Factory**

| **Aspect**     | **Factory Method**                                          | **Abstract Factory**                                         |
| -------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
| **But**        | Crée un **type unique** d'objet.                            | Crée **plusieurs types d'objets liés**.                      |
| **Extension**  | Ajout d'un nouveau type nécessite une nouvelle sous-classe. | Ajout d'une nouvelle famille nécessite une nouvelle factory. |
| **Complexité** | Moins complexe, mais moins flexible.                        | Plus complexe, mais offre une cohérence entre objets.****    |

### Builder :

Le **Builder** est un design pattern de création qui permet de construire des objets complexes étape par étape. Il est particulièrement utile lorsque :

1. Un objet a beaucoup de paramètres ou de sous-composants.
2. Tu veux construire différents types de représentations du même objet.

------

### **Principe**

1. Le **Builder** découpe la construction d'un objet complexe en plusieurs étapes (ou méthodes).
2. Un **Director** (facultatif) peut orchestrer le processus en appelant les méthodes du Builder dans un ordre précis.
3. Le client peut choisir le Builder qu'il veut utiliser pour construire l'objet final.

```java
// Produit final : Shape
abstract class Shape { /* Shape abstraite avec propriétés communes */ }

class Circle extends Shape { /* Cercle avec couleur et remplissage */ }
class Rectangle extends Shape { /* Rectangle avec couleur et remplissage */ }

// Builder : construit des objets Shape
class ShapeBuilder {
    public Shape buildCircle() { return new Circle(); }
    public Shape buildRectangle() { return new Rectangle(); }
}

// Director : orchestre la construction des formes
class ShapeDirector {
    private ShapeBuilder builder;
    public ShapeDirector(ShapeBuilder builder) {
        this.builder = builder;
    }
    public Shape createCircle() { return builder.buildCircle(); }
    public Shape createRectangle() { return builder.buildRectangle(); }
}

public class Main {
    public static void main(String[] args) {
        ShapeBuilder builder = new ShapeBuilder();
        ShapeDirector director = new ShapeDirector(builder);

        Shape circle = director.createCircle();
        Shape rectangle = director.createRectangle();
    }
}

```

Exemple concret
```java
// Produit final : Shape
abstract class Shape {
    protected String color;
    protected boolean isFilled;
    public abstract void draw();
}

class Circle extends Shape {
    private double radius;
    public Circle(double radius, String color, boolean isFilled) { /* Initialisation */ }
    public void draw() { System.out.println("Drawing Circle"); }
}

class Rectangle extends Shape {
    private double width, height;
    public Rectangle(double width, double height, String color, boolean isFilled) { /* Initialisation */ }
    public void draw() { System.out.println("Drawing Rectangle"); }
}

// Builder : construit des objets Shape
class ShapeBuilder {
    private String color;
    private boolean isFilled;

    public ShapeBuilder setColor(String color) { this.color = color; return this; }
    public ShapeBuilder setFilled(boolean isFilled) { this.isFilled = isFilled; return this; }

    public Shape buildCircle(double radius) { return new Circle(radius, color, isFilled); }
    public Shape buildRectangle(double width, double height) { return new Rectangle(width, height, color, isFilled); }
}

// Director : orchestre la construction
class ShapeDirector {
    private ShapeBuilder builder;

    public ShapeDirector(ShapeBuilder builder) {
        this.builder = builder;
    }

    // Créer un cercle avec un ordre spécifique
    public Shape createCircle() {
        return builder.setColor("Red").setFilled(true).buildCircle(5.0);
    }

    // Créer un rectangle avec un ordre spécifique
    public Shape createRectangle() {
        return builder.setColor("Blue").setFilled(false).buildRectangle(10.0, 4.0);
    }
}

// Classe principale
public class Main {
    public static void main(String[] args) {
        ShapeBuilder builder = new ShapeBuilder();
        ShapeDirector director = new ShapeDirector(builder);

        // Le Director utilise le Builder pour créer les objets dans un ordre spécifique
        Shape circle = director.createCircle();
        circle.draw();
        
        Shape rectangle = director.createRectangle();
        rectangle.draw();
    }
}
```

<img src="/home/abder/Desktop/notes_/programming/builder.png" alt="20" style="zoom:80%;" />

### Prototype :

Le **Prototype** est un design pattern qui permet de créer de nouveaux objets en clonant des objets existants, plutôt qu'en créant des objets à partir de zéro. Cela peut être utile pour des objets qui sont coûteux à créer ou pour des configurations spécifiques que l'on veut dupliquer rapidement.

Voici un exemple simple de **Prototype** en Java :

```java
// Prototype : Shape
abstract class Shape implements Cloneable {
    protected String color;
    
    public abstract void draw();

    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();  // Effectue un clonage superficiel
    }
}

class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        this.color = color;
        this.radius = radius;
    }

    @Override
    public void draw() {
        System.out.println("Drawing Circle with radius " + radius + " and color " + color);
    }
}

class Rectangle extends Shape {
    private double width, height;

    public Rectangle(String color, double width, double height) {
        this.color = color;
        this.width = width;
        this.height = height;
    }

    @Override
    public void draw() {
        System.out.println("Drawing Rectangle with width " + width + ", height " + height + " and color " + color);
    }
}

// Client (Main) - Utilisation du Prototype
public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        // Création d'un prototype original
        Shape originalCircle = new Circle("Red", 5.0);
        Shape originalRectangle = new Rectangle("Blue", 10.0, 4.0);

        // Clonage des objets prototypes
        Shape clonedCircle = (Shape) originalCircle.clone();
        Shape clonedRectangle = (Shape) originalRectangle.clone();

        // Affichage des objets clonés
        clonedCircle.draw();
        clonedRectangle.draw();
    }
}
```

<img src="/home/abder/Desktop/notes_/programming/prototype.png" alt="20" style="zoom:80%;" />

### Singleton :

Le **Singleton** est un design pattern qui garantit qu'une classe n'ait qu'une seule instance et fournit un point d'accès global à cette instance. Ce pattern est utilisé lorsque vous souhaitez contrôler l'accès à une ressource partagée, comme une connexion à une base de données ou un gestionnaire de configuration, pour éviter des créations multiples de la même instance.

#### **Caractéristiques du Singleton** :

1. **Instance unique** : La classe ne possède qu'une seule instance.
2. **Accès global** : Il fournit une méthode pour accéder à cette instance.

#### Exemple

```java
// Singleton : Logger
class Logger {
    private static Logger instance;

    // Le constructeur est privé pour empêcher l'instanciation externe
    private Logger() {}

    // Méthode pour obtenir l'instance unique
    public static Logger getInstance() {
        if (instance == null) {
            instance = new Logger();  // Crée l'instance si elle n'existe pas
        }
        return instance;
    }

    // Méthode pour enregistrer un message
    public void log(String message) {
        System.out.println("Log: " + message);
    }
}

// Utilisation du Singleton dans le programme
public class Main {
    public static void main(String[] args) {
        // Obtenir l'instance unique du Logger
        Logger logger1 = Logger.getInstance();
        Logger logger2 = Logger.getInstance();

        // Vérifier que les deux références pointent vers la même instance
        System.out.println("logger1 et logger2 sont-ils identiques ? " + (logger1 == logger2));

        // Utiliser le logger
        logger1.log("Application started");
        logger2.log("Logging an event");
    }
}
```

