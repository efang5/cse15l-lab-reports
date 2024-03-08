# Lab Report 5
## Part 1

1. The original post from a student with a screenshot showing a symptom and a description of a guess at the bug/some sense of what the failure-inducing input is. (Don't actually make the post! Just write the content that would go in such a post)

My code for Sanctuary.java does not compile properly.
<br>Here is my code.
```
/**
 * This file contains all methods for Sanctuary
 */
import java.util.Objects;
import java.util.Map;
import java.util.HashMap;
import java.util.Set;
import java.util.HashSet;
import java.util.Collections;
import java.util.ArrayList;
import java.util.Iterator;

/**
 * This class contains all methods for Sanctuary.
 */
public class Sanctuary {
    //class variables for sanctuary
    HashMap<String, Integer> sanctuary;
    private final int maxAnimals;
    private final int maxSpecies;

    /**
     * constructor for sanctuary sets maxAnimals and maxSpecies to the 
     * given input and makkes a new empty hashmap for sanctuary
     */
    public Sanctuary(int maxAnimals, int maxSpecies){
        if(maxAnimals <= 0 || maxSpecies <= 0 || maxSpecies > maxAnimals){
            throw new IllegalArgumentException();
        }
        this.maxAnimals = maxAnimals;
        this.maxSpecies = maxSpecies;
        this.sanctuary = new HashMap<>();
    }

    /**
     * returns the number of animals for a given species
     * @return the number of animals of the given species
     */
    public int countForSpecies(String species){
        if(species == null){
            throw new IllegalArgumentException();
        }
        if(!this.sanctuary.containsKey(species)){
            return 0;
        }
        return this.sanctuary.get(species);
    }

    /**
     * returns the number of animals in that sanctuary
     * @return the number of animals in the sanctuary
     */
    public int getTotalAnimals(){
        int count = 0;
        Set keys = this.sanctuary.keySet();
        for(Object key: keys){
            count += this.sanctuary.get(key);
        }
        return count;
    }

    /**
     * returns the number of species for a given sanctuary
     * @return the number of species of the given sanctuary
     */
    public int getTotalSpecies(){
        int count = 0;
        Set keys = this.sanctuary.keySet();
        for(Object key: keys){
            count ++;
        }
        return count;
    }

    /**
     * returns the max number of animals for a given sanctuary
     * @return the max number of animals of the given sanctuary
     */
    public int getMaxAnimals(){
        return this.maxAnimals;
    }

    /**
     * returns the max number of species for a given sanctuary
     * @return the max number of species of the given sanctuary
     */
    public int getMaxSpecies(){
        return this.maxSpecies;
    }

    /**
     * rescues as many animals as possible adding them to the sanctuary
     * and returns the number of animals not saved
     * @return the number of animals not saved
     */
    public int rescue(String species, int num){
        int unsaved = 0;
        if(num <= 0 || species == null){
            throw new IllegalArgumentException();
        }
        if((this.getMaxSpecies() == this.getTotalSpecies() && 
        !this.sanctuary.containsKey(species)) || 
        this.getMaxAnimals() == this.getTotalAnimals()){
            return num;
        }
        this.sanctuary.put(species, (this.countForSpecies(species) + num));
        while (this.getTotalAnimals() > this.getMaxAnimals()){
            this.sanctuary.put(species, (this.countForSpecies(species) - 1));
            unsaved++;

        }
        return unsaved;
    }

    /**
     * release a given number of animals from the sanctuary
     */
    public void release(String species, int num){
        if(num <= 0 || species == null || 
        num > this.countForSpecies(species) || 
        !this.sanctuary.containsKey(species)){
            throw new IllegalArgumentException();
        }
        if((this.countForSpecies(species) - num) == 0){
            this.sanctuary.remove(species);
        }
        else{
            this.sanctuary.put(species, (this.countForSpecies(species) - num));
        }
    }
}

    /**
     * rescues as many animals as possible adding them to the sanctuary from
     * the closingSanctuary and returns the number of animals saved
     * @return the number of animals saved
     */
    public int helpClosingSanctuary(Sanctuary closingSanctuary)    {
        int saved = 0;
        if(closingSanctuary ==null){
            throw new IllegalArgumentException();
        }
        if(this.getMaxAnimals() == this.getTotalAnimals()){
            return 0;
        }
        Set<String> closingSpecies = closingSanctuary.sanctuary.keySet();
        ArrayList<String> speciesArray = new ArrayList<>();
        for (String specie: closingSpecies){
            speciesArray.add(specie);
        } 
        Collections.sort(speciesArray);
        for(String specie: speciesArray){
            int tryToSave = closingSanctuary.countForSpecies(specie);
            int fail = this.rescue(specie, 
            closingSanctuary.countForSpecies(specie));
            closingSanctuary.sanctuary.put(specie, fail);
            if(fail == 0){
                closingSanctuary.sanctuary.remove(specie);
            }
            saved += tryToSave - fail;
        }
        return saved;
    }
}
```
Here is my javac results.
```
Sanctuary.java:139: error: class, interface, enum, or record expected
    public int helpClosingSanctuary(Sanctuary closingSanctuary) {
           ^
Sanctuary.java:141: error: class, interface, enum, or record expected
        if(closingSanctuary ==null){
        ^
Sanctuary.java:143: error: class, interface, enum, or record expected
        }
        ^
Sanctuary.java:146: error: class, interface, enum, or record expected
        }
        ^
Sanctuary.java:148: error: class, interface, enum, or record expected
        ArrayList<String> speciesArray = new ArrayList<>();
        ^
Sanctuary.java:149: error: class, interface, enum, or record expected
        for (String specie: closingSpecies){
        ^
Sanctuary.java:151: error: class, interface, enum, or record expected
        } 
        ^
Sanctuary.java:153: error: class, interface, enum, or record expected
        for(String specie: speciesArray){
        ^
Sanctuary.java:155: error: class, interface, enum, or record expected
            int fail = this.rescue(specie, 
            ^
Sanctuary.java:157: error: class, interface, enum, or record expected
            closingSanctuary.sanctuary.put(specie, fail);
            ^
Sanctuary.java:158: error: class, interface, enum, or record expected
            if(fail == 0){
            ^
Sanctuary.java:160: error: class, interface, enum, or record expected
            }
            ^
Sanctuary.java:162: error: class, interface, enum, or record expected
        }
        ^
Sanctuary.java:164: error: class, interface, enum, or record expected
    }
```

2. A response from a TA asking a leading question or suggesting a command to try (To be clear, you are mimicking a TA here.)
<br>Try checking the Problems section on VSCode and see if it gives you a better idea of the issue.

3. Another screenshot/terminal output showing what information the student got from trying that, and a clear description of what the bug is.
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-03-08%20at%208.37.11%20AM.png?raw=true)

