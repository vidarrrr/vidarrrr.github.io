---
layout: post
title: Scrollview => ConstraintLayout => Listview Implementation (My opinion)
---

Link to [Source](https://stackoverflow.com/questions/43098150/android-how-to-make-a-scrollable-constraintlayout)

NestedScrollView freezes the listview so you can't slide. But we can do it with the scrollview.


**activity_main.xml** 

<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fillViewport="true" //fill the view
    >

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"

        android:layout_height="match_parent"
        android:adjustViewBounds="true"
        android:background="#ffffff"
        android:orientation="vertical"
        android:scaleType="fitCenter"> 
        <!--android:padding="10dp"-->
       
	   <TextView
            android:id="@+id/text1"
            android:layout_width="match_parent"
            android:layout_height="40dp"

            android:text="@string/string"

            app:layout_constraintTop_toTopOf="parent" />
	   
        <ListView
            android:id="@+id/listView"
            android:layout_width="match_parent"
            android:layout_height="200dp"

            android:layout_marginBottom="10dp"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"

            app:layout_constraintTop_toBottomOf="@id/text1"

            />

    </androidx.constraintlayout.widget.ConstraintLayout>
</ScrollView>


