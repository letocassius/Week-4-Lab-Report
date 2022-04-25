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
>This is the [link](test1.md) to the first test file that I wrote.
>Symptom: the program has printed the letters that I put in the ( ) wich is not a link. 
<img width="671" alt="image" src="https://user-images.githubusercontent.com/64039891/165014403-f7d17db4-76b4-45fc-8517-3f51fe4587dd.png">


## Code Improvement #1
<img width="788" alt="image" src="https://user-images.githubusercontent.com/64039891/165015145-550fdd41-6d55-4aef-a731-52404801391d.png">
Since we wana make sure what gets extracted from the brackets is a link and not some randome letters. I have modified the code so it is now looking for "](" in stead of "(". Now we are searching for "](" all at once instead of doing to seperately. By doing this we could make sure that the methods extracts a correct link. 
