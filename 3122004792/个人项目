package org.example;
import java.io.*;

public class Main {
    public static void main(String[] args) {

        if (args.length < 3) {
            System.out.println("错误");//读取到文件小于3个
            return;
        }

        String originalFilePath = args[0];
        String plagiarizedFilePath = args[1];
        String outputFilePath = args[2];

        String originalContent = FileLoader.loadFile(originalFilePath);
        String plagiarizedContent = FileLoader.loadFile(plagiarizedFilePath);

        double plagiarismRate = calculatePlagiarismRate(originalContent, plagiarizedContent);

        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter(outputFilePath));
            writer.write(String.format("%.2f", plagiarismRate));
            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


    private static double calculatePlagiarismRate(String originalText, String copiedText) {//将文档分为小字符串
        String[] originalWords = originalText.split("[。,\\s\t\n]+");
        String[] copiedWords = copiedText.split("[。,\\s\t\n]+");

        int originalWordCount = originalWords.length;
        int copiedWordCount = copiedWords.length;
        int commonWordCount = 0;

        for (int i = 0; i < originalWords.length; i++) {
            for (int j = 0; j < copiedWords.length; j++) {
                if (originalWords[i].length() >= 4 && copiedWords[j].length() >= 4) {
                    if (originalWords[i].substring(0, 4).equals(copiedWords[j].substring(0, 4))) {
                        commonWordCount++;
                        break;
                    }
                }
            }
        }

        return ((double) commonWordCount / originalWordCount) * 100;
    }

}

class FileLoader {
    public static String loadFile(String filePath) {//读取文档
        StringBuilder content = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                content.append(line).append("\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        return content.toString();
    }
}

