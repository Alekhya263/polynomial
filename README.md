# polynomial
#You have a quadratic polynomial of the form:  𝑓 ( 𝑥 ) = 𝑎 𝑥 2 + 𝑏 𝑥 + 𝑐 f(x)=ax^2+bx+c  where  𝑎 ,  𝑏 , and  𝑐  are constants, and  𝑐 is the constant term you want to find.
import org.json.JSONObject;
import org.json.JSONTokener;

import java.io.FileInputStream;
import java.util.Iterator;

public class DecodeBases {

    public static void main(String[] args) {
        try {
            // Load JSON from file
            FileInputStream fis = new FileInputStream("data.json");
            JSONTokener tokener = new JSONTokener(fis);
            JSONObject json = new JSONObject(tokener);

            // Iterate over keys
            Iterator<String> keys = json.keys();
            while (keys.hasNext()) {
                String key = keys.next();

                // Skip the "keys" object
                if (key.equals("keys")) {
                    continue;
                }

                JSONObject entry = json.getJSONObject(key);
                String baseStr = entry.getString("base");
                String valueStr = entry.getString("value");

                int base = Integer.parseInt(baseStr);

                // Convert value string from the given base to decimal integer
                int decimalValue = Integer.parseInt(valueStr, base);

                System.out.println("Key " + key + ": value '" + valueStr + "' in base " + base + " = " + decimalValue + " in decimal");
            }

            fis.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

