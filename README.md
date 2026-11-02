
# Ex.No:2 To create a employee details fields and to display the employee details using Firebase Database in Android Studio.


## AIM:

To create and display the employee details using Firebase Database in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display the employee details in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the DatabaseTable using the firebasedatabase”.
Developed by:SANDEEP S
Registeration Number :212223220092
*/
```
```
/*
Main Activity in Java Folder
package com.example.ex_01_realtimedatabase;

import android.os.Bundle;
import android.widget.*;

import androidx.appcompat.app.AppCompatActivity;

import com.google.firebase.database.*;

import java.util.*;

public class MainActivity extends AppCompatActivity {

    EditText etName, etAge, etSalary;
    Button btnAdd, btnUpdate, btnDelete;
    ListView listView;

    DatabaseReference dbRef;

    ArrayList<String> items = new ArrayList<>();
    ArrayList<String> keys = new ArrayList<>();

    ArrayAdapter<String> adapter;

    String selectedKey = null;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        // Initialize views
        etName = findViewById(R.id.etName);
        etAge = findViewById(R.id.etAge);
        etSalary = findViewById(R.id.etSalary);

        btnAdd = findViewById(R.id.btnAdd);
        btnUpdate = findViewById(R.id.btnUpdate);
        btnDelete = findViewById(R.id.btnDelete);

        listView = findViewById(R.id.listView);

        // Firebase reference
        dbRef = FirebaseDatabase.getInstance().getReference("Employees");

        // ListView adapter
        adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,
                items
        );

        listView.setAdapter(adapter);

        // Read data from Firebase
        dbRef.addValueEventListener(new ValueEventListener() {

            @Override
            public void onDataChange(DataSnapshot snapshot) {

                items.clear();
                keys.clear();

                for (DataSnapshot d : snapshot.getChildren()) {

                    Emp e = d.getValue(Emp.class);

                    if (e != null) {
                        items.add(e.name + " | " + e.age + " | " + e.salary);
                        keys.add(d.getKey());
                    }
                }

                adapter.notifyDataSetChanged();
            }

            @Override
            public void onCancelled(DatabaseError error) {
            }
        });

        // Add employee
        btnAdd.setOnClickListener(v -> {

            Emp e = new Emp(
                    etName.getText().toString(),
                    etAge.getText().toString(),
                    etSalary.getText().toString()
            );

            dbRef.push().setValue(e);

            clearFields();
        });

        // Update employee
        btnUpdate.setOnClickListener(v -> {

            if (selectedKey != null) {

                Emp e = new Emp(
                        etName.getText().toString(),
                        etAge.getText().toString(),
                        etSalary.getText().toString()
                );

                dbRef.child(selectedKey).setValue(e);

                clearFields();

            } else {

                Toast.makeText(
                        this,
                        "Select an item first",
                        Toast.LENGTH_SHORT
                ).show();
            }
        });

        // Delete employee
        btnDelete.setOnClickListener(v -> {

            if (selectedKey != null) {

                dbRef.child(selectedKey).removeValue();

                clearFields();

            } else {

                Toast.makeText(
                        this,
                        "Select an item first",
                        Toast.LENGTH_SHORT
                ).show();
            }
        });

        // Select employee from ListView
        listView.setOnItemClickListener((p, v, pos, id) -> {

            selectedKey = keys.get(pos);

            dbRef.child(selectedKey).get().addOnSuccessListener(d -> {

                Emp e = d.getValue(Emp.class);

                if (e != null) {

                    etName.setText(e.name);
                    etAge.setText(e.age);
                    etSalary.setText(e.salary);
                }
            });
        });
    }

    // Clear input fields
    private void clearFields() {

        etName.setText("");
        etAge.setText("");
        etSalary.setText("");

        selectedKey = null;
    }
}
*/
```
```
/*
Layout part “Design” “activity_mail.xml”
```xml
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <!-- Name -->
    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="55dp"
        android:hint="Name" />

    <!-- Age -->
    <EditText
        android:id="@+id/etAge"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Age"
        android:inputType="number" />

    <!-- Salary -->
    <EditText
        android:id="@+id/etSalary"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Salary"
        android:inputType="number" />

    <!-- Buttons -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnAdd"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Add" />

        <Button
            android:id="@+id/btnUpdate"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Update" />

        <Button
            android:id="@+id/btnDelete"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Delete" />

    </LinearLayout>

    <!-- ListView -->
    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
*/
```

## OUTPUT
<img width="1535" height="814" alt="image" src="https://github.com/user-attachments/assets/b77d52c0-9249-48c0-a887-82e9606c85eb" />
<img width="1535" height="814" alt="image" src="https://github.com/user-attachments/assets/d189a729-95ed-4798-ad04-9cb7e9c4b9c7" />
<img width="1514" height="822" alt="image" src="https://github.com/user-attachments/assets/f33379d0-b55c-4a2c-b3bd-ffade742ab18" />



## RESULT
Thus a Simple Android Application create a firebase database and to display the employee details using Firbase Real Time Database in Android Studio is developed and executed successfully.
