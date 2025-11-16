    import java.util.*;
    
    public class Scrabble {
        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
    
            String[] lettersInput = sc.nextLine().replaceAll("\\s|,", "").split("");
            char[] word = new char[4];
            for (int i = 0; i < 4; i++) {
                word[i] = lettersInput[i].charAt(0);
            }
    
            int[] starts = new int[5];
            for (int i = 0; i < 5; i++) {
                starts[i] = sc.nextInt();
            }
    
            Map<Character, Integer> letterValue = new HashMap<>();
            letterValue.put('A',1); letterValue.put('E',1);
            letterValue.put('D',2); letterValue.put('R',2);
            letterValue.put('B',3); letterValue.put('M',3);
            letterValue.put('V',4); letterValue.put('Y',4);
            letterValue.put('J',8); letterValue.put('X',8);
    
            Set<Integer> DL = new HashSet<>(Arrays.asList(3,9,15,21,27,33,39));
            Set<Integer> TL = new HashSet<>(Arrays.asList(5,10,20,25,30,35,40));
            Set<Integer> DW = new HashSet<>(Arrays.asList(7,14,28));
            Set<Integer> TW = new HashSet<>(Arrays.asList(8,16,24,32,40));
    
            for (int s : starts) {
                int total = 0;
                int wordMultiplier = 1;
    
                for (int i = 0; i < 4; i++) {
                    int square = s + i;
                    char letter = word[i];
                    int value = letterValue.getOrDefault(letter, 0);
    
                    if (DL.contains(square)) value *= 2;
                    else if (TL.contains(square)) value *= 3;
    
                    total += value;
    
                    if (DW.contains(square)) wordMultiplier = 2;
                    else if (TW.contains(square)) wordMultiplier = 3;
                }
    
                total *= wordMultiplier;
                System.out.println(total);
            }
    
            sc.close();
        }
    }