4. At the end, all the information needed about the setup including:
<br>The file & directory structure needed
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-03-08%20at%208.37.35%20AM.png?raw=true)
<br>The contents of each file before fixing the bug
settings.json
```
{
    "java.debug.settings.onBuildFailureProceed": true
}
```
Course.java
```
/**
 * This file contains all methods for courses
 */
import java.util.Objects;
import java.util.Map;
import java.util.HashMap;
import java.util.Set;
import java.util.HashSet;
import java.util.Collections;
import java.util.ArrayList;
import java.util.Iterator;

/**
 * This class contains all methods for Course.
 */
public class Course {

    //class variables for course
    HashSet<Student> enrolled;
    private final int capacity;
    private final String department;
    private final String number;
    private final String description;

    /**
     * constructor for course sets department, number, description, 
     * and capacity to the given value 
     * and making a new empty haseset for enrolled
     */
    public Course(String department, String number, String description, 
    int capacity){
        if(department == null || number == null 
        || description == null || capacity <= 0){
            throw new IllegalArgumentException();
        }
        this.department = department;
        this.number = number;
        this.description = description;
        this.capacity = capacity;
        this.enrolled = new HashSet<>();
    }

    /**
     * returns the department of the course
     * @return the department
     */
    public String getDepartment(){
        return this.department;
    }

    /**
     * returns the number of the course
     * @return the number
     */
    public String getNumber(){
        return this.number;
    }

    /**
     * returns the desscription of the course
     * @return the description
     */
    public String getDescription(){
        return this.description;
    }

    /**
     * returns the capacity of the course
     * @return the capcity
     */
    public int getCapacity(){
        return this.capacity;
    }

    /**
     * enrolls the given student into the course
     * @return whether the student was sucessfully added
     */
    public boolean enroll(Student student){
        if (student == null){
            throw new IllegalArgumentException();
        }
        if(this.isFull()){
            return false;
        }
        if(this.enrolled.contains(student)){
            return false;
        }
        this.enrolled.add(student);
        return true;
    }

    /**
     * drops the given student from the course
     * @return whether the student was sucessfully dropped
     */
    public boolean drop(Student student){
        if (student == null){
            throw new IllegalArgumentException();
        }
        if(this.enrolled.contains(student)){
            this.enrolled.remove(student);
            return true;
        }
        return false;
    }

    /**
     * empties the course of all enrolled students
     */
    public void cancel(){
        this.enrolled.clear();
    }

    /**
     * returns whether the course is full or not
     * @return whether the course is at capacity
     */
    public boolean isFull(){
        return this.enrolled.size() == capacity;
    }

    /**
     * returns the number of enrolled students
     * @return the number of enrolled students
     */
    public int getEnrolledCount(){
        return this.enrolled.size();
    }

    /**
     * returns the number of seats availiable in the course
     * @return the number of seats availiable
     */
    public int getAvailableSeats(){
        return capacity - this.getEnrolledCount();
    }

    /**
     * returns a hashset of all the students enrolled in the course
     * @return all of the students enroleld in the course
     */
    public HashSet<Student> getStudents(){
        return (HashSet<Student>) this.enrolled.clone();
    }

    /**
     * returns an arraylist of all the students enrolled in the course
     * @return all of the students enroleld in the course
     */
    public ArrayList<Student> getRoster(){
        ArrayList<Student> enrolledArray = new ArrayList<>();
        for(Student student: this.enrolled){
            enrolledArray.add(student);
        }
        Collections.sort(enrolledArray);
        return enrolledArray;
    }

    /**
     * toString method to set the format when printing a course
     * @return the format for the string for course
     */
    public String toString(){
        String string = this.getDepartment() + " " + this.getNumber() + 
        " [" + this.getCapacity() + "] " + this.getDescription();
        return string;
    }
}
```
CustomTester.java
```
/**
 * This file contains all custom tests
 */

import java.util.Objects;
import java.util.Map;
import java.util.HashMap;
import java.util.Set;
import java.util.HashSet;
import java.util.Collections;
import java.util.ArrayList;
import java.util.Iterator;
import org.junit.Test;
import static org.junit.Assert.*;

/**
 * This class contains test cases for Sanctuary, Course, and Student.
 */
public class CustomTester {
    /**
     * Aims to test the equals() method for students when the 
     * input is not a student
     */
    @Test
    public void testStudentEquals() {
        Student student1 = new Student("Test", "Student",
                "A12345678");
        String student2 = "hi";
        assertEquals(false, student1.equals(student2));
    }

    /**
     * Aims to test the compareTo() method for students
     */
    @Test
    public void testStudentCompareTo() {
        Student student1 = new Student("Test", "Student",
                "A12345678");
        Student student2 = new Student("Test", "Student",
                "A12345679");
        assertEquals(-1, student1.compareTo(student2));
    }

    /**
     * Aims to test the drop() method for students 
     * when the given student is not in the course
     * when there are students in the course
     */
    @Test
    public void testCourseDrop(){
        Course course = new Course("math", "A10", 
        "alpha", 10);
        Student student1 = new Student("Test", "Student",
                "A12345678");
        Student student2 = new Student("Test", "Student",
                "A12345679");
        course.enrolled.add(student1);
        assertEquals(false, course.drop(student2));
        assertEquals(true, course.enrolled.contains(student1));
    }

    /**
     * Aims to test the enroll() method for course when the course is full
     */
    @Test
    public void testCourseEnroll(){
        Course course = new Course("math", "A10", 
        "alpha", 1);
        Student student1 = new Student("Test", "Student",
                "A12345678");
        Student student2 = new Student("Test", "Student",
                "A12345679");
        course.enrolled.add(student1);
        assertEquals(false, course.enroll(student2));
        assertEquals(true, course.enrolled.contains(student1));
        assertEquals(1, course.getCapacity());
    }
    
    /**
     * Aims to test the getRoster() method for course when there 
     * are many students
     */
    @Test
    public void testCourseGetRoster(){
        Course course = new Course("math", "A10", 
        "alpha", 100);
        ArrayList<Student> students = new ArrayList<>();
        Student newStudent;
        for(int i = 0; i < 100; i++){
            newStudent = new Student ("fname", 
            "lname", ("A" + (100 - i)));
            students.add(newStudent);
            course.enrolled.add(newStudent);
        }
        Collections.sort(students);
        assertEquals(students, course.getRoster());
    }

    /**
     * Aims to test the sanctuary constructor when the max animals is 
     * negative
     */
    @Test
    public void testSanctConstructor(){
        assertThrows(IllegalArgumentException.class, () -> {
            Sanctuary sanc = new Sanctuary(-1, 5);
        });
    }

    /**
     * Aims to test the rescue method for sanctuary when there are
     *  more animals to be saved then space availiable
     */
    @Test
    public void testSanctRescuePartial(){
        Sanctuary sanc = new Sanctuary(10, 5);
        assertEquals(5, sanc.rescue("dog", 15));
        assertEquals(1, sanc.getTotalSpecies());
        assertEquals(10, sanc.getTotalAnimals());
    }

    /**
    * Aims to test the rescue method for sanctuary when the 
    number of species is max and are trying yo rescue a new species
    */
    @Test
    public void testSanctRescueMaxSpecies(){
        Sanctuary sanc = new Sanctuary(5, 1);
        sanc.rescue("dog", 5);
        assertEquals(5, sanc.rescue("cat", 5));
        assertEquals(5, sanc.getTotalAnimals());
        assertEquals(1, sanc.getTotalSpecies());
    }

    /**
     * Aims to test the release method for sanctuary
     */
    @Test
    public void testSanctReleasePartial(){
        Sanctuary sanc = new Sanctuary(5, 1);
        sanc.rescue("dog", 5);
        sanc.release("dog", 3);
        assertEquals(2, sanc.getTotalAnimals());
        assertEquals(1, sanc.getTotalSpecies());
    }

    /**
     * Aims to test the release method for sanctuary when there are 
     * more animals to be released then there are in the sanctuary
     */
    @Test
    public void testSanctReleaseTooMany(){
        Sanctuary sanc = new Sanctuary(5, 1);
        sanc.rescue("dog", 3);
        assertThrows(IllegalArgumentException.class, () -> {
            sanc.release("dog", 5);
        });
    }

    /**
     * Aims to test the helpClosingSanctuary method for sanctuary when there are 
     * more animals to be saved from the closing sanctuary 
     * then there is space in the helping sanctuary
     */
    @Test
    public void testSanctHelpClosingSanctuaryPartial(){
        Sanctuary sanc1 = new Sanctuary(10, 1);
        Sanctuary sanc2 = new Sanctuary(5, 1);
        sanc1.sanctuary.put("dog", 8);
        sanc2.sanctuary.put("dog", 4);
        assertEquals(2, sanc1.helpClosingSanctuary(sanc2));
        assertEquals(10, sanc1.getTotalAnimals());
        assertEquals(1, sanc1.getTotalSpecies());
        assertEquals(2, sanc2.getTotalAnimals());
        assertEquals(1, sanc2.getTotalSpecies());
    }
}
```
PublicTester.java
```
/*
 * Name: Hannah Hui and Liam Fernandez
 * Email: hahui@ucsd.edu, lgf001@ucsd.edu
 * PID: A00000000
 * Sources Used: JDK 17 Doc
 *
 * This is an example of the public tester for CSE 12 PA5 in Winter 2024.
 * It contains sanity checks on all 3 classes.
 */

import org.junit.Test;

import java.util.HashSet;
import java.util.Objects;

import static org.junit.Assert.*;

/**
 * The public tester for PA5, which covers some basic test cases.
 */
public class PublicTester {

    // ----------------Student class----------------

    /**
     * Test Student constructor with valid argument
     */
    @Test
    public void testStudentConstructor() {
        Student student = new Student("Test", "Student", "A12345678");
        assertEquals("Test", student.getFirstName());
        assertEquals("Student", student.getLastName());
        assertEquals("A12345678", student.getPID());
    }

    /**
     * Test equals with two equivalent Student objects
     */
    @Test
    public void testEqualsSame() {
        Student student1 = new Student("Test", "Student",
                "A12345678");
        Student student2 = new Student("Test", "Student",
                "A12345678");
        assertEquals(student1, student2);
    }

    /**
     * Test hashCode from Student
     */
    @Test
    public void testHashValueSame() {
        Student student = new Student("Test", "Student",
                "A12345678");
        assertEquals(student.hashCode(), Objects.hash("Test",
                "Student", "A12345678"));
    }

    // ----------------Course class----------------

    /**
     * Test Course constructor with valid argument
     */
    @Test
    public void testCourseConstructor() {
        Course course = new Course("CSE", "12", "Data Structure", 100);
        assertEquals("CSE", course.getDepartment());
        assertEquals("12", course.getNumber());
        assertEquals("Data Structure", course.getDescription());
        assertEquals(100, course.getCapacity());
        assertNotNull(course.enrolled);
    }

    /**
     * Enroll a new non-null student
     */
    @Test
    public void testEnrollNewStudent() {
        Course course = new Course("CSE", "12", "Data Structure", 100);
        Student stu = new Student("Whales", "Ocean", "A123");
        assertTrue(course.enroll(stu));
        assertTrue(course.enrolled.contains(stu));
        assertEquals(1, course.enrolled.size());
    }

    /**
     * Drop an existing student
     */
    @Test
    public void testDropExistingStudent() {
        Course course = new Course("CSE", "12", "Data Structure", 100);
        Student stu = new Student("Whales", "Ocean", "A123");
        course.enrolled.add(stu);

        assertTrue(course.drop(stu));
        assertFalse(course.enrolled.contains(stu));
        assertEquals(0, course.enrolled.size());
    }

    /**
     * Test isFull with a full roster
     */
    @Test
    public void testIsFull() {
        Course course = new Course("CSE", "12", "Data Structure", 3);
        for (int i = 0; i < 3; i++) {
            course.enrolled.add(new Student("Whales" + i, "Ocean", "A123"));
        }

        assertTrue(course.isFull());
    }

    /**
     * Get a descriptive string from a normal course
     */
    @Test
    public void testToString() {
        Course course = new Course("CSE", "12", "Data Structure", 100);
        assertEquals("CSE 12 [100] Data Structure", course.toString());
    }

    // ----------------Sanctuary class----------------

    /**
     * Test Sanctuary constructor with valid argument
     */
    @Test
    public void testSanctuaryConstructor() {
        Sanctuary sanct = new Sanctuary(500, 50);
        assertEquals(500, sanct.getMaxAnimals());
        assertEquals(50, sanct.getMaxSpecies());
        assertEquals(0, sanct.sanctuary.size());
    }

    /**
     * Test getNum with valid argument
     */
    @Test
    public void testCountForSpecies() {
        Sanctuary sanct = new Sanctuary(500, 50);
        sanct.sanctuary.put("Giraffe", 20);
        sanct.sanctuary.put("Meerkat", 65);

        assertEquals(20, sanct.countForSpecies("Giraffe"));
        assertEquals(65, sanct.countForSpecies("Meerkat"));
    }

    /**
     * Get the total number of animals at the sanctuary
     */
    @Test
    public void TestGetTotalAnimals() {
        Sanctuary sanct = new Sanctuary(100, 4);
        sanct.sanctuary.put("Koala", 55);
        assertEquals(55, sanct.getTotalAnimals());
    }

    /**
     * Get total number of species at a sanctuary
     */
    @Test
    public void TestGetTotalSpecies() {
        Sanctuary sanct = new Sanctuary(1000, 4);
        sanct.sanctuary.put("Koala", 55);
        sanct.sanctuary.put("Capybara", 70);
        sanct.sanctuary.put("Groundhog", 22);
        sanct.sanctuary.put("Vulture", 3);
        sanct.sanctuary.put("Zebra", 14);
        assertEquals(5, sanct.getTotalSpecies());
    }

    /**
     * Add a new species of animals to not-full sanctuary
     */
    @Test
    public void testRescue() {
        Sanctuary sanct = new Sanctuary(100, 20);

        assertEquals(0, sanct.rescue("Panda", 3));
        assertTrue(sanct.sanctuary.containsKey("Panda"));
        assertEquals(3, (int) sanct.sanctuary.get("Panda"));

        assertEquals(0, sanct.rescue("Frog", 32));
        assertTrue(sanct.sanctuary.containsKey("Frog"));
        assertEquals(32, (int) sanct.sanctuary.get("Frog"));

        assertEquals(2, sanct.sanctuary.size());
    }

    /**
     * Remove animals from a larger group of them at the sanctuary
     */
    @Test
    public void testRelease() {
        Sanctuary sanct = new Sanctuary(50, 5);
        sanct.sanctuary.put("Capybara", 40);
        sanct.sanctuary.put("Horse", 5);

        sanct.release("Capybara", 10);
        assertTrue(sanct.sanctuary.containsKey("Capybara"));
        assertEquals(30, (int) sanct.sanctuary.get("Capybara"));

        assertTrue(sanct.sanctuary.containsKey("Horse"));
        assertEquals(5, (int) sanct.sanctuary.get("Horse"));

        assertEquals(2, sanct.sanctuary.size());
    }
    
    /**
     * Help closing sanctuary with no new species and all aniamls can be 
     * rescued
     */
    @Test
    public void TestHelpClosingSanctuary1() {
        Sanctuary sanct = new Sanctuary(10, 2);
        sanct.sanctuary.put("Owlbear", 5);
        sanct.sanctuary.put("Dragon", 2);

        Sanctuary closingSanct = new Sanctuary(2, 2);
        closingSanct.sanctuary.put("Owlbear", 1);
        closingSanct.sanctuary.put("Dragon", 1);

        int saved = sanct.helpClosingSanctuary(closingSanct);

        assertEquals(2, saved);
        assertEquals(6, (int) sanct.sanctuary.get("Owlbear"));
        assertEquals(3, (int) sanct.sanctuary.get("Dragon"));
        assertFalse(closingSanct.sanctuary.containsKey("Owlbear"));
        assertFalse(closingSanct.sanctuary.containsKey("Dragon"));
    }
}
```
Sanctuary.java
```

/**
 * This file contains all methods for Sanctuary
 */
import java.util.Objects;
import java.util.Map;
import java.util.HashMap;
import java.util.Set;
import java.util.HashSet;
import java.util.Collections;
import java.util.ArrayList;
import java.util.Iterator;

/**
 * This class contains all methods for Sanctuary.
 */
public class Sanctuary {
    //class variables for sanctuary
    HashMap<String, Integer> sanctuary;
    private final int maxAnimals;
    private final int maxSpecies;

    /**
     * constructor for sanctuary sets maxAnimals and maxSpecies to the 
     * given input and makkes a new empty hashmap for sanctuary
     */
    public Sanctuary(int maxAnimals, int maxSpecies){
        if(maxAnimals <= 0 || maxSpecies <= 0 || maxSpecies > maxAnimals){
            throw new IllegalArgumentException();
        }
        this.maxAnimals = maxAnimals;
        this.maxSpecies = maxSpecies;
        this.sanctuary = new HashMap<>();
    }

    /**
     * returns the number of animals for a given species
     * @return the number of animals of the given species
     */
    public int countForSpecies(String species){
        if(species == null){
            throw new IllegalArgumentException();
        }
        if(!this.sanctuary.containsKey(species)){
            return 0;
        }
        return this.sanctuary.get(species);
    }

    /**
     * returns the number of animals in that sanctuary
     * @return the number of animals in the sanctuary
     */
    public int getTotalAnimals(){
        int count = 0;
        Set keys = this.sanctuary.keySet();
        for(Object key: keys){
            count += this.sanctuary.get(key);
        }
        return count;
    }

    /**
     * returns the number of species for a given sanctuary
     * @return the number of species of the given sanctuary
     */
    public int getTotalSpecies(){
        int count = 0;
        Set keys = this.sanctuary.keySet();
        for(Object key: keys){
            count ++;
        }
        return count;
    }

    /**
     * returns the max number of animals for a given sanctuary
     * @return the max number of animals of the given sanctuary
     */
    public int getMaxAnimals(){
        return this.maxAnimals;
    }

    /**
     * returns the max number of species for a given sanctuary
     * @return the max number of species of the given sanctuary
     */
    public int getMaxSpecies(){
        return this.maxSpecies;
    }

    /**
     * rescues as many animals as possible adding them to the sanctuary
     * and returns the number of animals not saved
     * @return the number of animals not saved
     */
    public int rescue(String species, int num){
        int unsaved = 0;
        if(num <= 0 || species == null){
            throw new IllegalArgumentException();
        }
        if((this.getMaxSpecies() == this.getTotalSpecies() && 
        !this.sanctuary.containsKey(species)) || 
        this.getMaxAnimals() == this.getTotalAnimals()){
            return num;
        }
        this.sanctuary.put(species, (this.countForSpecies(species) + num));
        while (this.getTotalAnimals() > this.getMaxAnimals()){
            this.sanctuary.put(species, (this.countForSpecies(species) - 1));
            unsaved++;

        }
        return unsaved;
    }

    /**
     * release a given number of animals from the sanctuary
     */
    public void release(String species, int num){
        if(num <= 0 || species == null || 
        num > this.countForSpecies(species) || 
        !this.sanctuary.containsKey(species)){
            throw new IllegalArgumentException();
        }
        if((this.countForSpecies(species) - num) == 0){
            this.sanctuary.remove(species);
        }
        else{
            this.sanctuary.put(species, (this.countForSpecies(species) - num));
        }
    }
}

    /**
     * rescues as many animals as possible adding them to the sanctuary from
     * the closingSanctuary and returns the number of animals saved
     * @return the number of animals saved
     */
    public int helpClosingSanctuary(Sanctuary closingSanctuary)	{
        int saved = 0;
        if(closingSanctuary ==null){
            throw new IllegalArgumentException();
        }
        if(this.getMaxAnimals() == this.getTotalAnimals()){
            return 0;
        }
        Set<String> closingSpecies = closingSanctuary.sanctuary.keySet();
        ArrayList<String> speciesArray = new ArrayList<>();
        for (String specie: closingSpecies){
            speciesArray.add(specie);
        } 
        Collections.sort(speciesArray);
        for(String specie: speciesArray){
            int tryToSave = closingSanctuary.countForSpecies(specie);
            int fail = this.rescue(specie, 
            closingSanctuary.countForSpecies(specie));
            closingSanctuary.sanctuary.put(specie, fail);
            if(fail == 0){
                closingSanctuary.sanctuary.remove(specie);
            }
            saved += tryToSave - fail;
        }
        return saved;
    }
}
```
SanctuaryCompileFail.sh
```
javac Sanctuary.java
```
Student.java
```
/**
 * This file contains all methods for Student
 */
import java.util.Objects;
import java.util.Map;
import java.util.HashMap;
import java.util.Set;
import java.util.HashSet;
import java.util.Collections;
import java.util.ArrayList;
import java.util.Iterator;

/**
 * This class contains all methods for Student.
 */
public class Student implements Comparable<Student>{
    //class variables for Student
    private final String firstName;
    private final String lastName;
    private final String PID;

    /**
     * constructor for Student sets firstName, lastName, and PID to 
     * the given value
     */
    public Student(String firstName, String lastName, String PID){
        if (firstName == null || lastName == null || PID == null){
            throw new IllegalArgumentException();
        }
        this.firstName = firstName;
        this.lastName = lastName;
        this.PID = PID;
    }

    /**
     * returns the firstName of the student
     * @return the firstName of the student
     */
    public String getFirstName(){
        return this.firstName;
    }

    /**
     * returns the lastName of the student
     * @return the lastName of the student
     */
    public String getLastName(){
        return this.lastName;
    }

    /**
     * returns the PID of the student
     * @return the PID of the student
     */
    public String getPID(){
        return this.PID;
    }

    /**
     * returns whether the given input is the same as what is being called on
     * @return whether the given input is the same as what is being called on
     */
    public boolean equals(Object o){
        if(o == null){
            return false;
        }
        if(o.getClass() != Student.class){
            return false;
        }
        Student temp = (Student) o;
        if(this.getFirstName().equals(temp.getFirstName()) 
        && this.getLastName().equals(temp.getLastName()) 
        && this.getPID().equals(temp.getPID())){
            return true;
        }
        return false;
    }

    /**
     * returns the hashCode for the student
     * @return the hashCode for the student being called on
     */
    @Override public int hashCode() {
        return Objects.hash(this.getFirstName(), this.getLastName(), 
        this.getPID());
    }

    /**
     * returns how a student compares to a given student based on given 
     * priorities first comparing lastName, then firstName, then PID
     * @return the difference in values of the first difference
     */
    public int compareTo(Student o){
        if(o == null){
            throw new NullPointerException();
        }
        if(!this.getLastName().equals(o.getLastName())){
            return this.getLastName().compareTo(o.getLastName());
        }
        if(!this.getFirstName().equals(o.getFirstName())){
            return this.getFirstName().compareTo(o.getFirstName());
        }
        return this.getPID().compareTo(o.getPID());
    }
}
```
README.md
```
# CSE 12 Winter 2024 PA5 - Hash Table

**Due date: Thursday, Feb 15th @ 11:59 PM PST**

There is an FAQ post on Piazza. Please read that post first if you have any questions.


## **Learning goals:**



* Use Java’s HashSet and HashMap to solve real-world problems 
* Write JUnit tests to verify proper implementation

**Important: You won’t need to implement any hashing algorithms/data structures in this PA. Instead, you’ll need to use Java's built-in HashSet and HashMap to complete this PA.**



## Testing and Application of HashMap and HashSet [100 points]

### Part 1: Application of HashSet/HashMap (85 points)


In this part of the assignment,  you will directly use Java's built-in data structures and write JUnit tests to ensure that you call the functions correctly.

**Make sure to read the entire write-up before you start coding.** You may not change any public class/method or variable names given in the write-up or starter code.

Download the starter code from here and put it in a directory in your working environment.

You will find the following files:

```
+-- PA5
|   +-- PublicTester.java
```

You will have to create the following files: `Student.java`, `Course.java`, `Sanctuary.java`, and `CustomTester.java`.

Here are a list of imports you may use to help you complete this part of the assignment:
- `java.util.Objects`
- `java.util.Map`
- `java.util.HashMap`
- `java.util.Set`
- `java.util.HashSet`
- `java.util.Collections`
- `java.util.ArrayList`
- `java.util.Iterator`

For Tester files, you may import anything you want.


### Part 1a: `HashSet` Application

It’s time to register for classes again, and we need to organize the students and courses during the enrollment period.

You will be using a `HashSet` to help you track course enrollment. Refer to the [JDK 17 documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashSet.html) for more information on `HashSet`. You are allowed to directly use any of the methods listed in the documentation for Java’s `HashSet`.


#### Student

You will first complete the methods to implement the `Student` class in `Student.java`. `Student` objects will be stored in `Course` objects.

**All instance variables in `Student` should be declared as private final.** Think about what will happen to the hash code if you allow those elements to be changed after initialization.


|Instance Variable|Description|
|--- |--- |
|`String firstName`|A string representing the first name of the student.|
|`String lastName`|A string representing the last name of the student.|
|`String PID`|A string representing the PID of the student. This is unique for each student.|



You will be required to implement the following methods.


|Method Name|Description|
|--- |--- |
|`public Student(String firstName, String lastName, String PID)`|Initialize the student’s information. Throw an `IllegalArgumentException` if any of the arguments are null.|
|`public String getFirstName()`|Return the student’s first name|
|`public String getLastName()`|Return the student’s last name|
|`public String getPID()`|Return the student’s PID|
|`public boolean equals(Object o)` <br> *overrides [`Object::equals()`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)*| Returns `true` if `o` is 1) not `null`, 2) a `Student` object, 3) all the instance variables of `o` equal the corresponding instance variables of the current `Student` object. Otherwise, return `false`.|
|`public int hashCode()` <br>*overrides [`Object::hashCode()`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode())*| Return the hash value generated using the built-in [`Objects.hash`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Objects.html#hash(java.lang.Object...)) function. The hash function should generate a hash value in the order of the student’s `firstName`, `lastName`, and `PID`.|
|`public int compareTo(Student o)` <br> *implements [`Comparable<Student>::compareTo`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Comparable.html#compareTo(T))*| Compare this with another `Student` in the order of `lastName`, `firstName`, and `PID`, using [`String::compareTo`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html#compareTo(java.lang.String)). That said, continue to compare `firstName` if and only if `lastName` ties; and continue to compare `PID` if and only if `lastName` and `firstName` tie. <br><br>Throw a `NullPointerException` if `o` is `null`.<br><br> For example, if we have Student 1 with the last name “Jones”, first name “Angela”, and PID “A12345678” and Student 2 with the last name “Smith”, first name “Aaron”, and PID “A12345679”, then `student1.compareTo(student2)` will return a negative value (e.g. -1).|




#### Course

Our Course class will help us store the students registered for this particular course in the form of a `HashSet`.

**All Course variables should be declared as `private final` except for `HashSet<Student> enrolled`, which should have the default access modifier (no modifier).** This is default to help you write JUnit tests more easily.


|Instance Variable|Description|
|--- |--- |
|`HashSet<Student> enrolled`|A collection of students that are enrolled in this course.|
|`int capacity`|The maximum number of students that can be enrolled in this course.|
|`String department`|This course falls under this department.|
|`String number`|A string representing the course number.|
|`String description`|A string representing the description of the course.|



You will be required to implement the following methods.


|Method Name|Description|Exceptions to Throw|
|--- |--- |--- |
|`public Course(String department, String number, String description, int capacity)`|Initialize the course’s information with an initial enrollment of 0 students.|Throw an `IllegalArgumentException` if any of the arguments are null. Throw an `IllegalArgumentException` if capacity is 0 or negative.|
|`public String getDepartment()`|Return the department name.||
|`public String getNumber()`|Return the course number.||
|`public String getDescription()`|Return the description of the course.||
|`public int getCapacity()`|Return the capacity of the course.||
|`public boolean enroll(Student student)`|If there is room in this course and the student is not currently enrolled, add the student to the course. Return `true` for successful enrollment and `false` otherwise.|Throw an `IllegalArgumentException` if `student` is `null`.|
|`public boolean drop(Student student)`|If the student is enrolled in the course, drop them from the course. Return `true` for successfully dropping student and `false` otherwise (i.e. the student is not in the course).|Throw an `IllegalArgumentException` if `student` is `null`.|
|`public void cancel()`|If the course is canceled, all of the students are dropped from the course. Remove all the students from the course.||
|`public boolean isFull()`|If the course is at its capacity, return `true`. Otherwise, return `false`.||
|`public int getEnrolledCount()`|Return the current number of enrolled students.||
|`public int getAvailableSeats()`|Return the number of students that can still enroll in the course (assuming everyone stays enrolled).||
|`public HashSet<Student> getStudents()`|Return a shallow copy of all the students enrolled in this course. The returned set should have a different address than the original set, but the references to students that are stored in the set should be the same. Hint: check the behavior of [`HashSet<E>::clone()`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashSet.html#clone()) method.||
|`public ArrayList<Student> getRoster()`|Turn the collection of enrolled students into an `ArrayList<Student>` collection by iterating through the set using the iterator or a for-each loop. Return the final result as a sorted `ArrayList<Student>`. All the students in the course should be listed in the increasing order specified by the `compareTo` method in `Student` in the `ArrayList<Student>` version of the roster. You may use [`Collections.sort`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Collections.html#sort(java.util.List)) to sort the list.||
|`public String toString()` *overrides [Object::toString()](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString())*|Return a string representation for a Course object. The format should be as follows: `<department> <number> [<capacity>] <description>` where the contents inside the `< >` refer to the instance variables of the class. Do not include the `< >` characters in the return value. <br><br> For example, for a Course with `department = "CSE"`, `number = "12"`, `capacity = 196`, and `description = "Data Structure"`, it should return `"CSE 12 [196] Data Structure"` <br><br> You might find [`String::format()`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html#format(java.lang.String,java.lang.Object...)) helpful for this method.||




### Part 1b: `HashMap` Application

A wildlife sanctuary needs your help to efficiently track the animals that are in its care. The sanctuary wants to keep track of how many of each species are currently located on its grounds.

You will be using a `HashMap` to help you organize all the animals at the sanctuary. Refer to the [JDK 17 documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashMap.html) for more information on `HashMap`. You are allowed to directly use any of the methods listed in the documentation for Java’s `HashMap`.
    
**All Sanctuary variables should be declared as `private final` except for `HashMap<String, Integer> sanctuary`, which should have the default access modifier (no modifier).** This is default to help you write JUnit tests more easily.

|Instance Variable|Description|
|--- |--- |
|`HashMap<String, Integer> sanctuary`|Container to store all the animal species in the sanctuary. The key (`String`) represents the name of the animal species and the value (`Integer`) represents the number of that species at the sanctuary. If at anytime, the key is `null` or the value is 0, the species should not be in the sanctuary `HashMap`.|
|`int maxAnimals`|The maximum number of animals that the sanctuary can support.|
|`int maxSpecies`|The maximum number of species that the sanctuary can support.|



You will be required to implement the following methods.


|Method Name|Description|Exceptions to Throw|
|--- |--- |--- |
|`public Sanctuary(int maxAnimals, int maxSpecies)`|Initialize the `HashMap` with no elements. Initialize the other instance variables accordingly.|If `maxAnimals` or `maxSpecies` is less than or equal to `0`, or `maxSpecies` is larger than `maxAnimals`, throw an `IllegalArgumentException`. |
|`public int countForSpecies(String species)`|Return the number of animals in the sanctuary that are of the given `species`. If the given species does not exist in the sanctuary, return 0.|If `species` is `null`, throw an `IllegalArgumentException`.|
|`public int getTotalAnimals()`|Return the total number of animals in the sanctuary.||
|`public int getTotalSpecies()`|Return the total number of species in the sanctuary.||
|`public int getMaxAnimals()`|Return the maximum allowed number of animals in the sanctuary.||
|`public int getMaxSpecies()`|Return the maximum allowed number of species in the sanctuary.||
|`public int rescue(String species, int num)`|If it does not exceed the `maxAnimals` nor `maxSpecies` of the sanctuary, add `num` animals of `species` to the sanctuary. If adding `num` animals exceeds the maximum limit, add as many animals as permitted. Return the number of animals that could not be rescued.|If `num` is less than or equal to 0, throw an `IllegalArgumentException`. If species is `null`, throw an `IllegalArgumentException`.|
|`public void release(String species, int num)`|Remove `num` animals of species from the sanctuary. Remove the `species` from the sanctuary if its remaining count reaches 0.|Throw an `IllegalArgumentException` if any of the following are `true`: <br> - `num` is less than or equal to 0 <br> - `num` is greater than the number of animals of species at the sanctuary <br> - `species` is `null` <br> - `species` does not exist in the sanctuary|
|`public int helpClosingSanctuary(Sanctuary closingSanctuary)`|For each species in `closingSanctuary`, try to rescue as many animals of that species into the sanctuary. Any animals rescued into the sanctuary should be released from `closingSanctuary`. Remove the species from `closingSanctuary` if its remaining count reaches 0. Return the total number of animals rescued from `closingSanctuary`. <br><br> IMPORTANT: You must process the species in `closingSanctuary` in lexicographical order. You may use [`Collections.sort`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Collections.html#sort(java.util.List)) to help sort the species in `closingSanctuary`. <br><br> For example, consider an empty `sanctuary`  (no animals present) with `maxAnimals = 10` and `maxSpecies = 2` and a `closingSanctuary` with 2 dogs and 3 cats. `sanctuary.helpClosingSanctuary(closingSanctuary)` should return 5 with no species remaining in `closingSanctuary` and 2 dogs and 3 cats now inside `sanctuary`. | If `closingSanctuary` is null, throw an `IllegalArgumentException`.|




### **Part 2: JUnit Testing (10 points)**
- We provide `PublicTester.java`.
     This contains all the public test cases we will use to grade your Student, Course, and Sanctuary implementation (visible on Gradescope).
- Your task: create `CustomTester.java` and implement the unit tests in `CustomTester.java` based on the description in the Tests table below.
    * ⚠️There are hidden tests on Gradescope not described in the write-up. Make sure to write additional tests to verify your implementation's correctness! ⚠️
    * Your tests will be graded by checking if they pass on a   good implementation and fail on a bad implementation. If a test fails on a good implementation, then the test is written incorrectly. If a test passes on a bad implementation, it may be written incorrectly or may be not be rigorous enough (try adding more asserts).
    * **Gradescope will report whether your CustomTester fails on our good implementation (solution code) as a way to sanity check some of your test cases. However, you will not be able to see whether your tests pass/fail on the bad implementations until the PA is graded.** Do your best to write comprehensive test asserts based on the write-up description and public tester examples.
    * Some of your tests will be run on several bad implementations. You will receive 1.25 pts for every bad implementation your test fails (if your test also passes on the good implementation). **See the bottom of the writeup [here](#How-your-assignment-will-be-evaluated-100-points) for the new CustomTester point assignment (maximum score of 10pts for CustomTester).**
   * Make sure the names of your tests match exactly with the names in the table. If the names of any tests don't match, you'll not receive points for those tests.
   * Feel free to create more tests for your own benefits (additional test will not be graded).
   * Tip: You might find the `.equals` method of HashSet or HashMap helpful when you write your asserts. However, the downside is that this will not report detailed failure messages, in which case writing other asserts on HashSet/HashMap may be helpful.


#### Tests Table: List of test cases to write and their description
| Test Cases                  | Description                                                                                                                                                                                                          | Point Value |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| `testStudentEquals`         | Call `equals` when the argument is a non-Student object.                                                                                                                                                             | 1.25        |
| `testStudentCompareTo`      | Call `compareTo` to compare two Students that have the same last name and same first name. `this` Student should have a PID that is lexigraphically smaller than the other Student.                                  | 1.25        |
| `testCourseDrop`        | Attempt to `drop` a non-existing student with a non-empty course roster. This means the course should have at least 1 student enrolled already.                                                                  | 1.25        |
| `testCourseEnroll`          | Attempt to `enroll` a valid student into a course that is already at maximum capacity.                                                                                                                               | 1.25        |
| `testCourseGetRoster`       | Call `getRoster` on a course with a large number of enrolled students. (We suggest testing on a course that has 100 validly enrolled students.) <br></br>Hint: How might you generate 100 `Student` objects with a loop? How might you keep track of these `Student` objects and use the ArrayList `equals` method for assert statements?                                                                                           | 1.25        |
| `testSanctConstructor`      | Call the Sanctuary constructor with a negative argument for `maxAnimals`.                                                                                                                                              | 1.25        |
| `testSanctRescuePartial`    | `rescue` animals from an existing species, where rescuing `num` animals will cause the number of animals to exceed the sanctuary's max capacity. This means only some of the animals should be rescued successfully. | 1.25        |
| `testSanctRescueMaxSpecies` | `rescue` a new non-null species when the sanctuary is already at the max capacity for species.                                                                                                                       | 1.25        |
| `testSanctReleasePartial`   | `release` some (not all) of the animals of an existing species in the sanctuary.                                                                                                                                     | 1.25        |
| `testSanctReleaseTooMany`   | Attempt to `release` more animals than exists for a specific animal species in the sanctuary. The existing number of animals for this species should be non-zero.                                                           | 1.25        |
| `testSanctHelpClosingSanctuaryPartial` | All species in `closingSanctuary` already exist in the sanctuary, but not all of the animals in `closingSanctuary` can be rescued. (i.e., the sanctuary will reach `maxAnimals` before all animals in `closingSanctuary` can be transferred) | 1.25


#### How to compile and run the testers:
Running the tester on UNIX based systems (including macOS):

* Compile: `javac -cp ../libs/junit-4.13.2.jar:../libs/hamcrest-2.2.jar:. PublicTester.java`
* Execute: `java -cp ../libs/junit-4.13.2.jar:../libs/hamcrest-2.2.jar:. org.junit.runner.JUnitCore PublicTester`

Running the tester on Windows systems:

* Compile: `javac -cp ".;..\libs\junit-4.13.2.jar;..\libs\hamcrest-2.2.jar" PublicTester.java`
* Execute: `java -cp ".;..\libs\junit-4.13.2.jar;..\libs\hamcrest-2.2.jar" org.junit.runner.JUnitCore PublicTester`

You should run the above commands in the `starter` directory. To run the custom tester, replace references to PublicTester with CustomTester in the above commands.

⚠️Your code must first compile in order to receive credit for the different test cases. You will receive a zero if your code doesn’t compile.


### **Part 3: Coding Style (5 points)**

Coding style is an important part of ensuring readability and maintainability of your code. We will grade your code style in all submitted code files according to the style guidelines. Namely, there are a few things you must have in each file/class/method:

* File header
* Class header
* Method header(s)
* Inline comments
* Proper indentation
* Descriptive variable names
* No magic numbers (Exception: Magic numbers can be used for testing.)
* Reasonably short methods (if you have implemented each method according to the specification in this write-up, you’re fine). This is not enforced as strictly.
* Lines shorter than 80 characters
* Javadoc conventions (`@param`, `@return` tags, `/** comments */`, etc.)


A full style guide can be found [here](https://github.com/CaoAssignments/style-guide/blob/main/README.md) and a sample styled file can be found [here](https://github.com/CaoAssignments/guides/blob/main/resources/SampleFile.java). If you need any clarifications, feel free to ask on Piazza.


## Submission Instructions

#### Turning in your code

* Submit all of the following files to Gradescope
    * `Student.java`
    * `Course.java`
    * `Sanctuary.java`
    * `CustomTester.java`

**Important**: Even if your code does not pass all the tests, you will still be able to submit your homework to receive partial points for the tests that you passed. Make sure your code compiles in order to receive partial credit.

#### How your assignment will be evaluated [100 points]

* **Correctness** [95 points] You will earn points based on the autograder tests that your code passes. If the autograder tests are not able to run (e.g., your code does not compile or it does not match the specifications in this writeup), you may not earn credit.
    * Tester [10 points]
        * The autograder will test your implementation of the JUnit tests. Your unit tests are expected to fail or pass based on the [Part 2 Test Table](#Tests-Table-List-of-test-cases-to-write-and-their-description).
        * *This section has a maximum of 10 pts. This means if you pass at least 8 out of 11 custom tester cases, you will get full points for the Testing portion.*
    * HashMap/HashSet Implementation [85 points]
        * The autograder will test your implementation on the public test cases given in `PublicTester.java` and hidden test cases not described in this PA writeup.
* **Coding Style** [5 points]
    * `Student.java`, `Course.java`, `Sanctuary.java` will be graded on style. `CustomTester.java` will be graded on file, class, method headers and indentation.

```
<br>The full command line (or lines) you ran to trigger the bug
```
javac Sanctuary.java
```
<br>A description of what to edit to fix the bug
Delete the extra curly bracket on line 132 of Sanctuary.java.

## Part 2
I learned how to use java jdb to stop at a certain point and get the local variables at that point. You use ```Javac -g *.java(self expand)``` so that you will be able to access the local variables. Create the jdb with ```jdb MainClass(Main.java in this case)```
Break on line after the variable you want is created/changed with ```stop [classname]: [line #]``` Run with ```run```You can then use ```locals``` to find the locals at that point or print what you specifically want.
