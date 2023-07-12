import java.util.HashMap;
import java.util.Map;

class Solution { 


    

    public static void main(String[] args) { 

        System.out.println("Answer 1 ");
        /*  Question 1
        Given two strings s and t, *determine if they are isomorphic*.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

**Example 1:**

**Input:** s = "egg", t = "add"

**Output:** true */ 

    String s = "egg"; 
    String t = "add"; 

    System.out.println(checkIsomorphic(s, t)); 




    System.out.println("Answer 2 ");
        /*
💡 **Question 2**

Given a string num which represents an integer, return true *if* num *is a **strobogrammatic number***.

A **strobogrammatic number** is a number that looks the same when rotated 180 degrees (looked at upside down).

**Example 1:**

**Input:** num = "69"
 
**Output:**

true

 */ 

      String num = "69";

      boolean res = checkStrobogrammatic(num); 
      System.out.println(res); 






       /*<aside>
💡 **Question 4**

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Example 1:**

**Input:** s = "Let's take LeetCode contest"

**Output:** "s'teL ekat edoCteeL tsetnoc"

</aside> */ 


     String s4 = "Let's take LeetCode contest"; 
     String res4 = reverseString4(s4);
     System.out.println(res4);





       
        /*<aside>
💡 **Question 6**

Given two strings s and goal, return true *if and only if* s *can become* goal *after some number of **shifts** on* s.

A **shift** on s consists of moving the leftmost character of s to the rightmost position.

- For example, if s = "abcde", then it will be "bcdea" after one shift.

**Example 1:**

**Input:** s = "abcde", goal = "cdeab"

**Output:**

true

 */ 

   String s6 = "abcde"; 
   String goal = "cdeab";

System.out.println(rotateString4(s6, goal));  



/*<aside>
💡 **Question 7**

Given two strings s and t, return true *if they are equal when both are typed into empty text editors*. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

**Example 1:**

**Input:** s = "ab#c", t = "ad#c"

**Output:** true

**Explanation:**

Both s and t become "ac".

</aside> */ 
System.out.println("Answer 7 ");
  String s7 = "ab#c"; 
   String t7 = "ad#c";

   System.out.println(backspaceCompare(s7,t7));



    /*<aside>
💡 **Question 8**

You are given an array coordinates, coordinates[i] = [x, y], where [x, y] represents the coordinate of a point. Check if these points make a straight line in the XY plane.

**Example 1:**

**Input:** coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]

**Output:** true

</aside> */ 

    int coordinates[][] = {{1,2} ,{2,3} , {3,4} , {4,5} , {5,6}, {6,7}}; 

    if(checkStraightLine(coordinates)) {
        System.out.println("The Given Coordinates forms a straight line");
    } else {System.out.println("The given coordinates do not form a straight line");}
    
 

    } 



    // Funtion Defenition for question 1 

    public static boolean checkIsomorphic(String s, String t) {

        if(s.length() != t.length()) {
            return false; 
        } 
       
        Map<Character,Character> map = new HashMap<>();

        for(int i = 0; i<s.length(); i++) {
            char original = s.charAt(i); 
            char replaced = t.charAt(i); 

            if( !map.containsKey(original)) {
                if(!map.containsValue(replaced)) {
                    map.put(original, replaced);
                } else { return false;  }
            } else {
                if(map.get(original) != replaced) {
                    return false; 
                }
            }
        } 
        return true; 
    }

    


    // Function Defenition for Question 2 

    
      public static boolean checkStrobogrammatic(String num) {
        
        Map<Character,Character> map = new HashMap<>(); 
        map.put('0','0');
        map.put('1', '1');
        map.put('6','9');
        map.put('9','6');
        map.put('8', '8');
       
        int start = 0; 
        int end = num.length()-1;
    

       while(start <= end) {
     
        if(num.charAt(start) != map.getOrDefault(num.charAt(end),' ')) {
            return false; 
        } 
        start++; 
        end--; 
       }

        return true; 
      }



       

 // Function Defenition for question 4 

 
    public static String reverseString4(String s) {

        String sa[] = s.split(" "); 

        StringBuilder result = new StringBuilder();

        for(String cs : sa ) {
            StringBuilder words = new StringBuilder(); 
            words.append(cs);
            words.reverse(); 

             result.append(words+" ");  
                    
             
        }  

        result.setLength(result.length()-1);
        return result.toString(); 
    }


  // Function Defenition for question 6 

     public static boolean rotateString4(String s, String goal) {

        // first check the length of s and goal if they are equal 
        // And the we add s + s because all the roations will come in s + s 

        if(s.length() == goal.length() && (s+s).contains(goal)) {
            return true; 
        } 
        return false; 

        // suppose original string is - abcde    
        // s+s = abcdeabcde 
        // roatation possible bcdea, cdeab, deabc ,eabcd , abcde 
     }


// Function Defenition for question 7 

public static boolean backspaceCompare(String s, String t) {
     
      
      return getActual(s).equals(getActual(t));

    
    } 
    private static String getActual(String input) {

        int hashCount = 0; 
        
        StringBuilder result = new StringBuilder();  

        for(int i = input.length()-1; i>= 0 ; i--) {
            if(input.charAt(i) == '#') {
                hashCount++; 
                continue;
            } 
            if(hashCount > 0) {
                hashCount--;
            } else {
                result.insert(0,input.charAt(i)); 
            }
        } 
        return result.toString(); 

    } 



    // Function Defenition for question 8 

    
    public static boolean checkStraightLine(int coordinates[][]) {
      
        double deltaX = getXDiff(coordinates[0],coordinates[1]); 
        double deltaY = getYDiff(coordinates[0],coordinates[1]);

        for(int i = 2 ; i<coordinates.length; i++) {
            if(deltaY * getXDiff(coordinates[0], coordinates[i]) != deltaX * getYDiff(coordinates[0], coordinates[i])) {
                return false; 
            }
        }
       
       return true;  
    }
     
    private static double getXDiff(int p1[] , int p2[]) {
        return p2[0] - p1[0];
    } 
    private static double getYDiff(int p1[], int p2[]) {
        return p2[1] - p1[1]; 
    }


}