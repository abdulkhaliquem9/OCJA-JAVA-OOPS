# OCJA-JAVA-OOPS
OCJA notes


# Object Oriented programming (OOPs) Concepts in Java || by Durga sir
# ====================================================================
Note 1: Parent object can hold referrence of child object.
	Example: 

- java classes without public classes can be created with any file name.
- for each class in a single file .class file is generated.
- java class with public class should have the name of the class and file name to be same.
- 



## Implicit & Explicit imports
- No need to import java.lang and Default package classes
- All classes and interfaces present inside an imported class will be available,
  but not the nested level classes and interfaces of the the imported class's classes & interfaces.
  For example, 
	java ----
		| - util
		|	 | -  regex
		|	 |		| - pattern
  The classes & interfaces of java.* will import the classes & interfaces inside java package but not of java.util package, 
  we need to explicitly import java.util package's classes & interfaces
  
  import java.*;
  Pattern p = Pattern.compile("ab"); // throws error
  
  import java.util.regex.*
  Pattern p = Pattern.compile("ab"); // compiles fine

## Packages
- around 5000+ packages of java are well packaged & grouped.
- group of related things (classes & interfaces) is a package.
  It is an encapsulation mechanism.
  java.sql is related to DB
  java.io is related to I/O
- Naming conflicts can be resolved with packages.
  Readability, security, modularity, maintainability is achieved.
	java.sql.Date
	java.util.Date
- Package statement must be first statement in the program.
- use Internet domain name of client in reverse to name the packages.
	com.infosys.ocja
- destination to place generated .class files option is -d
  Compile:> javac -d . Test.java
  Run:> java com.infosys.ocja.Test.java
  Dot (.) will compile in current working directory(cwd)
  For example:
  com.infosys.ocja;
  class Test{}
  cwd
	|
	| - com
    |    | - infosys
	|    |     | - ocja
	|    | 	   |	  | - Test.class
Note 2: If we mention 2 packages in a file the compile Error occurs as only atmost one (1) package is allowed in a file.
	Error: class, interface or enum is expected but got <second package name>

Order of program
	package statement (Atmost one 0 or 1)
	import statements
	class | interface | enum

## Class Level Modifiers
- we have to specify some info about our class to JVM by using Access Modifiers.
  default (if noting is specified, package level class)  - with in the package
  abstract - Instantiation is not possible
  final - child class creation is not possible
  
- Access modifiers for Top Level classes are
	public, default, abstract, final, strictfp
- Access modifiers for nested classes are
	public, default, abstract, final, strictfp, private, protected, static

	public classes can be accessed from any where
	package pack1;
	public class A {} // accessible in any package
	classB 		// only accessed within the same package pack1.
	
	package pack2;
	import pack1.A;
	import pack1.B;
	class B {
	A a = new A();
	B b = new B(); // Error: B is not public in pack1; cannot be accessed from outside package.
	}

### - abstract Modifier is applicable only for class & methods only, but not for variables.
    - abstract methods 
	- are not implemented & has declaration but not implementation; child classes are responsible to provide implementation.
		abstract public class Vehicle{
			public drive(){}; // implemented  
			public abstract int getNoOfWheels(); // not implemented
		}
Note 3: Abstract class - If a class contains any abstract method then the class should be declared as an abstract class.

	- abstract class
		- partially implemented classes or a class with any abstract method should be declared as an abstract class.
		- are not instantiated or object cannot be created.
		Note 4: class can be declared as abstract even if there is no abstract method.
		 HttpServlet, Adapter classes has dummy implementation of methods and is an abstract class.
		 Example: 
		 public abstract class Test {
			......
			public void add(){};
			public void sub(){};
			public abstract doSomething(); // abstract method not implemented
		 }
		 Error: Test is abstract; cannot be instantiated
				Test t = new Test();
		
### Abstract class vs Abstract method (2:17:06)
- the advantage of declaring abstract methods in the Abstract class is to make the child class
  to provide the implementation without miss.
  If we don't declare abstract method in the parent class then the child class may or may not implement
  the implementation.
- Child class extending Abstract class should implement all the abstract methods, else we have
  to declare the child class as abstract.

## Member Modifier (variables and methods) (2::32: 15)
   
   private < default < protected < public (severity of access level restrictions).
   
