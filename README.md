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


2021-01-26
Har fixat problem idag och har lagt till en lista med fel gissade bokstäver och ett stäle jag kommer ha min gubbe
jag har fixat så att när man gissar på rätt bokstav kommer det visa sig i "visibleword" och att om du har fått bort alla "_" ifrån visibleword eller om du får 10 fel kommer du att vinna/förlora (beror på, har inte gjort en "if" sats än) det jag har lagt till är en lista på bokstäver du har gissat och haft fel på som dator kollar emot varje gång du gissar och en string array med olika "frames" som jag kommer ha gubben i.
Koden ser ut såhär
import javax.swing.*;
import java.util.Random;

public class Hangman {
    public static void main(String[] args) {
        String word = pickRandomword();
        String  Ourword;
        int k = 0;
        int d = 0;
        char ourquess;
        String Visibleword = "";
        String[] gubben = {"Frame1","Frame2","Frame3","Frame4","Frame5","Frame6","Frame7","Frame8","Frame9","Frame10"}; // detta kommer vara guben men just nu är det bara olika frames
        String felgisning = "";

        while (d<word.length()){     //vill kunna få längden på det vallda ordet
            if (word.charAt(d) != ' ') {                 //Vill kunna kolla om karaktären i positionen d
                Visibleword = Visibleword + "_ ";        // är " " och om det är det ha ett mellanrum där
            } else {
                Visibleword = Visibleword + "  ";
            }
            d++;
        }
        while (k<10 && Visibleword.contains("_")){
            Ourword = JOptionPane.showInputDialog(null, gubben[k] + "\nDina Bokstäver du har gissat: " + felgisning + "\n" + Visibleword + " " + word); //here we should print the hangman the quessed letters, the Visibleword and it should ask the user for a letter im not sure if i should use a JOptionpane or the console for this
            ourquess = Ourword.charAt(0);
            if (! felgisning.contains(Ourword)) {
                if (word.contains(Ourword)) {
                    for (int i = 0; i < word.length(); i++) {
                        if (word.charAt(i) == ourquess) {
                            Visibleword = Visibleword.substring(0, i * 2) + word.charAt(i) + Visibleword.substring((i * 2) + 1);
                        }
                    }
                } else {
                    k++; //fick ett fel, borde också lägga till den gissade bokstaven till en lista
                    felgisning = felgisning + ourquess + ",";
                }
            } else {
                JOptionPane.showMessageDialog(null, "Du har redan gissat " + Ourword);
            }
        } //kommer utanför denna när när du har slut på gisnignar eller när du är klar
        JOptionPane.showMessageDialog(null, "yooo");
    }

    private static String pickRandomword() {
        String[] words = {"Jack O Lantern", "Jack O Lantern", "Jack O Lantern", "Jack O Lantern"};
        Random R = new Random();
        int randomNumber = R.nextInt(words.length);
        return words[randomNumber];
    }
}


2021-01-29
Har lagt till antal försök, "the visual acpect", att både stora och små bokstäver fungerar och att det händer olika saker om du vinner eller förlorar.
Gjorde så att om du gissar antligen en liten eller en stor bokstav fungerar det, jag ville ha det som att ordet hade både stora och små boksäver inuti sig skulle det fungera men jag valde att bara göra alla bokstäver stora och göra din gissning till en stor bokstav, jag hittade också en hänga gubbe "copy paste" för a programmet och att det stor på slutet olika medelanden om du vinner eller förlorar och att det visar hur många gånger du gissade innan du fick det vann/förlora

fixade också så at alla gisade bokstäver hamnar i en lista och vi kollar emot den eftersom det blev ett problem när vi också hade någonting som räknade antal försök vi använde




import javax.swing.*;
import java.util.Random;

public class Hangman {
    public static void main(String[] args) { //tja
        String word = pickRandomword();
        String  Ourword;
        int k = 0;
        int d = 0;
        int Tries = 0;
        char ourquess;
        String Visibleword = "";
        String felgisning = "";
        String[] gubben = {" ------\n" +
                "|     |\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|     +\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|    -+\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|    -+-\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|     |\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|     |\n" +
                "|    |\n" +
                "|    |\n" +
                "----------", " ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|     |\n" +
                "|    | |\n" +
                "|    | |\n" +
                "----------"};
        while (d<word.length()){     //vill kunna få längden på det vallda ordet
            if (word.charAt(d) != ' ') {                 //Vill kunna kolla om karaktären i positionen d
                Visibleword = Visibleword + "_ ";        // är " " och om det är det ha ett mellanrum där
            } else {
                Visibleword = Visibleword + "  ";
            }
            d++;
        }
        while (k<10 && Visibleword.contains("_")){
            Ourword = JOptionPane.showInputDialog(null, gubben[k] + "\nBokstäver du har gissat: " + felgisning + "\n" + Visibleword); //here we should print the hangman the quessed letters, the Visibleword and it should ask the user for a letter im not sure if i should use a JOptionpane or the console for this
            Ourword = Ourword.toUpperCase();
            ourquess = Ourword.charAt(0);
            if (! felgisning.contains(Ourword)) {
                felgisning = felgisning + ourquess + ",";
                Tries++;
                if (word.contains(Ourword)) {
                    for (int i = 0; i < word.length(); i++) {
                        if (word.charAt(i) == ourquess) {
                            Visibleword = Visibleword.substring(0, i * 2) + word.charAt(i) + Visibleword.substring((i * 2) + 1);
                        }
                    }
                } else {
                    k++; //fick ett fel.
                }
            } else {
                JOptionPane.showMessageDialog(null, "Du har redan gissat " + Ourword);
            }
        } //kommer utanför denna när när du har slut på gisnignar eller när du är klar
        if (k<10) {
            JOptionPane.showMessageDialog(null,  gubben[k] + "\n\nDu vann! \nOrdet var " + word + "\nDet tog " + Tries + " försök att få ordet");
        } else { //om du van ser du medelandet över och om du förlorade ser du det som är under
            JOptionPane.showMessageDialog(null,  gubben[k] + "\n\nFan han dog! \nDet här är ditt fel, ordet var " + word + " det borde inte varit så svårt\nDet tog dig " + Tries + " försök Men endå kunde du inte rädda han");
        }
    }

