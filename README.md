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