- Public member: if a member is public then it can be accessed from any where; across classes and packages.
	Note 5: Even though member is public but the corresponding class is not public then we can't access the public memebers.

	Example:
	package pack1;
	class A {  // class is not public
		public void m1(){} // member is public
	}
	
	package pack2;
	import pack1.A;
	class B {
		public static void main(string args[]){
		A a = new A(); // Error: A is not public; cannot be accessed from outside package pack1.
		a.m1();
		}
	}
	compile: javac -d . B.java
	run: java pack2.B      // give fully qualified class name
	
- Default Member is only accessible within the corresponding package. (2:41:00)
	Example: class A {
		void m1(){}; // default modifier is added to m1
	}
	Error: m1() is not public in A; cannot be accessed from outside package.
	
- Private member is accessible only within the same class(2:44:00)
	private member is a class level member, 
	Note 6: highly recommended modifier for variables. where as recommended modifier for method is public.
	Example: 
		class A {
			private void m1(){}
		}
		class Test {
			public static void main(string args[]){
				A a = new A();
				a.m1(); // Error: m1() has private access in A. cannot be accessed from the outside class.
			}
		}
 - Protect member can be accessed from any where with in the current package (2:50:00).
  But from outside package it is accessed only in child classes (kids / extended classes).
  protected = default + kids (child / extended classes of other package)
  
  Note 7: In child class of other package protected methods can be accessed 
		the referrence of that respective child class only.
  
  Example: parent & child with in the same package pack1.
  package pack1;
  class A {
	protected void m1() {
		sout('A class protected mehtod m1()');
	};
  }
  class B extends A{
	public static void main(string args[]){
		A a = new A();
		a.m1();
		B b = new B();
		b.m1();
		
		A a1 = new B(); // Parent object A can hold referrence of child object B.
		a1.m1();
	}
  }
  
  Compile: javac -d . A.java
  Run: java pack1.B
  
  Example: parent & child with in the different packages pack1 & pack2.
  package pack1;
  class A {
	protected void m1() {
		sout('A class protected mehtod m1()');
	};
  }
  
  package pack2;
  import pack1.A;
  class B extends A{
	public static void main(string args[]){
		A a = new A(); // Error: m1() has protected access in A, a.m1();
		a.m1();
		
		B b = new B(); // Note 7: only child class B can access protected m1 of parent A.
		b.m1();
		
		A a1 = new B(); // Error: m1() has protected access in A, a1.m1();
		a1.m1();
	}
  }
  
## Interface (Service Requirement Specifications - SRS)
For Example, the Servlet API interface implementation of SUN Microsystem need to be implemented
by the web servers like Tomcat, Jetty, Resin, 
- Every method in an interface is public and abstract so the implementation has to have a public
  modifier in the child class (service provider), Other wise we'll get an error
  
  Error: m1() in ServiceProvider(class) cannot implement void m1(), attemting to assign weaker 
  access privileges; was public.
- Every method has to be implemented by the ServiceProvider(class), other wise error will occur
  Error: ServiceProvider is not abstract and does not override abstract method m2() in Intref(interface).
  
  Example:
	interface Intref{
		public void m1();
		public void m2();
	}
	class ServiceProvider implements Intref{
		public void m1(){};
		public void m2(){};
	}
Note 9: If we are not implementing all the methods in ServiceProvider then this class has to be declared as an abstract class.
	xample:
	interface Intref{
		public void m1();
		public void m2();
	}
	abstract class ServiceProvider implements Intref{ //declaring abstract class
		public void m1(){};
	}
	class SubServiceProvider extends serviceProvider{
		public void m2();
	}
		

				   	SUN
					|
				Servlet API (interface)
					|
			________________|_________________________________________________
			|			| 			|		|
			Tomcat			Resin			Jetty		Web Logic

Another example is that the DataBase vendors like MySQL, Oracle, Postgres etc., need to implement
the JDBC API interface in their respective drivers in order to communicate with Java application.

						JAVA APP
						|
					JDBC API (Interface)
						|
	________________________________________________________________________________________________________________________
	|					|						|				|
    Oracle Driver				MySQL Driver					PostGres Driver
	
- Any requirement specification / any contract between client and the service provider acts as an
interface.
Note 8: From JAVA 1.9; An interface can have public, private, default, static members.


			  SERVICE REQUIREMENTS
			   | --- m1(); --- |
			   | --- m2(); --- |
	Client---->| --- m3(); --- |<---- Service Provider (interface implementor)
			   |    .	   --- |
			   |    .	   --- |
			   
			  
## Data Hiding (OOPS) (3:47:40)

