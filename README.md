import java.util.Scanner;

class HealthAssessment {

    public String assessHealth(int heartRate, double temperature, String[] symptoms) {
        if (heartRate <= 0 || temperature <= 0) {
            return "Invalid input";
        }

        String healthStatus = "Normal";

        if (temperature > 37.5) {
            healthStatus = "Fever detected";
        }

        if (heartRate < 60 || heartRate > 100) {
            healthStatus = "Abnormal heart rate";
        }

        for (String symptom : symptoms) {
            symptom = symptom.toLowerCase();
            if (symptom.contains("chest pain") || 
                symptom.contains("difficulty breathing") || 
                symptom.contains("severe headache")) {
                healthStatus = "Critical condition";
                break;
            }
        }

        return healthStatus;
    }

    public String getRecommendation(String healthStatus) {
        switch (healthStatus) {
            case "Normal":
                return "You are stable. Maintain healthy habits.";
            case "Fever detected":
                return "Take rest, drink fluids, and monitor your temperature.";
            case "Abnormal heart rate":
                return "Avoid stress and consult a doctor if issue persists.";
            case "Critical condition":
                return "Seek immediate medical assistance.";
            default:
                return "Invalid data provided.";
        }
    }
}

public class SmartHealthcareSystem {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("----- SMART HEALTHCARE SYSTEM -----");
        
        System.out.print("Enter Heart Rate (BPM): ");
        int heartRate = sc.nextInt();

        System.out.print("Enter Body Temperature (°C): ");
        double temperature = sc.nextDouble();
        sc.nextLine();

        System.out.print("Enter Symptoms (comma separated): ");
        String symptomInput = sc.nextLine();
        String[] symptoms = symptomInput.split(",");

        HealthAssessment ha = new HealthAssessment();

        String status = ha.assessHealth(heartRate, temperature, symptoms);
        String advice = ha.getRecommendation(status);

        System.out.println("\n--- RESULT ---");
        System.out.println("Health Status: " + status);
        System.out.println("Recommendation: " + advice);

        sc.close();
    }
}

