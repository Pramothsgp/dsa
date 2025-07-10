Problem Statement



Consider a rat placed at (0, 0) in a square matrix of order N*N. It has to reach the destination at (N – 1, N – 1). Find all possible paths that the rat can take to reach from the source to the destination. The directions in which the rat can move are ‘U'(up), ‘D'(down), ‘L’ (left), and ‘R’ (right). Value 0 at a cell in the matrix represents that it is blocked and the rat cannot move to it while value 1 at a cell in the matrix represents that the rat can travel through it. Return the list of paths in lexicographically increasing order.



Note: In a path, no cell can be visited more than once. If the source cell is 0, the rat cannot move to any other cell.



Example 1



Input:

N = 4

m[][] =

{{1, 0, 0, 0},

{1, 1, 0, 1},

{1, 1, 0, 0},

{0, 1, 1, 1}}

Output:

DDRDRR DRDDRR

Explanation:

The rat can reach the destination at (3, 3) from (0, 0) by two paths - DRDDRR and DDRDRR, when printed in sorted order we get DDRDRR DRDDRR.



Example 2



Input:

N = 2

m[][] = 

{{1, 0},

{1, 0}}

Output:

-1

Explanation:

No path exists and the destination cell is blocked.

Input format :
The first line of input contains an integer n, representing the size of the maze.

The next n lines each contain n space-separated integers, representing the maze.

Output format :
The output consists of

If at least one path is found, print all valid paths as space-separated strings.

If no path is found, prints -1.



Refer to the sample output for the formatting specifications.

Code constraints :
In this scenario, the given test cases will fall under the following constraints:

2 ≤ N ≤ 5

0 ≤ m[i][j] ≤ 1

The initial and final cell will always be 1.

Sample test cases :
Input 1 :
4
1 0 0 0
1 1 0 1
1 1 0 0
0 1 1 1 
Output 1 :
DDRDRR DRDDRR
Input 2 :
2
1 0
1 0
Output 2 :
-1
Input 3 :
3
1 1 1
0 1 0
0 1 1
Output 3 :
RDDR

class RatInTheMaze {
    private static void findPath(int x , int y , int[][] maze ,int n, List<String> res , StringBuilder cur){
        if(x < 0 || y < 0 || x >= n || y >= n || maze[x][y] == 0) return;
        
        if(x == n - 1 && y == n - 1){
            res.add(cur.toString());
        }
        maze[x][y] = 0;
        
        cur.append('D');
        findPath(x + 1 , y , maze , n, res , cur);
        cur.deleteCharAt(cur.length() - 1);
        
        cur.append('L');
        findPath(x , y - 1, maze , n, res , cur);
        cur.deleteCharAt(cur.length() - 1);
        
        cur.append('R');
        findPath(x , y + 1, maze ,n ,res , cur);
        cur.deleteCharAt(cur.length() - 1);
        
        cur.append('U');
        findPath(x - 1 , y , maze , n, res , cur);
        cur.deleteCharAt(cur.length() - 1);
        
        maze[x][y] = 1;
    }
        public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        scanner.nextLine();

        int[][] maze = new int[n][n];
        for (int i = 0; i < n; i++) {
            String[] row = scanner.nextLine().split(" ");
            for (int j = 0; j < n; j++) {
                maze[i][j] = Integer.parseInt(row[j]);
            }
        }

        List<String> result = new ArrayList<>();
        StringBuilder currentPath = new StringBuilder();

        if (maze[0][0] != 0 && maze[n - 1][n - 1] != 0) {
             findPath(0, 0, maze, n, result, currentPath);
        }

        if (result.isEmpty()) {
            System.out.println(-1);
        } else {
            System.out.println(String.join(" ", result));
        }
    }
}