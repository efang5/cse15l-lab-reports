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
![Image](photo of problems section)

4. At the end, all the information needed about the setup including:
<br>The file & directory structure needed
![Image](photo of sidebar)
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
<br>The full command line (or lines) you ran to trigger the bug
```
javac Sanctuary.java
```
<br>A description of what to edit to fix the bug
Delete the extra curly bracket on line 132 of Sanctuary.java.

## Part 2
I learned how to use java jdb to stop at a certain point and get the local variables at that point. You use ```Javac -g *.java(self expand)``` so that you will be able to access the local variables. Create the jdb with ```jdb MainClass(Main.java in this case)```
Break on line after the variable you want is created/changed with ```stop [classname]: [line #]``` Run with ```run```You can then use ```locals``` to find the locals at that point or print what you specifically want.
