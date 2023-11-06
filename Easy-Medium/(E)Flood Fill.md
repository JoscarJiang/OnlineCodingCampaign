# 9 Flood Fill

**Leetcode Link:** [https://leetcode.com/problems/flood-fill/description/)

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75


An image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image.

You are also given three integers sr, sc, and color. You should perform a flood fill on the image starting from the pixel image[sr][sc].

To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with color.

Return the modified image after performing the flood fill.

Example 1: Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, color = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.


### Code

```python

class Solution(object):
    def floodFill(self, image, sr, sc, color):
        m = len(image)
        n = len(image[0])
        original_color = image[sr][sc]
        # 4 directionally: means for two pixel [x1,y1] [x2,y2], it should be |x1-x2| <=1 or |y1-y2| <=1 
        def flood(rr, cc):
            # stop if the coordinates are out of bounds, don't match the original color, or are already filled with the new color
            if rr < 0 or rr >= m or cc < 0 or cc >= n \
            or image[rr][cc] != original_color or image[rr][cc] == color:
                return
            
            image[rr][cc] = color
            # right, left, down, and up
            directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]
            for dr, dc in directions:
                new_row, new_col = rr + dr, cc + dc
                flood(new_row, new_col)

        flood(sr, sc)
        return image

      
 ```


### Analysis
-- do a recursion, set up base cases to stop the recursion: if the coordinates are out of bounds, don't match the original color, or are already filled with the new color, return without further recursion.

