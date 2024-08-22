# Spring Overview
This overview was created from notes following 2 youtube tutorials (links provided later in the article) and Spring tutorial articles

## Prerequisites
- Must have a solid understanding of Java and OOP (particularly interfaces)

## IoC
Inversion of control (IoC) is a **principle** where the control of creating objects (in this case) is given to something (Ex. Spring Framework) other than the developer. In Spring this is done through a **design pattern** called dependency injection

## DI
Dependency injection in Spring 
- Constructor injection
- Setter injection
- Field injection (Not recommended)
    - Loose coupling (code for interfaces)

## Coupling
Coupling: How much work is involved in changing something?
- Tightly coupled: Engine to a car, Computer to your house (harder to move)
- Loosely coupled: Tire to a car, laptop to your house (can take anywhere)
* In software, loosely coupled is often better as code is always changing and iterating to better versions

Tightly coupled code:
SuperMario mario = new SuperMario();
GameRunner runner = new GameRunner(mario);
// GameRunner can only run mario games, and code needs to be changed within GamerRunner to run others

Loosely coupled code:
* GamingConsole is an interface
GameingConsole game1 = new SuperMario();
GameingConsole game2 = new PacMan();
GameRunner runner = new GameRunner(game1);
GameRunner runner = new GameRunner(game2);
// Because all games must implement the GameingConsole interface, GameRunner can accept any GameingConsole object in the constructor

## Spring Container/Context (IoC Container)
(is within JVM [Java Virutal Machine])
- Manages Spring beans & their lifecycle
- Bean Factory: Basic Spring Container (Not really used)
- **Application Context**: Advanced Spring Container w/ enterprise-specific features
    - Good for web apps, web services, REST API, and microservices
    - Easy internationalization
    - Easy integration with Spring AOP (Aspect oriented programming)

### POJO: Plain Old Java Object
- No constraints
- Any Java Object is a POJO

### Spring Bean: Any Java Object managed by Spring
- Spring uses IoC Container (Ex. Application Context) to manage these objects

Tutorial References (Highly recommend watching!)
- https://www.youtube.com/watch?v=f6DHAgL7FWc (More beginner friendly, decent examples, not as concise)
- https://www.youtube.com/watch?v=If1Lw4pLLEo (Fast, comprehensive, good examples) [Also has a more recentt playlist making an example project with Spring and Springboot]
I watched the 2nd one first, and put the 1st on 1.5x to review.

# Gen Topics
- IoC containers (Inversion of Control)
- Data access framework
- Dependency injections
    - Injecting object dependencies

- Maven
    - Maven Project, Maven archetypes
    - Group ID / Artifact ID
    - pom.xml file
    - Maven repository for xml dependencies

### Achieving dependency injections through configuration
#### XML configuration (using Component)
    ex.
    App.java
    public class App {
        public static void main(String[] args) {
            ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml") // Your own xml file and file name

            Vehicle obj = (Vehicle)context.getBean("vehicle");
            obj.drive();
        }
    }
    spring.xml (in src)
    <?xml version="1.0" encoding="UTF-8"?>

    <beans [xml custom tag definition here, can find on spring website]>
        <bean id="vehicle" class="com.navin.Telusko.Car"></bean>
    </beans>

#### Annotation based configuration * (Components, Autowired)
    ex.
    App.java
    public class App {
        public static void main(String[] args) {
            ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml") // Your own xml file and file name

            Vehicle obj = (Vehicle)context.getBean("car");
            obj.drive();
        }
    }
    spring.xml (in src)
    <?xml version="1.0" encoding="UTF-8"?>

    <beans [xml custom tag definition here, can find on spring website]>
       <context:component-scan base-package='com.navin.Telusko'></context:component-scan> 
    </beans>

    Car.java
    package com.navin.Telusko;
    @Component // <- important
    public class Car implements Vehicle {
        public void drive() {
            System.out.println("driving");
        }
    }

#### Combo Annotation & Xml w/ Bean property tags
    ex.
    App.java
    public class App {
        public static void main(String[] args) {
            ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml") // Your own xml file and file name

            Tire t = (Tire) context.getBean("tire");
            System.out.println(t);
        }
    }
    spring.xml (in src)
    <?xml version="1.0" encoding="UTF-8"?>

    <beans [xml custom tag definition here, can find on spring website]>
       <context:component-scan base-package='com.navin.Telusko'></context:component-scan> 
        // Xml formatting to accomodate tire
       <bean id="tire" class="com.navin.Telusko.Tire">
            <property name="brand" value="MRF"></property>
       </bean>
    </beans>

    Car.java
    package com.navin.Telusko;

    @Component // <- important
    public class Car implements Vehicle {
        public void drive() {
            System.out.println("driving");
        }
    }

    Tire.java
    package com.navin.Telusko;

    public class Tire {
        private String brand;

        public String getBrand() {
            return brand;
        }

        public void setBrand(String brand) {
            this.brand= brand;
        }

        @Override
        public String toString() {
            return "Tire [brand=" + brand + "]";
        }
    }

