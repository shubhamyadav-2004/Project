package Important_question;
import java.util.*;

public class LargestHexagonRectangle {
    public static void main(String[] args) {
        Scanner scr = new Scanner(System.in);
        int n = scr.nextInt();
        int [] arr = new int[n];
        int [] nse = new int[n];
        int [] pse = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = scr.nextInt();
        }

        Stack<Integer> str = new Stack<>();
        nse[n-1] = n;
        str.push(n-1);
        for(int i=n-2;i>=0;i--){
            while (str.size()>0 && arr[str.peek()]>arr[i]) {
                str.pop();
            }
            if(str.size() == 0) nse[i] = n;
            else nse[i] = str.peek();
            str.push(i);

        }

        while (str.size()>0) str.pop();

        pse[0] = -1;
        str.push(0);
        for(int i = 1;i<n;i++){
            while (str.size()>0 && arr[str.peek()]>arr[i]) {
                str.pop();
                
            }
            if(str.size() ==0) pse[i] = -1;
            else pse[i] = str.peek();
            str.push(i);
        }
        System.out.println(max(arr,nse,pse));
    }
    public static int max(int[] arr , int[] nse,int[] pse){
        int max = -1;
        int n = arr.length;
        for(int i=0;i<n;i++){
            int area = arr[i] * (nse[i]-pse[i]-1);
            max = Math.max(area,max);
        }
        return max;
    }
    
}
