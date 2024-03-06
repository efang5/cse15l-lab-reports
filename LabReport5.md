# Lab Report 5
## Part 1

1. The original post from a student with a screenshot showing a symptom and a description of a guess at the bug/some sense of what the failure-inducing input is. (Don't actually make the post! Just write the content that would go in such a post)

My code for Sanctuary.java does no compile properly.\ Here is my code.
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


