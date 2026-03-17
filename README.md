## EX. NO: 05 — Simple Calculator App

### AIM:

To develop a program to create a simple calculator using Android Studio that performs basic arithmetic operations such as addition, subtraction, multiplication, and division.

### ALGORITHM / PROCEDURE:

Open Android Studio.

Create a new project named SimpleCalculator.

Select Empty Activity and click Finish.

Design the Layout (activity_main.xml):

Open the activity_main.xml file.

Use EditText to display the input and result.

Add Buttons for digits (0–9) and operators (+, −, ×, ÷, =, C).

Arrange the buttons in a GridLayout or LinearLayout for proper alignment.

Set up Button IDs:

Assign unique IDs for each button (e.g., btn1, btnAdd, btnEqual, etc.).

Assign an ID for the result display (EditText or TextView).

Write Java/Kotlin Code (MainActivity.java or MainActivity.kt):

Initialize all buttons and EditText using findViewById().

Set onClickListeners for each button to handle user input.

Store operands and the selected operation.

Perform calculations when the ‘=’ button is pressed.

Display the result in the EditText/TextView.

Run the Application:

Connect a physical device or start an Android Emulator.

Click Run ▶ to launch the app.

Test all arithmetic operations for accuracy.
### Program:

Main_activity.java

```

package com.example.calc;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    TextView tvInput, tvExpression;
    double num1 = 0, num2 = 0;
    String operator = "";
    boolean isNewOp = true;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tvInput = findViewById(R.id.tvInput);
        tvExpression = findViewById(R.id.tvExpression);
    }

    public void numberEvent(View view) {
        if (isNewOp) tvInput.setText("");
        isNewOp = false;
        Button btn = (Button) view;
        tvInput.append(btn.getText().toString());
    }

    public void operatorEvent(View view) {
        Button btn = (Button) view;
        operator = btn.getText().toString();
        num1 = Double.parseDouble(tvInput.getText().toString());
        isNewOp = true;
        tvExpression.setText(num1 + " " + operator);
    }

    public void equalEvent(View view) {
        num2 = Double.parseDouble(tvInput.getText().toString());
        double result = 0;

        switch (operator) {
            case "+":
                result = num1 + num2;
                break;
            case "−":
                result = num1 - num2;
                break;
            case "×":
                result = num1 * num2;
                break;
            case "÷":
                if (num2 != 0) result = num1 / num2;
                else {
                    tvInput.setText("Error");
                    tvExpression.setText("");
                    return;
                }
                break;
        }

        tvExpression.setText(num1 + " " + operator + " " + num2);
        tvInput.setText(String.valueOf(result));
        isNewOp = true;
    }

    public void plusMinusEvent(View view) {
        String val = tvInput.getText().toString();
        if (val.isEmpty()) return;
        double num = Double.parseDouble(val);
        num = -num;
        tvInput.setText(String.valueOf(num));
    }

    public void dotEvent(View view) {
        String val = tvInput.getText().toString();
        if (!val.contains(".")) tvInput.append(".");
    }
}

```

Activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:background="#F5F5F5"
    android:padding="12dp"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    
    <TextView
        android:id="@+id/tvExpression"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text=""
        android:textColor="#757575"
        android:textSize="20sp"
        android:gravity="end"
        android:padding="8dp" />

    
    <TextView
        android:id="@+id/tvInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text=""
        android:textColor="#212121"
        android:textSize="34sp"
        android:gravity="end"
        android:padding="16dp"
        android:background="#E0E0E0" />

    
    <View
        android:layout_width="match_parent"
        android:layout_height="1dp"
        android:background="#BDBDBD"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp" />

    
    <GridLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:columnCount="4"
        android:rowCount="5"
        android:alignmentMode="alignMargins"
        android:rowOrderPreserved="false"
        android:layout_marginTop="10dp">

        
        <Button
            android:layout_width="17dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1"
            android:layout_margin="5dp"
            android:backgroundTint="#009688"
            android:onClick="clearEvent"
            android:text="C"
            android:textColor="#FFFFFF"
            android:textSize="20sp" />

        <Button
            android:text="("
            android:onClick="operatorEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#FFFFFF"
            android:textSize="20sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text=")"
            android:onClick="operatorEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#FFFFFF"
            android:textSize="20sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="÷"
            android:onClick="operatorEvent"
            android:backgroundTint="#7E57C2"
            android:textColor="#FFFFFF"
            android:textSize="20sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        
        <Button
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1"
            android:layout_margin="5dp"
            android:backgroundTint="#CE93D8"
            android:onClick="numberEvent"
            android:text="7"
            android:textColor="#000000"
            android:textSize="22sp" />

        <Button
            android:text="8"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="9"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="×"
            android:onClick="operatorEvent"
            android:backgroundTint="#7E57C2"
            android:textColor="#FFFFFF"
            android:textSize="20sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        
        <Button
            android:text="4"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="5"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="6"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="−"
            android:onClick="operatorEvent"
            android:backgroundTint="#7E57C2"
            android:textColor="#FFFFFF"
            android:textSize="20sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        
        <Button
            android:text="1"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="2"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="3"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="+"
            android:onClick="operatorEvent"
            android:backgroundTint="#7E57C2"
            android:textColor="#FFFFFF"
            android:textSize="20sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />
      <Button
            android:text="0"
            android:onClick="numberEvent"
            android:backgroundTint="#CE93D8"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="2" />

        <Button
            android:text="."
            android:onClick="numberEvent"
            android:backgroundTint="#7E57C2"
            android:textColor="#000000"
            android:textSize="22sp"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

        <Button
            android:text="="
            android:onClick="equalEvent"
            android:backgroundTint="#7E57C2"
            android:textColor="#795548"
            android:textSize="22sp"
            android:textStyle="bold"
            android:layout_margin="5dp"
            android:layout_width="0dp"
            android:layout_height="80dp"
            android:layout_columnWeight="1" />

    </GridLayout>

</LinearLayout>

```


### Output:

<img width="1919" height="1079" alt="Screenshot 2025-10-28 140436" src="https://github.com/user-attachments/assets/d590eefa-9e7d-464a-8dc4-7fc99ea0ceb6" />

### Execution :

<img width="1919" height="1079" alt="Untitled design (23)" src="https://github.com/user-attachments/assets/89d701d9-93e7-4e42-8654-de07f27eb557" />

<img width="1919" height="1079" alt="Untitled design (24)" src="https://github.com/user-attachments/assets/a4d452d5-e233-44f3-8312-78f2e321306c" />

<img width="1919" height="1079" alt="Untitled design (25)" src="https://github.com/user-attachments/assets/06aba1b6-0801-4bd4-9acc-be381ee64b1b" />

<img width="1919" height="1079" alt="Untitled design (26)" src="https://github.com/user-attachments/assets/1ce13dae-a07a-43b6-a3d5-90377ecb8894" />

<img width="1919" height="1079" alt="Untitled design (27)" src="https://github.com/user-attachments/assets/d74a90f7-f7ee-40b0-ac8a-1668282927c7" />



### RESULT:

Thus, a simple calculator application was successfully developed and executed using Android Studio.