#### Constructor Injection (Still mixed Annotation and Xml Config) & Autowired
    ex.
    App.java
    public class App {
        public static void main(String[] args) {
            ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml") // Your own xml file and file name

            Car obj = (Car)context.getBean("car");
            obj.drive();
        }
    }
    spring.xml (in src)
    <?xml version="1.0" encoding="UTF-8"?>

    <beans [xml custom tag definition here, can find on spring website]>
       <context:component-scan base-package='com.navin.Telusko'></context:component-scan> 
        // Xml formatting to accomodate tire
       <bean id="tire" class="com.navin.Telusko.Tire">
            <constructor-arg value="MRF"></constructor-arg>
       </bean>
    </beans>

    Car.java
    package com.navin.Telusko;

    @Component // <- important
    public class Car implements Vehicle {

        @Autowired
        private Tire tire;

        public Tire getTire() {
            return tire
        }

        public void setTire(Tire tire) {
            this.tire = tire;
        }

        public void drive() {
            System.out.println("car" + tire);
        }
    }

    Tire.java
    package com.navin.Telusko;

    @Component
    public class Tire {
        private String brand;

        public Tire(String brand) {
            super();
            this.brand = brand;
        }

        public String getBrand() {
            return brand;
        }

        public void setBrand(String brand) {
            this.brand= brand;
        }

        @Override
        public String toString() {
            return "Tire [brand=" + brand + "]";
        }
    }

#### Annotation Confirguation using Maven (New Example)
    1. Create Maven project (Quick start maven archetype)
    2. Add dependencies to pom.xml from Maven Repository
        - Spring context copy and paste
    Samsung.java
    package com.telusko.SpringAnno;


    public class Samsung {

        @Autowired // checks by type
        MobileProcessor cpu;

        public MobileProcessor getCpu() {
            return cpu;
        }

        public void setCpu(MobileProcessor cpu) {
            this.cpu = cpu;
        }

        public void config() {
            System.out.println("Octa Core, 4 gb Ram, 12MP camera");
            cpu.process();
        }
    }

    App.java
    package com.telusko.SpringAnno;

    public class App {
        public static void main(String[] args) {
            ApplicationContext factory = new AnnotationConfigApplicationContext(AppConfig.class);

            Samsung s7 = factory.getBean(Samsung.class);
            s7.config();
        }
    }

    AppConfig.java
    package com.telusko.SpringAnno;

    // import statements auto inserted here

    @Configuration
    public class AppConfig {

        @Bean
        public Samsung getPhone() {
            return new Samsung();
        }
        @Bean
        public MobileProcessor getProcessor() {
            return new Snapdragon();
        }

    }

    MobileProcessor.java
    package com.telusko.SpringAnno;

    public interface MobileProcessor {
        void process();
    }

    Snapdragon.java
    package com.telusko.SpringAnno;

    public class Snapdragon implements MobileProcessor {
        public void process() {
            System.out.println("Word's best CPU");
        }
    }
#### Annotation Component (AutoWird Primary Qualifier)
    1. Add Component tags to Samsung and Snapdragon
    2. Add ComponentScan to AppConfig to find components (it looks by type)
        - defaults to class name decapitalized (Samsung->samsung)
        - With multiple components, you can define a primary (@Primary) or a qualifier (@Qualifier("id"))
        - 
    Samsung.java
    package com.telusko.SpringAnno;

    @Component
    public class Samsung {

        @Autowired // checks by type
        @Qualifier("snapdragon")
        MobileProcessor cpu;

        public MobileProcessor getCpu() {
            return cpu;
        }

        public void setCpu(MobileProcessor cpu) {
            this.cpu = cpu;
        }

        public void config() {
            System.out.println("Octa Core, 4 gb Ram, 12MP camera");
            cpu.process();
        }
    }

    App.java
    package com.telusko.SpringAnno;

    // Spring Core Annotations
    public class App {
        public static void main(String[] args) {
            ApplicationContext factory = new AnnotationConfigApplicationContext(AppConfig.class);

            Samsung s7 = factory.getBean(Samsung.class);
            s7.config();
        }
    }

    AppConfig.java
    package com.telusko.SpringAnno;

    // import statements auto inserted here

    @Configuration
    @ComponentScan(basePackages="com.telusko.SpringAnno")
    public class AppConfig {

    }

    MobileProcessor.java
    package com.telusko.SpringAnno;

    public interface MobileProcessor {
        void process();
    }

    Snapdragon.java
    package com.telusko.SpringAnno;

    // importing Component

    @Component
    @Primary
    public class Snapdragon implements MobileProcessor {
        public void process() {
            System.out.println("Word's best CPU");
        }
    }

    MediaTek.java
    package com.telusko.SpringAnno;

    // importing Component

    @Component
    public class MediaTek implements MobileProcessor {
        public void process() {
            System.out.println("2nd best CPU");
        }
    }

### Another Example of implementing Spring -> Hello World Application

App.java
package ...

imports

public class App {
    public static void main(String[] args) {
        // 1: Launch a Spring Context
        try(var context = new AnnotationConfigApplicationContext(AppConfig.class)) {
            // 2: Configure the things we want Spring to manage - @Configuration
            context.getBean(GamingConsole.class).up();

            context.getBean(GameRunner.class).run();
        }
        

        
        System.out.println(context.getBean("name")); // Returns "Jenn"
        System.out.println(context.getBean("address")) // Returns error, we renamed address -> address2

        System.out.println(context.getBean(Address.class)) // Can use type of Bean
        
        
    }
}

AppConfig.java
package ...

imports

record Person (String name, int age) {};
record Address (String firstLine, String city) {};

public class AppConfig {

    @Bean
    public GamingConsole game() {
        var game = new PacmanGame();
        return game;
    }

    @Bean
    public GameRunner gameRunner(GamingConsole game) {
        var gameRunner = new GameRunner(game);
        return game;
    } // Can also change new GameRunner(game) -> new GameRunner(game()) with no parameters
}

## Tips

#### List all Spring Beans
// Prints the list out to System, the :: is a method reference
// Some internal Spring Beans will be listed alongside your own defined Beans
Arrays.stream(context.getBeanDefinitionNames()).forEach(System.out::println);

## More Resources
- https://www.javatpoint.com/spring-tutorial
- https://www.baeldung.com/spring-tutorial
- https://www.geeksforgeeks.org/spring/
