# java-lemda-experience-
lemda
package com.dailycodebuffer;

import java.util.List;
import java.util.function.Predicate;

public class Main {


    interface CheckPerson {
        boolean test(Person p);
    }

    static class CheckPersonEligibleForSelectiveSearch
    implements CheckPerson {

        @Override
        public boolean test(Person p) {
            return p.gender == Person.Sex.FEMALE &&
                    p.getAge() >= 18 &&
                    p.getAge() <=25;
        }
    }

    public static void printPersonOlderThan(List<Person> people,
                                            int age) {
        for(Person p: people) {
            if(p.getAge() >= age) {
                p.printPerson();
            }
        }
    }

    public static void printPersonWithinAgeRange(
            List<Person> people, int low, int high) {
        for(Person p: people) {
            if(low <= p.getAge() && p.getAge() <high) {
                p.printPerson();
            }
        }
    }

    public static void printPeople(List<Person> people,
                                   CheckPerson tester) {
        for(Person p: people) {
            if(tester.test(p)) {
                p.printPerson();
            }
        }
    }

    public static void printPeopleWithPredicate(List<Person> people,
                                   Predicate<Person> tester) {
        for(Person p: people) {
            if(tester.test(p)) {
                p.printPerson();
            }
        }
    }

    public static void main(String[] args) {
	// write your code here
        List<Person> people = Person.generateDefaultList();
        //printPersonOlderThan(people,20);
        //printPersonWithinAgeRange(people,20,21);
       // printPeople(people, new CheckPersonEligibleForSelectiveSearch());

        printPeople(people, new CheckPerson() {
            @Override
            public boolean test(Person p) {
                return p.gender == Person.Sex.MALE &&
                        p.getAge() >= 18 &&
                        p.getAge() <=25;
            }
        });

        printPeople(people,  (p) -> p.gender == Person.Sex.MALE && p.getAge() >= 18 && p.getAge() <=25);

        printPeopleWithPredicate(people,  (p) -> p.gender == Person.Sex.MALE && p.getAge() >= 18 && p.getAge() <=25);
    }
}


class Person {


    public void printPerson() {
        System.out.println(this.toString());
    }

    public enum Sex {
        MALE, FEMALE
    }

    String name;
    int age;
    Sex gender;
    String emailAddress;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Sex getGender() {
        return gender;
    }

    public void setGender(Sex gender) {
        this.gender = gender;
    }

    public String getEmailAddress() {
        return emailAddress;
    }

    public void setEmailAddress(String emailAddress) {
        this.emailAddress = emailAddress;
    }

    public Person() {
    }

    public Person(String name, int age, Sex gender, String emailAddress) {
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.emailAddress = emailAddress;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", gender=" + gender +
                ", emailAddress='" + emailAddress + '\'' +
                '}';
    }



    public static List<Person> generateDefaultList() {
        List<Person> people = new ArrayList<>();

        people.add(new Person("Shabbir", 20, Sex.MALE, "shabbir@gmail.com"));
        people.add(new Person("Nikhil", 21, Sex.MALE, "nikhil@gmail.com"));
        people.add(new Person("Shivam", 19, Sex.MALE, "shivam@gmail.com"));
        return  people;
    }
}
