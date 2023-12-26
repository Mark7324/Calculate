import java.util.Scanner;

public class Main {
    public static void main(String[] args) throws Exception {
        System.out.println(Roman.convertToRoman(4));
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите два числа: ");
        String expression = scanner.nextLine();
        System.out.println(parse(expression));


    }
    public static String parse(String expression) throws Exception{
        int a, b;
        String oper;
        String result;
        boolean isRoman;
        String[] operands = expression.split("[+\\-*/]");
        if(operands.length!=2) throw new Exception("Должно быть два операнда");
        oper = detectOperation(expression);
        if(oper==null) throw new Exception("Непроддерживаемая матем. опреция");
        if(Roman.isRoman(operands[0])&&Roman.isRoman(operands[1])){
            a=Roman.convertToArabian(operands[0]);
            b=Roman.convertToArabian(operands[1]);
            isRoman=true;
        } else if (!Roman.isRoman(operands[0])&&!Roman.isRoman(operands[1])) {
            a=Integer.parseInt(operands[0]);
            b=Integer.parseInt(operands[1]);
            isRoman=false;
        }else {
            throw new Exception("Числа должны быть в одном формате");
        }
        if(a>10||b>10)
            throw new Exception("Числа должны быть от 1 до 10");
        int arabian = calc(a,b,oper);
        if(isRoman==true){
            if(arabian<=0)
                throw new Exception("Римское число должно быть больше нуля");
            result = Roman.convertToRoman(arabian);
        }
        else{
            result = String.valueOf(arabian);
        }
        return result;
    }

    static int calc(int a, int b, String oper){
        if(oper.equals("+")) return a+b;
        else if(oper.equals("-")) return a-b;
        else if(oper.equals("*")) return a*b;
        else return a/b;

    }


    static String detectOperation(String expression){
        if(expression.contains("+"))return "+";
        else if (expression.contains("-"))return "-";
        else if (expression.contains("*"))return "*";
        else if (expression.contains("/"))return "/";
        else return null;
    }
}

class Roman{
    static String[] romanArray = new String[]{"0","I","II","III","IV","V","VI","VII","VIII","IX","X","XI","XII","XIII","XIV","XV","XVI","XVII","XVIII",
    "XIX","XX","XXI","XXIV","XXV","XXVII","XXVIII","XXX","XXXII","XXXV","XXXVI","XL","XLII","XLV","XLVIII","XLIX","L","LIV","LVI","LX","LXIII","LXIV",
    "LXX","LXXII","lxxx","LXXXI","XC","C"};

    public static boolean isRoman(String v){
        for(int i = 0; i< romanArray.length; i++){
            if(v.equals(romanArray[i]))
                return true;
        }
        return false;
    }
    public static int convertToArabian(String roman){
        for(int i = 0; i< romanArray.length;i++){
            if(roman.equals(romanArray[i])) return i;
        }
        return -1;
    }
    public static String convertToRoman(int arabian){
        return romanArray[arabian];
    }
}
