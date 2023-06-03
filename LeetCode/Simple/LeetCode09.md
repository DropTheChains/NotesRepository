```java
public class Leet09 {  
    /**  
     * 给你一个整数 x ，如果 x 是一个回文整数，返回 true ；否则，返回 false 。  
     * <p>  
     * 回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。  
     * <p>  
     * 例如，121 是回文，而 123 不是。  
     *  
     * @param args  
     */  
    public static void main(String[] args) {  
        System.out.println(isPalindrome(-121));  
    }  
  
    public static boolean isPalindrome(int x) {  
        String value = String.valueOf(x);  
        String restring = new StringBuffer(value).reverse().toString();  
        if (restring.equals(value)) {  
            return true;  
        }  
        return false;  
  
    }  
}
```
