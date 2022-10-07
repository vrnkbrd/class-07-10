# class-07-10
Diff: 6 
Task: 
We search non-negative integer numbers, with at most 3 digits, such as the sum of the cubes of their digits is the number itself; we will call them "cubic" numbers.

153 is such a "cubic" number : 1^3 + 5^3 + 3^3 = 153
These "cubic" numbers of at most 3 digits are easy to find, even by hand, so they are "hidden" with other numbers and characters in a string.

The task is to find, or not, the "cubic" numbers in the string and then to make the sum of these "cubic" numbers found in the string, if any, and to return a string such as:

"number1 number2 (and so on if necessary) sumOfCubicNumbers Lucky" 
if "cubic" numbers number1, number2, ... were found.

The numbers in the output are to be in the order in which they are encountered in the input string.

If no cubic numbers are found return the string: `"Unlucky"``.

Examples:
 - s = "aqdf&0#1xyz!22[153(777.777" 
   the groups of at most 3 digits are 0 and 1 (one digit), 22 (two digits), 153, 777, 777 (3 digits)
   Only 0, 1, 153 are cubic and their sum is 154
   Return: "0 1 153 154 Lucky"

- s = "QK29a45[&erui9026315"
  the groups are 29, 45, 902, 631, 5. None is cubic.
  Return: "Unlucky"
My solution: 
class Cubes {
  
  public static String isSumOfCubes(String s) {

    final int MAX_NUM_DIGITS = 3;

    StringBuilder str = new StringBuilder();
 
    char arr[] = s.toCharArray();
    int sum_total = 0;
    boolean found_cubic_nums = false;

    for (int i = 0; i < arr.length; i++) {
      while (i < arr.length && !Character.isDigit(arr[i])) {
        i++;
      }

      int num_digits = 0;
      int num = 0;
      int cubic_sum = 0;

      while (i < arr.length && Character.isDigit(arr[i])) {

        num_digits++;

        int x = arr[i] - '0';
        num = num * 10 + x;
        cubic_sum += x * x * x;

        if (num_digits == MAX_NUM_DIGITS) {
          break;
        }

        i++;
      }

      if (num_digits > 0 && num == cubic_sum) {
        found_cubic_nums = true;
        sum_total += num;
        str.append(num + " ");
      }
    }

    if (found_cubic_nums) {
      return str.append(sum_total+ " Lucky").toString();
    } else {
      return "Unlucky";
    }
  }
}

Fav solution: 
import java.util.ArrayList;

class Cubes {
  static String isSumOfCubes(String s) {
    var cubes = new ArrayList<String>();
    for (String num : s.replaceAll("[^\\d]", " ").trim().split("\\s+")) {
      for (String top3 : num.split("(?<=\\G...)")) {
        if (top3.equals(top3.chars().map(n -> (int) Math.pow(n - 48., 3)).sum() + "")) {
          cubes.add(top3);
        }
      }
    }
    return cubes.isEmpty() ? "Unlucky" : String.join(" ", cubes) + " " + cubes.stream().mapToInt(Integer::parseInt).sum() + " Lucky";
  }
}
I loved that the the participant used this data structure and maximized using of functions from library

Task 2 6 kyu
Task: Complete the method/function so that it converts dash/underscore delimited words into camel casing. The first word within the output should be capitalized only if the original word was capitalized (known as Upper Camel Case, also often referred to as Pascal case).

Examples
"the-stealth-warrior" gets converted to "theStealthWarrior"
"The_Stealth_Warrior" gets converted to "TheStealthWarrior"
My solution: 
import java.lang.StringBuilder;
class Solution{

  static String toCamelCase(String s){
     StringBuilder a = new StringBuilder();
     for(int i = 0; i < s.length(); i++) {
          if(s.charAt(i) == '-' || s.charAt(i) == '_') {
             a.append(Character.toUpperCase(s.charAt(i + 1))); 
             i++;
             continue;      
          }else {
             a.append(s.charAt(i));
          }
       
      
       
     }
    return String.valueOf(a);
  }
}

Fav solution: 
import java.lang.StringBuilder;
class Solution{

  static String toCamelCase(String s){
    String[] words = s.split("[_\\-]");
    s=words[0];
    for(int i=1; i<words.length; i++)
      s+=words[i].substring(0,1).toUpperCase()+words[i].substring(1).toLowerCase();
    return s;
  }
}
It seems llike it s the shortest solution withouy any additional data structures. Very lovely 
