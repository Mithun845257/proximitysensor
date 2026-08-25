# Ex.No:5 Develop a simple application for proximity sensor using Sensor Manager in android studio.


## AIM:

To develop a sensor application for proximity sensor using sensor manager in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Giraffe)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as proximitysensor and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display process of proximitysensor in android mobile devices.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the process of proximitysensor in android mobile devices”.
Developed by:Mithun G
Registeration Number :212225040235
*/
```
MAINACTIVITY.JAVA
```
package com.example.proximitysensorapp;

import androidx.appcompat.app.AppCompatActivity;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity implements SensorEventListener {

    private SensorManager sensorManager;
    private Sensor proximitySensor;
    private TextView tvStatus;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tvStatus = findViewById(R.id.tvStatus);

        sensorManager = (SensorManager) getSystemService(SENSOR_SERVICE);

        if (sensorManager != null) {
            proximitySensor =
                    sensorManager.getDefaultSensor(Sensor.TYPE_PROXIMITY);
        }

        if (proximitySensor == null) {
            tvStatus.setText("This device has NO proximity sensor.");

            Toast.makeText(
                    this,
                    "No proximity sensor found",
                    Toast.LENGTH_LONG
            ).show();

        } else {
            tvStatus.setText(
                    "Proximity sensor ready.\nMove your hand near the top of the phone."
            );
        }
    }

    @Override
    protected void onResume() {
        super.onResume();

        if (proximitySensor != null) {
            sensorManager.registerListener(
                    this,
                    proximitySensor,
                    SensorManager.SENSOR_DELAY_NORMAL
            );
        }
    }

    @Override
    protected void onPause() {
        super.onPause();

        if (sensorManager != null) {
            sensorManager.unregisterListener(this);
        }
    }

    @Override
    public void onSensorChanged(SensorEvent event) {

        if (event.sensor.getType() == Sensor.TYPE_PROXIMITY) {

            float distance = event.values[0];
            float maxRange = proximitySensor.getMaximumRange();

            if (distance < maxRange) {

                tvStatus.setText(
                        "Object is NEAR\nDistance: " + distance + " cm"
                );

                getWindow().getDecorView().setBackgroundColor(
                        getResources().getColor(android.R.color.holo_red_dark)
                );

            } else {

                tvStatus.setText(
                        "Object is FAR\nDistance: " + distance + " cm"
                );

                getWindow().getDecorView().setBackgroundColor(
                        getResources().getColor(android.R.color.holo_green_dark)
                );
            }
        }
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {
        // Not required
    }
}
```
ACTIVITY.XML
```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp"
    tools:context=".MainActivity">

    <com.google.android.material.textview.MaterialTextView
        android:id="@+id/tvTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Proximity Sensor"
        android:textSize="28sp"
        android:textStyle="bold"
        android:layout_marginBottom="40dp"/>

    <com.google.android.material.textview.MaterialTextView
        android:id="@+id/tvStatus"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Waiting for sensor data..."
        android:textSize="22sp"
        android:gravity="center"/>

</LinearLayout>

## OUTPUT
<img width="1920" height="1080" alt="Screenshot (91)" src="https://github.com/user-attachments/assets/a0933032-f5c4-41ee-99d6-72be50475cf7" />

<img width="1920" height="1080" alt="Screenshot (92)" src="https://github.com/user-attachments/assets/1ae41293-8f57-47d9-8ee0-ef47b3bc9f65" />



## RESULT
Thus a Simple Android Application to display the details of proximity sensor using sensor manager in Android Studio is developed and executed successfully.
