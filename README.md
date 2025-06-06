import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class project {

    
    public static int lcsLength(String X, String Y) {
        int m = X.length();
        int n = Y.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (X.charAt(i) == Y.charAt(j)) {
                    dp[i + 1][j + 1] = dp[i][j] + 1;
                } else {
                    dp[i + 1][j + 1] = Math.max(dp[i + 1][j], dp[i][j + 1]);
                }
            }
        }
        return dp[m][n];
    }

    
    public static double calculateSimilarity(String text1, String text2) {
        text1 = text1.replaceAll("\\s+", "").toLowerCase();
        text2 = text2.replaceAll("\\s+", "").toLowerCase();

        int lcsLen = lcsLength(text1, text2);
        int maxLen = Math.max(text1.length(), text2.length());

        return ((double) lcsLen / maxLen) * 100;
    }

    
    public static String readFileContent(String path) throws IOException {
        return new String(Files.readAllBytes(Paths.get(path)));
    }

    
    public static void main(String[] args) {

        String filePath1 = "C:\\Users\\ASUS\\Desktop\\ada project\\AI.txt";
        String filePath2 = "C:\\Users\\ASUS\\Desktop\\ada project\\DS.txt";

        try {
            String doc1 = readFileContent(filePath1);
            String doc2 = readFileContent(filePath2);

            double similarity = calculateSimilarity(doc1, doc2);
            System.out.printf("Similarity based on LCS: %.2f%%\n", similarity);

        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}
