# Hangman
 Hangman    Min kod finns i ett annat repo för tillfället men har kopierat in en kopia i botten av documentet

2021-01-15
Har skapat min fil idag och gjort en ordslumpare
jag har också jobbat med att göra ordet till en rad av mellanslag och understreck för använder ---> "_ _ _  _ _ _ _" Men har kommit in i ett problem, jag vet inte hur jag ska kolla om karatären i position (d) är ett mellanslag elller inte och hur jag kollar det i en "if" sats.
Det jag ska göra nästa lektion är att fixa Det jag skrev om övre och börja med delen om att gisa en bokstav.



______________________________________________________________________________________________________________________________________________________________________________
import javax.swing.*;
import java.util.Random;

public class Hangman {
    public static void main(String[] args) {
        String word = pickRandomword();
        String Wrongword = "";
        int k = 0;
        int d = 0;
        String Visibleword = "_";

        while (d<word.length()){     //vill kunna få längden på det vallda ordet
            if (word.charAt(d) != " ") {                 //Vill kunna kolla om karaktären i positionen d
                Visibleword = Visibleword + " _";        // är " " och om det är det ha ett mellanrum där
            } else {
                Visibleword = Visibleword + "  ";
            }
            d++;
        }
        JOptionPane.showMessageDialog(null, Visibleword + word); //just checkin
        while (k<10 || !Visibleword.contains("_")){
            k++;
            System.out.println(); //here we should print the hangman the quessed letters, the Visibleword and it should ask the user for a letter im not sure if i should use a JOptionpane or the console for this
        } //kommer utanför denna när när du har slut på gisnignar eller när du är klar
    }

    private static String pickRandomword() {
        String[] words = {"ett", "tvås", "Trete", "Jack O Lantern"};
        Random R = new Random();
        int randomNumber = R.nextInt(words.length);
        return words[randomNumber];
    }
}


2021-01-19
Jag har gjort mycket idag, har fixat så att mitt valda ord har blivit tex "_ _ _ _   _   _ _ _ _ _ _ _ " *Jack o lantern
har också gjort så man kan gissa på ett ord och att det kollar om det är rätt eller inte.
Det enda jag har kvar är att fixa så att om man får fel sparar det din gissning och proggrament "hänger" gubben mer och att fixa så att när man gissar rätt till exempel om man hade gissat "a", "j" och "n" skulle det bli "J a _ _   _   _ a n _ _ _ n "
Nästa lektion ska jag först fixa att "reaveala" Bokstäver sedan ska jag göra gubben och spara bokstäver.

Under här är den nya koden om du inte orkar gå till "Helloworlds"
import javax.swing.*;
import java.util.Random;

public class Hangman {
    public static void main(String[] args) {
        String word = pickRandomword();
        String  Ourword;
        int k = 0;
        int d = 0;
        int i;
        char ourquess;
        String Visibleword = "";

        while (d<word.length()){     //vill kunna få längden på det vallda ordet
            if (word.charAt(d) != ' ') {                 //Vill kunna kolla om karaktären i positionen d
                Visibleword = Visibleword + "_ ";        // är " " och om det är det ha ett mellanrum där
            } else {
                Visibleword = Visibleword + "  ";
            }
            d++;
        }
        while (k<10 || !Visibleword.contains("_")){
            Ourword = JOptionPane.showInputDialog(null, Visibleword + " " + word); //here we should print the hangman the quessed letters, the Visibleword and it should ask the user for a letter im not sure if i should use a JOptionpane or the console for this
            ourquess = Ourword.charAt(0);
            if (word.contains(Ourword)) {
                for (i=0; i<word.length(); i++) {
                    if (word.charAt(i) == ourquess) {
                        Visibleword.charAt(i*2) = ourquess; //Question, how do i change a character at a certain point in a string
                    }
                }
            } else {
                k++;
            }
        } //kommer utanför denna när när du har slut på gisnignar eller när du är klar
        System.out.println(Visibleword + " the word is " + word);
    }

    private static String pickRandomword() {
        String[] words = {"Jack O Lantern", "Jack O Lantern", "Jack O Lantern", "Jack O Lantern"};
        Random R = new Random();
        int randomNumber = R.nextInt(words.length);
        return words[randomNumber];
    }
}
