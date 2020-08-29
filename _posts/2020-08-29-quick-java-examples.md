---
layout: post
title: "Quick Java Examples"
tags:
 -
---

```java
/**
 * 
 */
package tutorial;
import java.util.HashMap;
import java.util.Scanner;
import java.lang.*;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.time.*;
import java.util.Date;
/**
 * @author asjha2
 *
 */
public class HashMapExample {
	enum DAYS{
		SUNDAY, MONDAY, TUESDAY, WEDBESDAY, FRIDAY, SATURDAY
	};
	public static void main(String[] args) {
		HashMap<String, String> capitalCities = new HashMap<String, String>();
		    capitalCities.put("England", "London");
		    capitalCities.put("Germany", "Berlin");
		    capitalCities.put("Norway", "Oslo");
		    capitalCities.put("USA", "Washington DC");
		    System.out.println(capitalCities.get("USA")); 
		    
		    /*
		     * IO Operation
		     */
		    String Country;
			Scanner sc = new Scanner(System.in);
			System.out.println("Enter Country:\n");
			Country = sc.nextLine();
			
			String Capital;
			System.out.println("Enter Capital City\n");
			Capital = sc.nextLine();
			
			capitalCities.put(Country, Capital);
			System.out.println(capitalCities);
			
			/*
			 * Thread Operation
			 */
			//Create two thread and prints local time.
			Thread t1 = new Thread();
			Thread t2 = new Thread();
			System.out.println(t1.getId()); 
			System.out.println(t2.getId());
			
			
			/*
			 * File Handling
			 */
			File myFile = new File("dump.txt");
			if(myFile.exists()) {
				System.out.println("File Already exist");
			}
			else {
				System.out.println("File is being Created");
				try {
					if(myFile.createNewFile()) {
						System.out.println("File Created!");
					}
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
			//FileWriter Operation
			try {
				FileWriter fw = new FileWriter(myFile);
				fw.write("Hi Ashish");
				fw.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
			//FileReader
			try {
				Scanner fsc = new Scanner(myFile);
				while(fsc.hasNextLine()) {
					System.out.println(fsc.nextLine());
				}
				fsc.close();
			} catch (FileNotFoundException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
			//String Method
			System.out.println("The hash of Ashish is : ");
			System.out.println("Ashish".hashCode());
			
			/*
			 * Lambda Expression: Java 8
			 */
			ArrayList<Integer> a = new ArrayList<Integer>();
			for(int i =0;i<10;i++) {
				a.add(i);
			}
			a.forEach((num)-> {System.out.println(num);});
			
			/*
			 * Date and time
			 */
			LocalDate l = LocalDate.now();
			System.out.println(l);
			System.out.println(LocalTime.now());;
			
			/*
			 * Enums
			 */

			System.out.println(DAYS.SATURDAY);
			
	}
	
	
	
}
```