    private static String pickRandomword() {
        String[] words = {"JACK O LANTERN", "DANDARA", "UNDERTALE", "JACK THE RIPPER", "NEW PHONE WHO DIS", "PIE", "DEAD MEN TELL NO TALES", "MONKEY VS LIZARD"};
        Random R = new Random();
        int randomNumber = R.nextInt(words.length);
        return words[randomNumber];
    }
}



2021-02-02
Har fixat med att du kan välja antal försök och gubben "responderar" till det med vilken bild som visas och har fixat så att om du inte gissar någonting alls kommer inte programmet krasha.

import javax.swing.*;
import java.util.Random;

public class Hangman {
    public static void main(String[] args) { //tja
        String word = pickRandomword();
        String  Ourword;
        int k = 0;
        int d = 0;
        int Tries = 0;
        char ourquess;
        int försök = 0;
        String Check;
        String Visibleword = "";
        String felgisning = "";
        String[] gubben = {" ------\n" +
                "|     |\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|     +\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|    -+\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|    -+-\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|     |\n" +
                "|\n" +
                "|\n" +
                "----------"," ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|     |\n" +
                "|    |\n" +
                "|    |\n" +
                "----------", " ------\n" +
                "|     |\n" +
                "|     0\n" +
                "|   /-+-/\n" +
                "|     |\n" +
                "|     |\n" +
                "|    | |\n" +
                "|    | |\n" +
                "----------"};
        while (d<word.length()){     //vill kunna få längden på det vallda ordet
            if (word.charAt(d) != ' ') {                 //Vill kunna kolla om karaktären i positionen d
                Visibleword = Visibleword + "_ ";        // är " " och om det är det ha ett mellanrum där
            } else {
                Visibleword = Visibleword + "  ";
            }
            d++;
        }
        försök = Integer.parseInt(JOptionPane.showInputDialog(null, "Hur många försök vill du ha\nRekomenderat mellan 8 och 10"));
        while (k<försök && Visibleword.contains("_")){
            Ourword = "";
            while (Ourword.equals("")) {
                    Ourword = JOptionPane.showInputDialog(null, gubben[(k * 10) / försök] + "\nBokstäver du har gissat: " + felgisning + "\nfel: " + k + "/" + försök + "\n" + Visibleword); //here we should print the hangman the quessed letters, the Visibleword and it should ask the user for a letter im not sure if i should use a JOptionpane or the console for this
            }
            Ourword = Ourword.toUpperCase();
            ourquess = Ourword.charAt(0);
            if (! felgisning.contains(ourquess + "")) {
                felgisning = felgisning + ourquess + ",";
                Tries++;
                if (word.contains(ourquess+"")) {
                    for (int i = 0; i < word.length(); i++) {
                        if (word.charAt(i) == ourquess) {
                            Visibleword = Visibleword.substring(0, i * 2) + word.charAt(i) + Visibleword.substring((i * 2) + 1);
                        }
                    }
                } else {
                    k++; //fick ett fel.
                }
            } else {
                JOptionPane.showMessageDialog(null, "Du har redan gissat " + ourquess);
            }
        } //kommer utanför denna när när du har slut på gisnignar eller när du är klar
        if (k<försök) {
            JOptionPane.showMessageDialog(null,  gubben[(k*10)/försök] + "\n\nDu vann! \nOrdet var " + word + "\nDet tog " + Tries + " försök att få ordet");
        } else { //om du van ser du medelandet över och om du förlorade ser du det som är under
            JOptionPane.showMessageDialog(null,  gubben[(k*10)/försök] + "\n\nFan han dog! \nDet här är ditt fel, ordet var " + word + " det borde inte varit så svårt\nDet tog dig " + Tries + " försök Men endå kunde du inte rädda han");
        }
    }

    private static String pickRandomword() {
        String[] words = {"JACK O LANTERN", "DANDARA", "UNDERTALE", "JACK THE RIPPER", "NEW PHONE WHO DIS", "PIE", "DEAD MEN TELL NO TALES", "MONKEY VS LIZARD", "yoooooo", ""};
        Random R = new Random();
        int randomNumber = R.nextInt(words.length);
        return words[randomNumber];
    }
}

