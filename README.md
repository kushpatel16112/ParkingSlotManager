# Parking Management System

## Overview
This project is a **Parking Management System** implemented in Java. It provides a console-based interface to manage the parking slots in a parking lot. The system allows users to enter cars, remove them when they exit, and calculate parking fees based on the duration of their stay. It also maintains a record of the available and occupied parking slots.

## Features
- **Car Entry:** Users can enter their details (name, car number, mobile number) to park their cars in available slots.
- **Car Exit:** When a car exits, the system calculates the total parking time and charges accordingly.
- **Display Receipts:** Both entry and exit receipts are displayed to the user.
- **Pre-filled Slots:** A few slots are pre-filled with dummy data for testing purposes.
- **Parking Suggestions:** The system can suggest parking slots based on availability.
- **Validations:** Mobile number and car number are validated for correct format.

## Project Structure
- `parking.java`: Contains the main class that runs the application.
- `Slots.java`: Contains the class that handles parking slots, car details, and parking management logic.

## Important Methods

### 1. `Defult_Entry(Slots[][] arr)`
This method initializes the parking system with a few pre-filled parking slots. It simulates the presence of a few parked cars at the start of the system and helps to test the program.

#### Explanation:
- Fills specific slots in the parking grid (e.g., arr[0][0], arr[0][2], etc.) with dummy car details such as the car number, owner's name, and the mobile number.
- The current date and time are set as the entry time for these cars.

**Example:**
```java
arr[0][0].slot_full = true;
arr[0][0].Name = "PATEL RISHI";
arr[0][0].Car_no = "GJ01AB0801";
arr[0][0].Mobile_no = 1234567891;
arr[0][0].Enter_Date_Time = dtf.format(now);
arr[0][0].Sloat_no = 1;
```
### 2. `Check_Mobile_No()`
This method ensures that the user inputs a valid 10-digit mobile number. It checks the length of the input and verifies that all characters are digits.

#### Explanation
- If the mobile number entered has less than or more than 10 digits, the user is prompted to re-enter the number.
- It uses a loop to ensure that only digits are entered for the mobile number.

**Example:**
```
if (s.length() == 10) {
    for (int j = 0; j < 10; j++) {
        if (s.charAt(j) >= '0' && s.charAt(j) <= '9') {
            count++;
        } else {
            System.out.println("Enter Only Digit For Mobile No");
            break;
        }
    }
}
```

### 3. `Check_Car_No()`
This method validates the format of the car number. The format must be in the pattern GJ12AB1234, where the first two characters are alphabets, followed by two digits, then two more alphabets, and finally four digits.

#### Explanation
- It enforces the correct format by checking each part of the string.
- If the car number does not match the pattern, the user is prompted to re-enter it.

**Example:**
```
if (j == 2 || j == 3 || j == 6 || j == 7 || j == 8 || j == 9) {
    if (s.charAt(j) >= '0' && s.charAt(j) <= '9') {
        count++;
    } else {
        System.out.println("Enter Only Digit For " + (j+1) + " character");
        break;
    }
} else {
    if (s.charAt(j) >= 'A' && s.charAt(j) <= 'Z') {
        count++;
    } else {
        System.out.println("Enter Only A To Z For " + (j+1) + " character");
        break;
    }
}
```

### 4. `Enter_Detail(Slots[][] arr)`
This method handles the process of entering the car details when a car arrives at the parking lot. It checks if the parking lot is full and then assigns a slot to the car.

#### Explanation
- It asks the user to enter their name, car number, and mobile number.
- The car number is checked to ensure it does not already exist in the parking lot.
- It assigns the first available slot to the car.
- The system records the entry time.

**Example:**
```
System.out.print("Enter customer Name: ");
String C_Name = sc.nextLine();
String C_car_No = Check_Car_NO(arr);
long C_Mobile_no = Check_Mobile_No();
LocalDateTime now = LocalDateTime.now();
arr[colum][row].Enter_Date_Time = dtf.format(now);

```


### 5. `Exit_Detail(Slots[][] arr)`
This method is called when a car exits the parking lot. It calculates the total time the car was parked and generates a receipt.

#### Explanation
- The system checks the car number, retrieves the entry time, and calculates the total minutes the car was parked.
- Based on the parking time, a fee is calculated.
- A receipt is generated that includes the car number, entry and exit times, and the total amount due.

**Example:**
```
LocalDateTime entry = LocalDateTime.parse(arr[i][j].Enter_Date_Time, dtf);
LocalDateTime exit = LocalDateTime.now();
Duration duration = Duration.between(entry, exit);
arr[i][j].Total_Minutes = duration.toMinutes();
arr[i][j].payment = calculateParkingFee(arr[i][j].Total_Minutes);
```


### 6. `Display_Receipt(Slots[][] arr)`
This method displays the parking receipt after a car has successfully entered the parking lot.

#### Explanation
- It prints the car's details, including the owner's name, car number, mobile number, and the assigned slot.

**Example:**
```
System.out.println("Parking Receipt");
System.out.println("Name: " + arr[colum][row].Name);
System.out.println("Car Number: " + arr[colum][row].Car_no);
System.out.println("Slot Number: " + arr[colum][row].Sloat_no);
```

### 7. `Display_Payment_Receipt(Slots[][] arr)`
This method displays the payment receipt when a car exits the parking lot.

#### Explanation
- It shows the details of the parked car, the total time it was parked, and the parking fee.

**Example:**
```
System.out.println("Payment Receipt");
System.out.println("Car Number: " + arr[i][j].Car_no);
System.out.println("Total Time Parked: " + arr[i][j].Total_Minutes + " minutes");
System.out.println("Amount Due: $" + arr[i][j].payment);
```

## How to Run the Program

1. **Clone or download the project.**
   ```bash
   git clone https://github.com/kushpatel16112/ParkingSlotManager.git
   ```

2. **Compile the Java files using a Java compiler:**
   ```bash
   javac parking.java
   ```

3. **Run the main class to start the Parking Management System:**
   ```bash
   java parking
   ```

4. **Follow the on-screen instructions to manage car entries and exits.**

## Future Enhancements
- Add a graphical user interface (GUI) for better user interaction.
- Support for different vehicle types (e.g., bikes, trucks).
- Dynamic pricing based on vehicle size or duration.
