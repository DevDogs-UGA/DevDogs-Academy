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

Achieving dependency injections through configuration
- XML configuration (using Component)
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

- Annotation based configuration * (Components, Autowired)
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

- Combo Annotation & Xml w/ Bean property tags
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

- Constructor Injection (Still mixed Annotation and Xml Config) & Autowired
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

- Annotation Confirguation using Maven (New Example)
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
- Annotation Component (AutoWird Primary Qualifier)
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

