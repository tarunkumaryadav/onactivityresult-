# onactivityresult-
sending data from one activity to 2nd activity and to 1st again

package com.resultrestore;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.view.View.OnClickListener;

public class MainActivity extends Activity implements OnClickListener {
    Button mbtnGetResult;
    EditText metName, metAge, metPhone;
    TextView mtvResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mbtnGetResult = (Button) findViewById(R.id.activity_main_submit_button);
        metName = (EditText) findViewById(R.id.activity_main_name_editText);
        metAge = (EditText) findViewById(R.id.activity_main_age_editText);
        metPhone = (EditText) findViewById(R.id.activity_main_phone_editText);
        mtvResult = (TextView) findViewById(R.id.activity_main_pincode_textView);

        mbtnGetResult.setOnClickListener(this);


    }

    public void onClick(View view) {

        // 1. create an intent pass class name or  action name
        Intent intent = new Intent(this, GetData.class);


        intent.putExtra("NAME", metName.getText().toString().trim());
        intent.putExtra("AGE", metAge.getText().toString());
        intent.putExtra("PHONE", metPhone.getText().toString());

        // 3. start the activity
        startActivityForResult(intent, 100);
    }

    protected void onActivityResult(int requestCode, int resultCode, Intent data) {

        if (resultCode == RESULT_OK) {
            if (requestCode == 100) {
                String str = data.getExtras().getString("result");
                mtvResult.setText(str);
            }
        }

    }


    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.menu_main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
}



package com.resultrestore;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
/**
 * Created by tarun on 30/6/15.
 */
public class GetData extends Activity implements OnClickListener {

    TextView mtvName,mtvAge,mtvPhone;
    Button mbtnSendResult;
    EditText meditTextPin;

    protected void onCreate(Bundle savedInstanceState) {
        // TODO Auto-generated method stub
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_getdata);

        mbtnSendResult = (Button) findViewById(R.id.activity_getdata_sendback_button);
        mbtnSendResult.setOnClickListener(this);

        //Intent intent = getIntent();
        String value = getIntent().getStringExtra("NAME");
        String value2 = getIntent().getStringExtra("AGE");
        String value3 = getIntent().getStringExtra("PHONE");
        mtvName = (TextView) findViewById(R.id.activity_getdata_name_textView);
        mtvAge = (TextView) findViewById(R.id.activity_getdata_age_textView);
        mtvPhone = (TextView) findViewById(R.id.activity_getdata_phone_textView);

        mtvName.setText(value);
        mtvAge.setText(value2);
        mtvPhone.setText(value3);



        meditTextPin=(EditText)findViewById(R.id.activity_getdata_pincode_editText4);
    }
    public void onClick(View view) {

        Intent returnIntent = new Intent();

        returnIntent.putExtra("result",meditTextPin.getText().toString().trim());

        setResult(RESULT_OK,returnIntent);
        finish();
    }
}


<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
    android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/activity_main_name_editText"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"

        />

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/activity_main_age_editText"
        android:layout_below="@+id/activity_main_name_editText"
        android:layout_alignLeft="@+id/activity_main_name_editText"
        android:layout_alignStart="@+id/activity_main_name_editText"
        android:layout_marginTop="54dp" />

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/activity_main_phone_editText"
        android:layout_marginTop="66dp"
        android:layout_below="@+id/activity_main_age_editText"
        android:layout_alignLeft="@+id/activity_main_age_editText"
        android:layout_alignStart="@+id/activity_main_age_editText" />


    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Submit"
        android:id="@+id/activity_main_submit_button"
        android:textSize="30dp"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="350dp"

        />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"

        android:id="@+id/activity_main_pincode_textView"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true" />
</RelativeLayout>



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    >

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text=""
        android:layout_marginTop="50dp"
        android:id="@+id/activity_getdata_name_textView" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="50dp"
        android:text=""
        android:id="@+id/activity_getdata_age_textView" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text=""
        android:layout_marginTop="50dp"
        android:id="@+id/activity_getdata_phone_textView" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Send Back"
        android:id="@+id/activity_getdata_sendback_button"
        android:layout_gravity="center_horizontal" />

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/activity_getdata_pincode_editText4"
        android:layout_marginTop="50dp"
        android:layout_gravity="center_horizontal" />

</LinearLayout>
