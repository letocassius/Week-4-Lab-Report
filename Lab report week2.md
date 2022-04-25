# **week 4 lab report 2**
## Yichen Le

# Original Code And Test File
> Original Code:

```
// File reading code from https://howtodoinjava.com/java/io/java-read-file-to-string-examples/
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class MarkdownParse {
    public static ArrayList<String> getLinks(String markdown) {
        ArrayList<String> toReturn = new ArrayList<>();
        // find the next [, then find the ], then find the (, then take up to
        // the next )
        int currentIndex = 0;
        while(currentIndex < markdown.length()) {
            int nextOpenBracket = markdown.indexOf("[", currentIndex);
            int nextCloseBracket = markdown.indexOf("]", nextOpenBracket);
            int openParen = markdown.indexOf("(", nextCloseBracket);
            int closeParen = markdown.indexOf(")", openParen);
            toReturn.add(markdown.substring(openParen + 1, closeParen));
            currentIndex = closeParen + 1;
        }
        return toReturn;
    }
    public static void main(String[] args) throws IOException {
	Path fileName = Path.of(args[0]);
	String contents = Files.readString(fileName);
        ArrayList<String> links = getLinks(contents);
        System.out.println(links);
    }
} 
```

> Original Test File:

```
# Title

[a link!](https://something.com)
[another link!](some-page.html)
```

## Bug #1
> This is the [link](test1.md) to the first test file that I wrote.
> Symptom: the program has printed the letters that I put in the ( ) wich is not a link. 
<img width="671" alt="image" src="https://user-images.githubusercontent.com/64039891/165014403-f7d17db4-76b4-45fc-8517-3f51fe4587dd.png">


## Code Improvement #1
<img width="788" alt="image" src="https://user-images.githubusercontent.com/64039891/165015145-550fdd41-6d55-4aef-a731-52404801391d.png">
Since we wana make sure what gets extracted from the brackets is a link and not some randome letters. I have modified the code so it is now looking for "](" in stead of "(". Now we are searching for "](" all at once instead of doing to seperately. By doing this we could make sure that the methods extracts a correct link. 

## Bug #2
> This is the [link](test2.md) to the second test file that I wrote.
> Symptom: after about 30 seconds the program stop becasue of a OutOfMemoryError. This is caused becaue I added some random line after the last link, so now the program has no way to exsit the while loop. 
<img width="725" alt="image" src="https://user-images.githubusercontent.com/64039891/165016120-6df1948a-c97c-49c9-bbbc-0270ebdeaa00.png">

## Code Improvement #2
<img width="725" alt="image" src="https://user-images.githubusercontent.com/64039891/165016430-5f49e0dd-a503-40f0-953c-5a641913ac85.png">
The bug occurs because the program has no way to exit the while loop when there is some line after the las t link. Therefore I have added a break command so when the file does not end with a link. By breaking the loop when index is -1. The program will still be able to exit the while loop and execute the program.

## Bug #3
> This is the [link](test3.md) to the third test file that I wrote.
<img width="652" alt="image" src="https://user-images.githubusercontent.com/64039891/165017110-0fca9ca5-6b90-4ec4-ada4-7e2ee1150b04.png">
This time I have added a image in to the file, and the program has taken the image information as a link and printed it out.

## Code Improvement #3

