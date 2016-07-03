# AndSes8Ass3

MainActivity.java
package me.rk.andses8ass3;

import android.os.AsyncTask;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ProgressBar;

public class MainActivity extends AppCompatActivity {
    private Button startparallelButton;
    private ProgressBar progressBar1;
    private ProgressBar progressBar2;
    private ProgressBar progressBar3;
    private ProgressBar progressBar4;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        progressBar1 = (ProgressBar) findViewById(R.id.progressBar1);
        progressBar2 = (ProgressBar) findViewById(R.id.progressBar2);
        progressBar3 = (ProgressBar) findViewById(R.id.progressBar3);
        progressBar4 = (ProgressBar) findViewById(R.id.progressBar4);
        startparallelButton = (Button) findViewById(R.id.startparalleldownload);
        startparallelButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                AppAsyncTask appAsyncTask = new AppAsyncTask(MainActivity.this, progressBar1, progressBar2, progressBar3, progressBar4);
                appAsyncTask.execute();
            }
        });

        class download extends AsyncTask<Void, Integer, String>{
            @Override
            protected String doInBackground(Void... params) {
                for (int i = 0; i <= 100;i++) {
                    try {
                        Thread.sleep(300);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    publishProgress(i);
                }
                return null;
            }
            @Override
            protected void onProgressUpdate(Integer... values) {
                progressBar1.setProgress(values[0]);
                progressBar2.setProgress(values[0]);
                super.onProgressUpdate(values);
            }
        }
        download d1=new download();
        d1.execute();
    }
}

AppAsyncTask.java
package me.rk.andses8ass3;

import android.content.Context;
import android.os.AsyncTask;
import android.view.View;
import android.widget.ProgressBar;

/**
 * Created by airodyra on 7/2/2016.
 */
public class AppAsyncTask extends AsyncTask<Void, Integer, String> {
    private ProgressBar mprogressBar3;
    private ProgressBar mprogressBar4;


    public AppAsyncTask (Context context, ProgressBar progressBar1, ProgressBar progressBar2, ProgressBar progressBar3,ProgressBar progressBar4){
        mprogressBar3=progressBar3;
        mprogressBar4=progressBar4;
    }

    @Override
    protected void onPreExecute() {
        mprogressBar3.setVisibility(View.VISIBLE);
        mprogressBar4.setVisibility(View.VISIBLE);
        super.onPreExecute();
    }

    @Override
    protected String doInBackground(Void... params) {
        for (int i = 0; i <= 100;i++) {
            try {
                Thread.sleep(300);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            publishProgress(i);
        }
        return null;
    }

    @Override
    protected void onProgressUpdate(Integer... values) {

        mprogressBar3.setProgress(values[0]);
        mprogressBar4.setProgress(values[0]);
        super.onProgressUpdate(values);
    }

    @Override
    protected void onPostExecute(String s) {
        super.onPostExecute(s);
    }
}

activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="me.rk.andses8ass3.MainActivity">

    <Button
        android:id="@+id/startparalleldownload"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Start Parallel Download"
        android:padding="10dp"/>

    <ProgressBar
    style="?android:attr/progressBarStyleHorizontal"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:id="@+id/progressBar1"
    android:layout_below="@+id/startparalleldownload"
    android:layout_alignParentStart="true"
    android:padding="10dp" />

    <ProgressBar
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/progressBar2"
        android:layout_below="@+id/progressBar1"
        android:layout_alignParentStart="true"
        android:padding="10dp" />

    <ProgressBar
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/progressBar3"
        android:layout_below="@+id/progressBar2"
        android:layout_alignParentStart="true"
        android:padding="10dp" />

    <ProgressBar
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/progressBar4"
        android:layout_below="@+id/progressBar3"
        android:layout_alignParentStart="true"
        android:padding="10dp" />

</RelativeLayout>



