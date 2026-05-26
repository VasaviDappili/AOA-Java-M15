
# EX 5C Graph coloring
## DATE: 26/05/2026
## AIM:
To write a Java program to for given constraints.
Problem Description:
In a hilly region, several radio towers are installed to provide communication services. However, due to signal interference, two adjacent towers (i.e., in communication range of each other) must not use the same frequency channel.

You are given N radio towers and their communication ranges represented as an undirected graph. Your task is to assign channels (colors) to these towers using at most M channels such that no two adjacent towers use the same channel.

Write a program to determine if such an assignment is possible or not.

Input Format:
First line contains two integers: N (number of towers), and M (number of available frequency channels).

Next line contains an integer E — number of edges representing the communication range.

Next E lines contain two integers u and v — representing that tower u and tower v are within range (0-based index).

Output Format:
Print "YES" if it's possible to assign frequencies to towers such that no two adjacent towers have the same frequency.

Otherwise, print "NO".

<img width="182" height="440" alt="image" src="https://github.com/user-attachments/assets/b32078a2-c79d-4a25-88c4-e51144b5456f" />


## Algorithm
1. Input & Graph Construction:
Read number of towers n, available channels m, and connections e.
Build an adjacency list representing connections between towers (edges).
2. Color Representation:
Create a color[] array where color[i] stores the assigned channel for tower i.
Initially, all towers are uncolored (0).
3. Recursive Backtracking (isColorable):
For each tower (node), try assigning channels (colors) from 1 to m.
Before assigning, check if the channel is safe using the isSafe() function.
4. Safety Check (isSafe):
Ensure no adjacent (connected) tower has the same channel.
If safe, assign the channel and recursively color the next tower.
If no valid channel exists, backtrack by resetting the color. 
5. Result:
If all towers can be assigned valid channels → print "YES".
Otherwise → print "NO" (conflict in channel assignment).  

## Program:
```
Program to implement Reverse a String
Developed by: Dappili Vasavi
Register Number: 212223040030
import java.util.*;

public class RadioTowerChannelAssignment {

    
    public static boolean isSafe(List<List<Integer>> graph, int[] color, int node, int c) {
        for (int neighbour : graph.get(node)) {
            if (color[neighbour] == c) {
                return false; 
            }
        }
        return true;
    }

    
    public static boolean isColorable(List<List<Integer>> graph, int[] color, int node, int m, int n) {
        if (node == n) return true; 

       
        for (int c = 1; c <= m; c++) {
            if (isSafe(graph, color, node, c)) {
                color[node] = c; 
                if (isColorable(graph, color, node + 1, m, n))
                    return true;
                color[node] = 0; 
            }
        }
        return false; 
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); 
        int m = sc.nextInt(); 
        int e = sc.nextInt();

        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++)
            graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] color = new int[n];

        if (isColorable(graph, color, 0, m, n))
            System.out.println("YES");
        else
            System.out.println("NO");

        sc.close();
    }
}
 
```

## Output:
<img width="411" height="491" alt="image" src="https://github.com/user-attachments/assets/80a5bcb4-a0bb-44f6-a6e4-0c389e78284c" />



## Result:
The program successfully implemented and the expected output is verified.
